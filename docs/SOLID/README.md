### Definition
Solid Principles are sets of principles in Object Oriented Software Development. SOLID is an acronym for five design principles intended to make software design more understandable, flexible and maintainable.

### Origin
- SOLID principles are subset of many principles promoted by Robert C. Martin (Uncle Bob)
- The SOLID acronym was first introduced by Michael Feathers

### SRP - Single Responsibility Principle
- A Class should have only one reason to change (A class should do only one job).

Benifits
- Maintainability
- Testability
- Flexibility and Extensibility
- Parallel Development
- Loose coupling

```csharp
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
- 
```
// Bad  
class Employee
{
    public string EmployeeType { get; set; }
    public decimal Salary { get; set; }
    
    public Employee(string employeeType, decimal salary)
    {
        this.EmployeeType = employeeType;
        this.Salary = salary;
    }

    public decimal GetBonusAmount()
    {
        if (this.EmployeeType == "permanent")
        {
            return this.Salary * 1;
        }
        
        return this.Salary * 0.5;
    }
}

// Good  
class Employee
{
    public string EmployeeType { get; set; }
    public decimal Salary { get; set; }
    
    public Employee(string employeeType, decimal salary)
    {
        this.EmployeeType = employeeType;
        this.Salary = salary;
    }

    public decimal GetBonusAmount()
    {
        return this.Salary * 0.5;
    }
}

class PermanentEmployee
{
    public decimal GetBonusAmount()
    {
        return this.Salary * 1;
    }
}
class TemporaryEmployee
{
    public decimal GetBonusAmount()
    {
        return this.Salary * 0.5;
    }
}
```

### LSP - Liskov Substitution Principle
- Objects in a program should be replaceable with instances of thier subtypes without altering the correctness of that program.
- Reference of base class can be replaced with derived class without affecting the functionality of the program module.
- Derived types should be substitutable for its base types
- Extension of OCP

Implementation Guidelines
- No new exceptions can be thrown by the sub type
- Client should not know which specific subtype they are calling
- New derived classes just extend without replacing the funcitonality of old classes

```
// Bad - For Contract employees there will not be any bonus amount.
interface IEmployee
{
    DateTime GetJoiningDate();
    bool CalculateBonus();
}

class PermanentEmployee: IEmployee
{
    DateTime GetJoiningDate()
    {
        // .... implementation
    }
    public bool CalculateBonus()
    {
        return 10000;
    }
}
class ContractEmployee: IEmployee
{
    DateTime GetJoiningDate()
    {
        // .... implementation
    }
    public bool CalculateBonus()
    {
        throw new NotImplementedException();
    }
}

// Good
interface IEmployee
{
    DateTime GetJoiningDate();   
}
interface IEmployeeBonus
{
    bool CalculateBonus();
}

class PermanentEmployee: IEmployee, IEmployeeBonus
{
    DateTime GetJoiningDate()
    {
        // .... implementation
    }
    public bool CalculateBonus()
    {
        return 10000;
    }
}
class ContractEmployee: IEmployee
{
    DateTime GetJoiningDate()
    {
        // .... implementation
    }
}

// usage
IEmployee emp = new ContractEmployee();
IEmployee pEmp = new PermanentEmployee();
IEmployeeBonus pBonusEmp = new PermanentEmployee();
```

### ISP - Interface Segregation Principle
- A client should never be forced to implement an interface that it doesn’t use.
- One fat intreface need to be split to many smaller and relevant interfaces so that clients can known about the interfaces that are relevant to them.

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

### DIP - Dependency Inversion Principle
- Entities must depend on abstractions, not on concretions.
- High level modules should not depend on low level modules

```
// Consider
interface ILogger
{
    void Log();
}
class Logger: ILogger
{
    public void Log() {}
}

// Bad
class User
{
    private ILogger _logger;
    
    public User()
    {
        this._logger = new Logger();
    }
    
    public SaveUser()
    {
        //.... implementation
        _logger.Log();
    } 
}

// Good
class User
{
    private ILogger _logger;
    
    public User(ILogger logger)
    {
        this._logger = logger;
    }
    
    public SaveUser()
    {
        //.... implementation
        _logger.Log();
    } 
}
```

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
