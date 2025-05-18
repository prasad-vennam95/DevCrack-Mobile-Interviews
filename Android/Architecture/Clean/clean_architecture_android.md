# Clean Architecture in Android

Clean Architecture is a software design pattern that promotes separation of concerns and organizes code into distinct layers. It helps in building maintainable, testable, and scalable applications. In Android, Clean Architecture typically consists of three main layers:

## 1. **Presentation Layer**
- Handles the UI and user interactions.
- Contains Activities, Fragments, ViewModels, and UI-related logic.
- Communicates with the domain layer to fetch or update data.

## 2. **Domain Layer**
- The core of the application, independent of frameworks or external libraries.
- Contains business logic and use cases.
- Interfaces for repositories are defined here to abstract data sources.

## 3. **Data Layer**
- Responsible for data management.
- Contains implementations of repositories, APIs, and database access.
- Converts raw data into domain models for the domain layer.

### Benefits of Clean Architecture:
- **Separation of Concerns**: Each layer has a specific responsibility.
- **Testability**: Business logic can be tested independently of UI or data sources.
- **Scalability**: Easy to add new features without affecting other layers.
- **Maintainability**: Clear structure makes it easier to understand and modify the code.

### Diagram of Clean Architecture:
```
[ Presentation Layer ]
            |
[  Domain Layer  ]
            |
[   Data Layer   ]
```

By following Clean Architecture, Android developers can create robust and flexible applications.

---

## Example of Clean Architecture in Android

### Use Case: Fetching a List of Users

### 1. **Presentation Layer**
```kotlin
class UserViewModel(private val getUsersUseCase: GetUsersUseCase) : ViewModel() {
    val users = MutableLiveData<List<User>>()
    val error = MutableLiveData<String>()

    fun fetchUsers() {
        viewModelScope.launch {
            try {
                users.value = getUsersUseCase.execute()
            } catch (e: Exception) {
                error.value = e.message
            }
        }
    }
}
```

### 2. **Domain Layer**
```kotlin
data class User(val id: Int, val name: String)

interface UserRepository {
    suspend fun getUsers(): List<User>
}

class GetUsersUseCase(private val userRepository: UserRepository) {
    suspend fun execute(): List<User> {
        return userRepository.getUsers()
    }
}
```

### 3. **Data Layer**
```kotlin
class UserRepositoryImpl(private val apiService: ApiService) : UserRepository {
    override suspend fun getUsers(): List<User> {
        return apiService.fetchUsers().map { User(it.id, it.name) }
    }
}

data class ApiUser(val id: Int, val name: String)

interface ApiService {
    suspend fun fetchUsers(): List<ApiUser>
}
```

### Dependency Injection Example (Koin)
```kotlin
val appModule = module {
    single<ApiService> { ApiServiceImpl() }
    single<UserRepository> { UserRepositoryImpl(get()) }
    factory { GetUsersUseCase(get()) }
    viewModel { UserViewModel(get()) }
}
```

This example demonstrates how each layer interacts while maintaining separation of concerns. The `Presentation Layer` interacts with the `Domain Layer` through the `GetUsersUseCase`, and the `Domain Layer` interacts with the `Data Layer` through the `UserRepository` interface.

---

## Common Interview Questions on Clean Architecture

### Conceptual Questions
1. What is Clean Architecture, and why is it important in Android development?
2. Can you explain the different layers of Clean Architecture and their responsibilities?
3. How does Clean Architecture promote separation of concerns?
4. What are the benefits of using Clean Architecture in a project?

### Practical Questions
1. How would you implement a new feature using Clean Architecture?
2. Can you explain how dependency inversion is applied in Clean Architecture?
3. How do you handle communication between layers in Clean Architecture?
4. How would you test the business logic in the domain layer?

### Code-Based Questions
1. Write a simple use case for fetching data from a repository using Clean Architecture.
2. How would you implement a repository pattern in the data layer?
3. Can you demonstrate how to inject dependencies into a ViewModel using a DI framework like Koin or Dagger?

### Scenario-Based Questions
1. If a new data source is introduced, how would you integrate it into an existing Clean Architecture setup?
2. How would you refactor a tightly coupled codebase to follow Clean Architecture principles?
3. What challenges have you faced while implementing Clean Architecture, and how did you overcome them?

## Comparison with Other Architectures

### Conceptual Questions
1. How does Clean Architecture differ from MVVM, MVP, MVI, and MVC?
2. What are the advantages of Clean Architecture over MVVM or MVP in terms of scalability and testability?
3. Can you explain how the separation of concerns in Clean Architecture compares to that in MVC or MVP?
4. Why might you choose Clean Architecture over MVI for a complex application?

### Practical Questions
1. How would you migrate an existing MVVM or MVP-based project to Clean Architecture?
2. What challenges might arise when transitioning from MVC to Clean Architecture?
3. How does the role of ViewModels in MVVM differ from their role in Clean Architecture?
4. How does Clean Architecture handle state management compared to MVI?

### Code-Based Questions
1. Demonstrate how you would refactor an MVP Presenter into a Clean Architecture Use Case.
2. How would you adapt an MVVM ViewModel to fit into the Presentation Layer of Clean Architecture?
3. Write a comparison of how data flows in Clean Architecture versus MVI.

### Scenario-Based Questions
1. If you were working on a legacy MVC project, how would you introduce Clean Architecture principles incrementally?
2. In what scenarios would you prefer MVVM or MVP over Clean Architecture, and why?
3. How would you handle shared state across multiple screens in Clean Architecture compared to MVI?
4. What trade-offs should be considered when choosing between Clean Architecture and simpler patterns like MVVM or MVP for a small project?