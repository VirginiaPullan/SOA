// UserService.java
public interface UserService {
    User getUserById(long id);
    List<User> getAllUsers();
    void createUser(User user);
    void updateUser(User user);
    void deleteUser(long id);
}

// UserServiceImpl.java
public class UserServiceImpl implements UserService {
    private UserRepository userRepository;

    public UserServiceImpl(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    @Override
    public User getUserById(long id) {
        return userRepository.findById(id);
    }

    @Override
    public List<User> getAllUsers() {
        return userRepository.findAll();
    }

    @Override
    public void createUser(User user) {
        userRepository.save(user);
    }

    @Override
    public void updateUser(User user) {
        userRepository.update(user);
    }

    @Override
    public void deleteUser(long id) {
        userRepository.delete(id);
    }
}

// UserRepository.java
public interface UserRepository {
    User findById(long id);
    List<User> findAll();
    void save(User user);
    void update(User user);
    void delete(long id);
}

// User.java
public class User {
    private long id;
    private String username;
    private String email;
    
    // Getters and setters
}

// UserController.java
public class UserController {
    private UserService userService;

    public UserController(UserService userService) {
        this.userService = userService;
    }

    public ResponseEntity<User> getUserById(long id) {
        User user = userService.getUserById(id);
        if (user != null) {
            return ResponseEntity.ok(user);
        } else {
            return ResponseEntity.notFound().build();
        }
    }

    public ResponseEntity<List<User>> getAllUsers() {
        List<User> users = userService.getAllUsers();
        return ResponseEntity.ok(users);
    }

    public ResponseEntity<Void> createUser(User user) {
        userService.createUser(user);
        return ResponseEntity.ok().build();
    }

    public ResponseEntity<Void> updateUser(long id, User user) {
        userService.updateUser(user);
        return ResponseEntity.ok().build();
    }

    public ResponseEntity<Void> deleteUser(long id) {
        userService.deleteUser(id);
        return ResponseEntity.ok().build();
    }
}
