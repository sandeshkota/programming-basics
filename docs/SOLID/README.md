Solid Principles are sets of principles in Object Oriented Software Development. SOLID is an acronym for five design principles intended to make software design more understandable, flexible and maintainable.

### origin
- SOLID principles are subset of many principles promoted by Robert C. Martin (Uncle Bob)
- The SOLID acronym was first introduced by Michael Feathers

### SRP - Single Responsibility Principle
- A Class should have only one reason to change (A class should do only one job).

#### benifits
- Maintainability
- Testability
- Flexibility and Extensibility
- Parallel Development
- Loose coupling

```
// Bad
interface IUser
{
    bool Login(string userName, string password);
    bool Register(string userName, string password, string email);
    bool SendEmail(string emailContent);
}

// Good
interface IUser
{
    bool Login(string userName, string password);
    bool Register(string userName, string password, string email);
}
interface IEmail
{
    bool SendEmail(string emailContent);
}
```

### OCP - Open Close Principle
- Software Entities should be open for extension and closed for modification.

### LSP - Liskov Substitution Principle
- Objects in a program should be replaceable with instances of thier subtypes without altering the correctness of that program.
- Reference of base class can be replaced with derived class without affecting the functionality of the program module.
- Derived types should be substitutable for its base types

### ISP - Interface Segregation Principle
- A client should never be forced to implement an interface that it doesn’t use.

### DIP - Dependency Inversion Principle
- Entities must depend on abstractions, not on concretions.
- High level modules should not depend on low level modules


### If not followed
- End up with tight coupling with other modules
- Impacts testability of the code
- Increases TTM (Time to market) - Takes time to do changes (any enhancement)
- Posibility of Code duplication
- Prone to issues during modification

### If followed
- Reduces the complexity and hence increases readability, flexibility and maintainability
- Better testability
- Reduces coupling
