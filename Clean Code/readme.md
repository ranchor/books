## Chapter 1: Clean Code

### Key Points:
1. **Definition of Clean Code**:
   - Clean code is **simple**, **focused**, **readable**, and **efficient**.
   - It is easy to understand, even by someone unfamiliar with the code.
   - It minimizes dependencies and avoids complexity.

2. **Characteristics of Clean Code**:
   - **Readable**: Anyone reading the code can understand its purpose and how it works. It is self-explanatory.
   - **Simple**: It solves the problem in the least complicated way possible.
   - **Well-structured**: Code should have a clear structure with appropriate separation of concerns.
   - **Minimal**: There should be no superfluous lines or unnecessary complexity.

3. **Understanding from Experts**:
   - **Bjarne Stroustrup**: Code should be both correct and elegant. Efficiency should never sacrifice clarity.
   - **Grady Booch**: Clean code is written for **humans** first and **machines** second. Readability is key.

4. **Bad Code vs. Clean Code**:
   - Bad code works, but it is **fragile**, hard to understand, and maintain.
   - Clean code evolves and improves. As programmers, we must avoid leaving bad code behind.
   - **Continuous refactoring** is crucial to maintaining clean code.

### Example (expanded):
```java
// Bad code - poor naming, unclear logic
public int c(int[] a) {
    int r = 0;
    for (int i = 0; i < a.length; i++) {
        r += a[i];
    }
    return r;
}

// Clean code - meaningful names, simple and direct logic
public int sumArray(int[] numbers) {
    int total = 0;
    for (int number : numbers) {
        total += number;
    }
    return total;
}
```



## Chapter 2: Meaningful Names

### Introduction:
In software, names are everywhere—variables, functions, classes, etc. Thus, naming well is critical to clean code. Naming should be done with **intention** and **clarity** to ensure code is easy to understand.

### 1. Intention-Revealing Names
Names should express the purpose or intent of a variable, method, or class clearly. A well-named entity reduces the need for comments, making the code self-explanatory. When someone reads the code, they should easily understand what it represents or what action it performs.

**Example**:
```java
// Bad Example
int d; // unclear what 'd' represents

// Good Example
int elapsedTimeInDays; // Clear and intention-revealing
```

### 2. Avoid Disinformation
Names should not mislead the reader. It’s important to avoid naming variables or functions in a way that might imply incorrect or confusing information. For example, don't name a collection `accountList` if it is not a list but another data structure like a `Set`.

**Example**:
```java
// Bad Example
List<Account> accountList = new LinkedList<>(); // It's a LinkedList, not necessarily a List

// Good Example
List<Account> accounts = new LinkedList<>();
```

### 3. Make Meaningful Distinctions
Names should be distinct and meaningful. Avoid unnecessary words like `Info` or `Data` in names when they don’t provide clarity. The distinction should reflect real differences rather than arbitrary distinctions added to avoid name conflicts.

**Example**:
```java
// Bad Example
getActiveAccountInfo();

// Good Example
getActiveAccount();
```

### 4. Use Pronounceable Names
Choose names that are easy to pronounce. When names are easy to say, it becomes easier to talk about them in discussions or when reviewing code with a team.

**Example**:
```java
// Bad Example
Date genymdhms; // What does 'genymdhms' stand for?

// Good Example
Date generationTimestamp;
```

### 5. Use Searchable Names
It’s important to use names that are easy to search through the codebase. Single-letter variable names or short, vague names are hard to find, especially in large projects. Searchable names increase efficiency when navigating code.

**Example**:
```java
// Bad Example
int e = 5; // 'e' is not easily searchable

// Good Example
int maxEmployees = 5; // Clearly searchable and descriptive
```

### 6. Avoid Encodings
Don’t encode type or scope information into names, such as using prefixes like `i` for integers (Hungarian notation). Modern languages and IDEs handle this information, making it unnecessary and potentially confusing.

**Example**:
```java
// Bad Example
int iNumUsers; // 'i' prefix adds no value

// Good Example
int userCount;
```

### 7. Avoid Mental Mapping
Variables should not require the reader to mentally map them to something else. For example, using single-letter variables like `a`, `b`, or `c` forces readers to translate them mentally into something more meaningful. Variables should be self-explanatory.

**Example**:
```java
// Bad Example
int c = 0; // What does 'c' represent?

// Good Example
int totalSum = 0;
```

### 8. Class Names
Class names should be nouns or noun phrases that describe what the class represents. They should not be verbs. Avoid generic names like "Manager" or "Processor" that don't clarify what the class does.

**Example**:
```java
// Bad Example
public class AccountManager { }

// Good Example
public class AccountService { }
```

### 9. Method Names
Method names should be verbs or verb phrases that describe the action the method performs. This makes the purpose of the method clear.

**Example**:
```java
// Bad Example
public void data() { }

// Good Example
public void retrieveData() { }
```

### 10. Pick One Word per Concept
Be consistent in your terminology across the entire codebase. For example, don’t use `fetch`, `retrieve`, and `get` interchangeably for the same concept. Consistency reduces cognitive load on the reader, making the code easier to understand.

**Example**:
```java
// Bad Example
fetchData(), retrieveData(), getData();

// Good Example
getData() in all cases.
```

### 11. Don’t Pun
Avoid using the same word for two different concepts. The same word for unrelated actions can lead to confusion. Be careful not to overload names with multiple meanings.

**Example**:
```java
// Bad Example
list.add(item);   // Adds an item to a collection
invoice.add(item); // Adds an item to an invoice

// Good Example
list.addItem(item);  
invoice.appendItem(item);
```


## Chapter 3: Functions
### Introduction
Functions are the building blocks of any software system. Writing clean, small, and focused functions is essential to ensuring code is maintainable, easy to understand, and flexible. This chapter emphasizes keeping functions small, doing one thing well, and avoiding side effects.

### 1. Small Functions
Functions should be small, and ideally, even smaller than most developers think. A function should be able to fit in your view without scrolling, generally no longer than 20 lines of code.

**Example**:
```java
// Bad Example - Long function
public void processOrder(Order order) {
    // code for processing order
    // code for logging the order
    // code for sending email
}

// Good Example - Small, focused functions
public void processOrder(Order order) {
    logOrder(order);
    sendOrderEmail(order);
}

private void logOrder(Order order) { /* code */ }
private void sendOrderEmail(Order order) { /* code */ }
```

### 2. Do One Thing
Each function should do **one thing** and do it well. A function that tries to do multiple things introduces complexity and makes the code harder to maintain.

**Example**:
```java
// Bad Example - Doing multiple things
public void handleUserRequest(User user) {
    authenticateUser(user);
    fetchData(user);
    logAccess(user);
}

// Good Example - One thing per function
public void handleUserRequest(User user) {
    authenticateUser(user);
}

private void fetchData(User user) { /* code */ }
private void logAccess(User user) { /* code */ }
```

### 3. Blocks and Indentation
Avoid deep nesting of logic within functions. Ideally, blocks of code (like `if` or `for` statements) should contain **one line**, usually a function call. This keeps the code simple and the function shallow in terms of logic depth.

**Example**:
```java
// Bad Example - Nested blocks and indentation
public void processOrders(List<Order> orders) {
    for (Order order : orders) {
        if (order.isValid()) {
            if (order.hasStock()) {
                process(order);
            }
        }
    }
}

// Clean Example - Simplifying blocks
public void processOrders(List<Order> orders) {
    for (Order order : orders) {
        processValidOrder(order);
    }
}

private void processValidOrder(Order order) {
    if (order.isValid() && order hasStock()) {
        process(order);
    }
}
```

### 4. Use Descriptive Names
Function names should clearly describe **what the function does**. Descriptive names make the code easier to understand and maintain. Don’t be afraid to use long names if they better describe what the function is doing.

**Example**:
```java
// Bad Example - Non-descriptive function name
public void d(Order order) {
    // code
}

// Clean Example - Descriptive function name
public void sendOrderConfirmationEmail(Order order) {
    // code to send email confirmation
}
```

### 5. One Level of Abstraction per Function
Functions should operate at a single level of abstraction. Mixing different abstraction levels within a function makes it harder to understand and maintain. High-level functions should not contain low-level details.

**Example**:
```java
// Bad Example - Mixing abstraction levels
public void saveUser(User user) {
    if (user.getName() != null) {
        db.save(user); // low-level operation
    }
}

// Good Example - Consistent abstraction levels
public void saveUser(User user) {
    validateUser(user);
    saveToDatabase(user);
}

private void saveToDatabase(User user) { /* low-level operation */ }
```

### 6. Function Arguments
The ideal number of arguments for a function is zero. If you must use arguments, keep them to one or two, and avoid using more than three. Too many arguments make functions hard to understand and test. Consider using objects if you have more than three parameters.

**Example**:
```java
// Bad Example - Too many arguments
public void createUser(String name, String email, String address, int age) { /* code */ }

// Good Example - Using an object to group arguments
public void createUser(UserDetails userDetails) { /* code */ }
```

### 7. Avoid Side Effects
Functions should not modify global variables or other hidden states outside their scope. Side effects make it harder to understand what a function does and lead to bugs that are difficult to trace.

**Example**:
```java
// Bad Example - Side effect by modifying external state
public void updateBalance(Account account, int amount) {
    globalBalance += amount;  // side effect
}

// Good Example - No side effect
public void updateBalance(Account account, int amount) {
    account.setBalance(account.getBalance() + amount);  // modifies only local state
}
```

### 8. Command Query Separation - Functions Should Either Do or Ask, Not Both
Functions should either do something (a **command**) or answer something (a **query**), but not both. A function that changes the state of the system while also returning a value can lead to confusion.

**Example**:
```java
// Bad Example - Command and query combined
public boolean setBalance(Account account, int amount) {
    account.setBalance(amount);
    return true;  // changing state and returning a value
}

// Good Example - Separation of command and query
public void setBalance(Account account, int amount) {
    account.setBalance(amount);  // command only
}

public boolean hasSufficientBalance(Account account) {
    return account.getBalance() > 0;  // query only
}
```

### 9. Prefer Exceptions to Returning Error Codes
Returning error codes forces the caller to handle errors immediately, cluttering the main logic of the program. Using exceptions separates error-handling logic from normal flow, making the code cleaner and easier to follow.

**Example**:
```java
// Bad Example - Using error codes
public int deleteFile(File file) {
    if (!file.exists()) {
        return -1;  // error code
    }
    // delete file
    return 0;  // success
}

// Good Example - Using exceptions
public void deleteFile(File file) throws FileNotFoundException {
    if (!file.exists()) {
        throw new FileNotFoundException();
    }
    // delete file
}
```

### 10. DRY (Don't Repeat Yourself)
Avoid duplicating code across functions. Duplicate code not only increases the size of the codebase but also makes it harder to maintain and introduces inconsistencies. Instead, refactor common logic into reusable functions.

**Example**:
```java
// Bad Example - Repeated code
public void printUserDetails(User user) {
    System.out.println(user.getName());
    System.out.println(user.getEmail());
}

public void printAdminDetails(Admin admin) {
    System.out.println(admin.getName());
    System.out.println(admin.getEmail());
}

// Good Example - Reusable function
public void printPersonDetails(Person person) {
    System.out.println(person.getName());
    System.out.println(person.getEmail());
}
```


## Chapter 4: Comments

### Introduction
Comments are often seen as a way to clarify code, but they should be used sparingly and only when necessary. Ideally, code should be self-explanatory, reducing the need for comments. Comments can become outdated or misleading, and in many cases, they are a sign that the code itself could be improved for clarity.

### 1. Comments Do Not Make Up for Bad Code
Comments should not be used as a crutch for bad or unclear code. Instead of using a comment to explain confusing logic, the code should be refactored to make it more understandable. Good code is often self-explanatory and does not require comments to describe what it does.

**Example**:
```java
// Bad Example - Comment explaining unclear code
int age; // This stores the user's age

// Good Example - Clear code without the need for a comment
int userAge;
```

### 2. Explain Yourself in Code
Whenever possible, the code itself should explain its purpose. Well-named variables, methods, and classes eliminate the need for comments. If you find yourself writing a comment to explain what your code is doing, consider refactoring the code to make it clearer instead.

**Example**:
```java
// Bad Example - Comment used to explain code
if ((employee.flags & HOURLY_FLAG) && (employee.age > 65)) {
    // check if the employee is eligible for full benefits
}

// Good Example - Clearer code, no comment needed
if (employee.isEligibleForFullBenefits()) {
    // code to handle benefits
}
```

### 3. Good Comments
While the goal is to avoid comments, there are cases where comments can be helpful or necessary. Good comments add useful context, explain why something was done (rather than what is being done), or provide documentation that cannot be easily expressed in the code.

**Examples of Good Comments**:
- **Legal Comments**: Required by law or licensing, such as copyright notices.
- **Explanation of Intent**: Explaining why a particular approach was taken when it’s not immediately obvious.
- **Clarifying Complex Code**: For exceptionally complex or unusual logic, a comment may be helpful to explain the intent.
  
**Example**:
```java
// Good Example - Explaining a non-obvious decision
// We use a custom sorting algorithm here because the default sorting is too slow for our dataset size.
customSort(data);
```

### 4. Bad Comments
Most comments fall into the category of "bad comments"—comments that are redundant, outdated, or provide no real value. These types of comments clutter the code and make maintenance more difficult.

- **Redundant Comments**: Comments that simply restate what the code is already doing.
- **Misleading Comments**: Outdated or incorrect comments that mislead developers.
- **Noise Comments**: Comments that provide no useful information, such as stating the obvious.

**Example**:
```java
// Bad Example - Redundant comment
int userAge; // This is the user's age

// Bad Example - Misleading comment
// Calculate the discount (this comment is outdated and incorrect)
applyTax(amount);
```

### 5. Mumbling Comments
Vague or unclear comments—referred to as "mumbling comments"—do not add value and should be avoided. These comments fail to properly explain the logic or intent, leaving future developers confused.

**Example**:
```java
// Bad Example - Vague comment
// Handles stuff
processData();
```

### 6. Commented-Out Code
Commented-out code should be removed from the codebase. It creates unnecessary clutter and can lead to confusion about whether it is still needed. Modern version control systems (like Git) make it easy to retrieve old code if needed, so there is no reason to keep it in the source files.

**Example**:
```java
// Bad Example - Commented-out code
// int result = calculateResult(value);

// Good Example - Remove unused code
int result = calculateResult(value);
```

### 7. Don’t Use a Comment When You Can Use a Function or Variable
Instead of explaining code with a comment, consider refactoring it into a self-explanatory function or variable. This improves readability and removes the need for a comment entirely.

**Example**:
```java
// Bad Example - Comment used to explain complex logic
if (smodule.getDependSubsystems().contains(subSysMod.getSubSystem())) {
    // does the module depend on the subsystem?
}

// Good Example - Refactor into a descriptive method
if (moduleDependsOnSubsystem(smodule, subSysMod)) {
    // code
}

private boolean moduleDependsOnSubsystem(Module smodule, SubSystem subSysMod) {
    return smodule.getDependSubsystems().contains(subSysMod.getSubSystem());
}
```

### 8. Use “TODO” Comments Sparingly
“TODO” comments can be useful for tracking incomplete work, but they should not be overused. It’s easy to forget or ignore them, leading to unaddressed issues. If you use them, make sure they are addressed in a timely manner.

**Example**:
```java
// Good Example - TODO comment to mark future work
// TODO: Refactor this method to handle edge cases.
processData();
```



## Chapter 5: Formatting
### Introduction
The way code is formatted significantly affects its readability and maintainability. Good formatting practices ensure that code is easy to understand and navigate, making it more accessible for other developers and your future self. Consistent formatting allows the code to "flow" naturally and reduces cognitive load when reading it.

### 1. The Purpose of Formatting
Formatting is primarily about communication. Code is written for people to read, so its structure should be optimized for clarity and ease of navigation. Well-formatted code makes it easier to spot errors, understand logic, and collaborate with others.

**Example**:
```java
// Bad Example - No consistent structure or clarity
public class Order{private String id;public void processOrder(Order order){if(order!=null){System.out.println("Processing order");}}}

// Good Example - Proper formatting for readability
public class Order {
    private String id;

    public void processOrder(Order order) {
        if (order != null) {
            System.out.println("Processing order");
        }
    }
}
```

### 2. Vertical Formatting
Vertical formatting focuses on the placement of code elements from top to bottom. Proper vertical formatting helps the reader understand the relationships between different parts of the code and ensures a logical flow.

#### The Newspaper Metaphor
Just like a newspaper article, code should be structured so that the most important information (high-level functions) appears at the top, and details (low-level implementation) follow. This allows the reader to grasp the overall purpose before diving into the specifics.

**Example**:
```java
// Bad Example - Low-level details appear before high-level logic
private void validateUser(User user) { /* validation logic */ }

public void processOrder(Order order) {
    validateUser(order.getUser());
    // further logic
}

// Good Example - High-level functions appear first
public void processOrder(Order order) {
    validateUser(order.getUser());
    // further logic
}

private void validateUser(User user) { /* validation logic */ }
```

### 3. Vertical Openness Between Concepts
Use blank lines to separate different concepts or blocks of logic. This helps visually distinguish between unrelated sections of code, making it easier to follow.

**Example**:
```java
// Bad Example - No separation between concepts
public class PaymentProcessor {
    public void processPayment(double amount){logPayment(amount);deductBalance(amount);sendConfirmation();}
    private void logPayment(double amount){System.out.println("Logging payment of " + amount);}
    private void deductBalance(double amount){System.out.println("Deducting balance of " + amount);}
    private void sendConfirmation(){System.out.println("Sending confirmation email.");}
}

// Good Example - Blank lines to separate different concerns
public class PaymentProcessor {
    public void processPayment(double amount) {
        logPayment(amount);
        deductBalance(amount);
        sendConfirmation();
    }

    private void logPayment(double amount) {
        System.out.println("Logging payment of " + amount);
    }

    private void deductBalance(double amount) {
        System.out.println("Deducting balance of " + amount);
    }

    private void sendConfirmation() {
        System.out.println("Sending confirmation email.");
    }
}
```

### 4. Vertical Density
While vertical openness helps separate different concepts, vertical density refers to keeping related lines of code close together. Lines that are closely related should appear without unnecessary spaces between them.

**Example**:
```java
// Bad Example - Unnecessary vertical spacing within a block of related code
public class UserService {
    
    public void createUser(User user) {
        
        validate(user);
        
        saveToDatabase(user);
        
        sendWelcomeEmail(user);
    }
}

// Good Example - Related lines are grouped together
public class UserService {
    public void createUser(User user) {
        validate(user);
        saveToDatabase(user);
        sendWelcomeEmail(user);
    }
}
```

### 5. Vertical Distance
Functions that are closely related should appear near each other in the code. Keeping related functions close together reduces the need to scroll through files and improves the readability of the code.

**Example**:
```java
// Bad Example - Closely related methods are placed far apart
public class Cart {
    public void checkout() {
        double total = calculateTotal();
    }

    // unrelated methods here...

    private double calculateTotal() {
        return 100.0;
    }
}

// Good Example - Related methods are kept together
public class Cart {
    public void checkout() {
        double total = calculateTotal();
    }

    private double calculateTotal() {
        return 100.0;
    }
}
```

### 6. Horizontal Formatting
Horizontal formatting deals with the placement of code elements across the width of the page. Long lines of code are hard to read and should be broken up. Additionally, the horizontal spacing between elements should reflect their logical relationship.

**Example**:
```java
// Bad Example - Long line and lack of horizontal spacing
public void processPayment(Payment payment){payment.charge();payment.sendReceipt();logTransaction(payment);}

// Good Example - Proper horizontal spacing and line breaking
public void processPayment(Payment payment) {
    payment.charge();
    payment.sendReceipt();
    logTransaction(payment);
}
```

### 7. Indentation
Indentation is used to show the structure and hierarchy of code blocks. Proper indentation ensures that nested logic (such as loops, conditionals, or method calls) is easily distinguishable from other parts of the code.

**Example**:
```java
// Bad Example - Incorrect indentation
public class PaymentService{
public void process(){double total = calculateTotal();if(total>0){System.out.println("Processing payment.");}}}

// Good Example - Correct indentation
public class PaymentService {
    public void process() {
        double total = calculateTotal();
        if (total > 0) {
            System.out.println("Processing payment.");
        }
    }
}
```

### 8. Horizontal Alignment
While aligning code vertically (like aligning assignment operators) can sometimes improve readability, it should be used sparingly as it can lead to inconsistent and hard-to-maintain code.

**Example**:
```java
// Bad Example - Excessive alignment
int    firstVar      = 10;
double secondVariable = 20.0;
float  thirdVar     = 30.0f;

// Good Example - Avoiding unnecessary alignment
int firstVar = 10;
double secondVariable = 20.0;
float thirdVar = 30.0f;
```

### 9. Breaking Indentation Rules
Avoid breaking indentation rules, such as collapsing multiple statements on a single line. Proper indentation makes the code easier to read and maintain. Combining statements on a single line can lead to confusion.

**Example**:
```java
// Bad Example - Multiple statements on one line
if (total > 0) {processPayment();}

// Good Example - Each statement on its own line
if (total > 0) {
    processPayment();
}
```

### 10. Team Rules
Consistency is key when it comes to formatting. Your team should agree on a set of formatting rules and apply them uniformly across the codebase. Adopting automated tools like linters or code formatters can help enforce these rules and ensure consistency.



## Chapter 6: Objects and Data Structures
### Introduction
Objects and data structures represent two different approaches to organizing data and behavior in a system. Objects encapsulate data and expose behavior, while data structures expose data but have little or no behavior. Understanding the difference between these two concepts and using them appropriately is essential for writing clean, maintainable code.

### 1. Data Abstraction
Objects should hide their data and expose behavior through methods. This encapsulation allows the object to control how its data is accessed and modified, maintaining consistency and reducing dependencies. Data structures, on the other hand, expose their data without behavior, which can lead to tight coupling and less flexibility.

**Example**:
```java
// Bad Example - Exposing data directly
public class Point {
    public double x;
    public double y;
}

// Good Example - Encapsulating data behind methods
public class Point {
    private double x;
    private double y;

    public double getX() { return x; }
    public double getY() { return y; }
    public void setCartesian(double x, double y) {
        this.x = x;
        this.y = y;
    }
}
```

### 2. Data/Object Anti-Symmetry
Objects and data structures serve opposite purposes. Objects encapsulate data and expose behavior, while data structures expose data and provide little to no behavior. Mixing the two concepts can lead to confusion and reduce the benefits of encapsulation. Using objects means focusing on behavior, while using data structures means focusing on data access.

**Example**:
```java
// Bad Example - Mixing data and behavior
public class Square {
    public Point topLeft;
    public double side;

    public double area() {
        return side * side;
    }
}

// Good Example - Separating behavior from data
public class Geometry {
    public double area(Square s) {
        return s.side * s.side;
    }
}
```

### 3. The Law of Demeter
The Law of Demeter (also known as the **Principle of Least Knowledge**) advises that a method should only interact with:

- The current object.
- Objects passed in as parameters.
- Objects that are directly owned by the current object (instance variables).

This principle helps to reduce coupling between classes and makes the code more maintainable. When following this law, methods should not navigate through object chains to manipulate deep internal structures.

**Example**:
```java
// Bad Example - Violating the Law of Demeter
public void processOrder(Order order) {
    order.getCustomer().getAddress().getCity(); // too much navigation
}

// Good Example - Following the Law of Demeter
public void processOrder(Order order) {
    Customer customer = order.getCustomer();
    String city = customer.getCity(); // direct interaction
}
```
*Explanation*: Instead of chaining through several objects to access the city, the responsibility is delegated to the `Customer` class to provide this information directly. This reduces the coupling between `Order` and `Address`.

### 4. Train Wrecks
Train wrecks refer to the practice of chaining multiple method calls together. This results in tightly coupled code that is difficult to maintain, test, or modify. Train wrecks often arise when an object relies on deeply nested objects instead of delegating responsibility appropriately.

To avoid train wrecks, break long method chains into smaller, more focused methods that delegate responsibility.

**Example**:
```java
// Bad Example - Train wreck with long method chaining
public void displayCustomerInfo(Order order) {
    System.out.println(order.getCustomer().getAddress().getPostalCode());
}

// Good Example - Avoiding train wrecks by delegating responsibility
public void displayCustomerInfo(Order order) {
    System.out.println(order.getCustomerPostalCode());
}

public String getCustomerPostalCode(Order order) {
    return order.getCustomer().getPostalCode(); // simpler and more direct
}
```
*Explanation*: Instead of chaining multiple method calls in one line, we introduce a method (`getCustomerPostalCode`) that hides the complexity of navigating through the object hierarchy. This makes the code more readable and easier to maintain.

### 5. Data Transfer Objects (DTOs)
Data Transfer Objects (DTOs) are simple data structures used to transfer data between systems or layers in an application. They contain no behavior and are purely used for encapsulating data. DTOs can simplify the process of passing multiple pieces of data between different parts of a system.

**Example**:
```java
// Example - Data Transfer Object
public class Address {
    private String street;
    private String city;
    private String state;
    private String zip;

    public Address(String street, String city, String state, String zip) {
        this.street = street;
        this.city = city;
        this.state = state;
        this.zip = zip;
    }

    // Getters and setters for each field
    public String getStreet() { return street; }
    public String getCity() { return city; }
    public String getState() { return state; }
    public String getZip() { return zip; }
}
```

### 6. Active Record Pattern
The Active Record pattern is a design pattern where data structures (similar to DTOs) are combined with behavior that interacts with a database. This pattern is often used for objects that map directly to database tables and provide CRUD (Create, Read, Update, Delete) methods. While this pattern simplifies data access, it can blur the line between data structures and behavior, making it harder to maintain clean separation.

**Example**:
```java
// Example - Active Record pattern
public class User extends ActiveRecord {
    public String name;
    public String email;

    public void save() {
        // code to save user to the database
    }

    public static User find(int id) {
        // code to find user by id
    }
}
```

### 7. Objects Hide Data, Data Structures Expose It
Objects should be designed to hide their internal data and expose only the necessary behavior. This encapsulation allows objects to maintain control over their internal state. Data structures, on the other hand, are designed to expose their data without behavior, making them more suitable for scenarios where direct data manipulation is needed.

**Example**:
```java
// Bad Example - Exposing internal state through getters
public class Rectangle {
    public double length;
    public double width;
}

// Good Example - Encapsulating internal state and providing behavior
public class Rectangle {
    private double length;
    private double width;

    public double calculateArea() {
        return length * width;
    }
}
```

### 8. Prefer Objects for Behavior, Data Structures for Raw Data
Use objects when you need to hide internal state and provide specific behavior, such as calculations or operations on that data. Use data structures when you need to move or store raw data, and no behavior is needed. Mixing these approaches can lead to unclear and unmaintainable code.

**Example**:
```java
// Bad Example - Object with unnecessary exposed data
public class Product {
    public String name;
    public double price;

    public void applyDiscount(double discount) {
        this.price -= discount;
    }
}

// Good Example - Data structure for raw data, separate service for behavior
public class Product {
    public String name;
    public double price;
}

public class PricingService {
    public void applyDiscount(Product product, double discount) {
        product.price -= discount;
    }
}
```


## Chapter 7: Error Handling

### Introduction
Error handling is an essential part of writing clean, maintainable, and robust software. Proper error handling ensures that your code behaves correctly in the face of unexpected situations, improving the quality and reliability of your system. This chapter focuses on using exceptions, avoiding return codes, and following best practices for managing errors to keep your code clean and maintainable.

### 1. Use Exceptions Rather Than Return Codes
Using exceptions instead of return codes makes error handling cleaner and more efficient. Returning error codes requires the caller to check for errors after every operation, cluttering the main logic. Exceptions separate error-handling logic from normal flow, making the code more readable and maintainable.

**Example**:
```java
// Bad Example - Using return codes for error handling
public int deleteFile(File file) {
    if (!file.exists()) {
        return -1; // error code
    }
    // code to delete file
    return 0; // success
}

// Good Example - Using exceptions for error handling
public void deleteFile(File file) throws FileNotFoundException {
    if (!file.exists()) {
        throw new FileNotFoundException();
    }
    // code to delete file
}
```

### 2. Write Your `try-catch-finally` Statements First
When dealing with potentially failing operations, it’s a good practice to write the `try-catch-finally` block first. This ensures that error-handling logic is considered from the start and that the code maintains a consistent state in case of exceptions.

**Example**:
```java
// Good Example - Writing error handling first
try {
    FileInputStream stream = new FileInputStream("file.txt");
    // process the file
} catch (FileNotFoundException e) {
    // handle file not found
} finally {
    // close the file stream
}
```

### 3. Use Unchecked Exceptions
Unchecked exceptions (those not declared in a method’s `throws` clause) simplify the code by reducing the need for explicit handling throughout the call chain. Checked exceptions can introduce unnecessary complexity, forcing every method to declare or handle them.

**Example**:
```java
// Bad Example - Using checked exceptions excessively
public void process() throws FileNotFoundException, IOException {
    // code
}

// Good Example - Using unchecked exceptions
public void process() {
    try {
        // code
    } catch (IOException e) {
        throw new RuntimeException(e); // wrapping in an unchecked exception
    }
}
```

### 4. Provide Context with Exceptions
When throwing exceptions, always include meaningful context in the exception message. This makes debugging easier, as it provides enough information to trace the root cause of the problem.

**Example**:
```java
// Bad Example - Throwing a generic exception without context
throw new RuntimeException();

// Good Example - Providing context in the exception
throw new RuntimeException("Failed to process order: Order ID " + orderId);
```

### 5. Define Exception Classes in Terms of the Caller’s Needs
Custom exceptions should be defined based on how they are handled by the caller. This helps to simplify the error-handling logic and ensures that the caller can manage the exception appropriately.

**Example**:
```java
// Bad Example - Handling specific exceptions separately
try {
    port.open();
} catch (DeviceResponseException e) {
    reportError(e);
} catch (PortLockedException e) {
    reportError(e);
} catch (PortFailureException e) {
    reportError(e);
}

// Good Example - Wrapping exceptions in a common type
try {
    port.open();
} catch (PortDeviceFailure e) {
    reportError(e);
}
```

### 6. Define the Normal Flow
Error handling should not obscure the normal flow of the program. The special-case pattern or default objects can be used to simplify the code and make the logic cleaner, eliminating the need for error-handling in some cases.

**Example**:
```java
// Bad Example - Using exceptions for special cases
try {
    MealExpenses expenses = expenseReportDAO.getMeals(employee.getID());
    total += expenses.getTotal();
} catch (MealExpensesNotFound e) {
    total += getMealPerDiem();
}

// Good Example - Using a special-case object
MealExpenses expenses = expenseReportDAO.getMeals(employee.getID());
total += expenses.getTotal();
```

### 7. Don’t Return `null`
Returning `null` can lead to errors and excessive `null` checks throughout your code. Instead, use special-case objects or throw exceptions to handle invalid conditions.

**Example**:
```java
// Bad Example - Returning null
public Item findItem(String id) {
    return null; // Item not found
}

// Good Example - Using a special-case object
public Item findItem(String id) {
    return Item.NOT_FOUND; // Special case object
}
```

### 8. Don’t Pass `null`
Avoid passing `null` as a parameter. Code that expects non-null values is cleaner and safer. If a method requires a valid object, it should validate or throw an exception when passed `null`.

**Example**:
```java
// Bad Example - Passing null as a parameter
calculator.xProjection(null, new Point(12, 13));

// Good Example - Validating input parameters
public double xProjection(Point p1, Point p2) {
    if (p1 == null || p2 == null) {
        throw new IllegalArgumentException("Points cannot be null");
    }
    return (p2.x - p1.x) * 1.5;
}
```


## Chapter 8: Boundaries
### Introduction
Working with boundaries is essential in software development, as we often rely on third-party libraries, APIs, or other external systems. Boundaries between your code and external code (such as libraries or frameworks) need to be managed carefully to prevent tight coupling and ensure maintainability. This chapter discusses best practices for working with external code, managing boundaries, and keeping your system flexible.

### 1. Using Third-Party Code
When integrating third-party libraries or APIs, it's crucial to encapsulate them within your own code. This minimizes the dependency on external systems and ensures that if the library changes or becomes obsolete, you can easily modify your code without large-scale rewrites.

**Example**:
```java
// Bad Example - Exposing third-party code directly
Map<String, Sensor> sensors = new HashMap<>();
Sensor sensor = sensors.get(sensorId);

// Good Example - Encapsulating third-party code
public class Sensors {
    private Map<String, Sensor> sensors = new HashMap<>();

    public Sensor getById(String id) {
        return sensors.get(id);
    }
}
```

### 2. Exploring and Learning Boundaries
When working with unfamiliar third-party code, it's essential to explore and understand its boundaries before fully integrating it into your system. A good practice is to write **learning tests**—small tests that help you understand how a third-party library behaves. These tests don't necessarily test your application but give you insights into how the library works.

**Example**:
```java
// Good Example - Writing a learning test for a logging library
@Test
public void testLogCreate() {
    Logger logger = Logger.getLogger("MyLogger");
    logger.info("Logging message");
}
```

### 3. Learning Tests Are Better Than Free
Learning tests help you understand external systems or libraries without directly modifying your application. By writing these tests, you not only explore how the external code behaves, but you also create a test suite that can help ensure that future changes in the external library do not break your system.

**Benefits of Learning Tests**:
- **Immediate feedback** on how the library behaves.
- **Helps with future upgrades** to the external library.

### 4. Using Code That Does Not Yet Exist
In many cases, you may need to integrate with code or systems that are not yet fully developed. To avoid being blocked by these dependencies, you can define your own interfaces or wrappers. Once the external code becomes available, you can easily adapt your system to integrate with it.

**Example**:
```java
// Define your own interface to abstract external dependency
public interface Transmitter {
    void transmit(Frequency frequency, DataStream dataStream);
}

// Later, adapt to the external system when it's ready
public class TransmitterAdapter implements Transmitter {
    private final ExternalTransmitterAPI externalTransmitter;

    public TransmitterAdapter(ExternalTransmitterAPI api) {
        this.externalTransmitter = api;
    }

    @Override
    public void transmit(Frequency frequency, DataStream dataStream) {
        externalTransmitter.sendSignal(frequency, dataStream.toAnalog());
    }
}
```

### 5. Clean Boundaries
It's important to maintain clean boundaries between your code and third-party libraries. By encapsulating the interaction with external systems, you protect your application from changes in the external code and reduce the complexity of your system. Encapsulation ensures that your application’s internal logic doesn’t depend directly on the implementation details of the external code.

**Example**:
```java
// Bad Example - Scattering third-party library calls across the codebase
public class SystemMonitor {
    public void checkSensors() {
        Map<String, Sensor> sensors = new HashMap<>();
        Sensor sensor = sensors.get("123");
        // process sensor data
    }
}

// Good Example - Encapsulating third-party interactions
public class Sensors {
    private Map<String, Sensor> sensors = new HashMap<>();

    public Sensor getById(String id) {
        return sensors.get(id);
    }
}

public class SystemMonitor {
    private Sensors sensors;

    public void checkSensors() {
        Sensor sensor = sensors.getById("123");
        // process sensor data
    }
}
```

### 6. Boundaries Should Be Tested
Whenever you interact with external systems, it's essential to test the boundaries between your code and external libraries or APIs. Testing at these boundaries helps ensure that your code behaves correctly even when the external code does not.

Writing boundary tests ensures that you understand how your system interacts with external code and that it will fail gracefully if the external system behaves unexpectedly.

**Example**:
```java
@Test
public void testExternalLibraryIntegration() {
    try {
        externalService.connect();
    } catch (ServiceUnavailableException e) {
        // handle exception gracefully in the application
    }
}
```

### 7. Prefer Adapters for External Dependencies
Use adapter patterns to wrap third-party libraries or external systems. Adapters provide a clean interface to the rest of your application, allowing you to replace the external dependency without affecting the internal logic of your system. This also helps to ensure clean separation of concerns.

**Example**:
```java
// Adapter to wrap external payment service
public class PaymentServiceAdapter {
    private ExternalPaymentService externalService;

    public PaymentServiceAdapter(ExternalPaymentService service) {
        this.externalService = service;
    }

    public void processPayment(Order order) {
        externalService.makePayment(order.getTotalAmount());
    }
}
```

## Chapter 9: Unit Tests

### Introduction
Unit testing is essential to writing clean, reliable, and maintainable code. By writing automated tests that verify individual units of code, you can ensure that your code behaves as expected. Well-structured unit tests provide quick feedback on potential errors, help maintain code quality during refactoring, and act as a safety net against bugs. This chapter focuses on the importance of unit testing, the characteristics of good tests, and best practices for writing clean tests.

### 1. The Three Laws of TDD (Test-Driven Development)
Test-Driven Development (TDD) encourages writing tests before writing the actual code. This approach helps ensure that every piece of code has a clear purpose and that it is testable.

The three laws of TDD are:
1. **You may not write production code until you have written a failing unit test**.
2. **You may not write more of a unit test than is sufficient to fail** (compilation failures count as failures).
3. **You may not write more production code than is sufficient to pass the failing test**.

Following TDD helps developers focus on writing testable and clean code.

**Example**:
```java
// Test first (fail)
@Test
public void testAddTwoNumbers() {
    Calculator calculator = new Calculator();
    assertEquals(5, calculator.add(2, 3));
}

// Write just enough code to make the test pass
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
}
```

### 2. Keep Tests Clean
Just like production code, tests should be clean and maintainable. Tests should be easy to read and understand because they act as documentation for the system. If your tests are hard to maintain, they become a burden rather than a safety net. Follow clean code principles in your tests as well.

**Key aspects of clean tests**:
- **Readable**: Tests should clearly show the intent.
- **Maintainable**: Avoid duplication and ensure tests are easy to update.
- **Focused**: Each test should test one concept or behavior.

**Example**:
```java
// Bad Example - Unclear test
@Test
public void testSomething() {
    // lots of setup code
    assertEquals(true, something.doStuff());
}

// Good Example - Clear and focused test
@Test
public void shouldReturnTrueWhenConditionMet() {
    Condition condition = new Condition(true);
    assertTrue(condition.isMet());
}
```

### 3. Tests Should Be Fast
Unit tests should be fast to run. When tests are slow, developers may skip running them regularly, reducing their effectiveness. Fast tests provide immediate feedback, allowing you to catch errors early and often. Make sure your tests run quickly so that you can execute them frequently without hesitation.

**Example**:
```java
// Bad Example - Slow test involving database connection
@Test
public void testDatabaseInteraction() {
    Database db = new Database();
    db.connect();
    db.save(new Record("Test"));
    db.disconnect();
}

// Good Example - Use a mock object to speed up the test
@Test
public void testDatabaseInteractionWithMock() {
    Database db = mock(Database.class);
    when(db.save(any(Record.class))).thenReturn(true);
    assertTrue(db.save(new Record("Test")));
}
```

### 4. Tests Should Be Independent
Each test should be independent of other tests. A test should be able to run in isolation and still pass, regardless of the order in which tests are executed. Dependencies between tests can lead to false positives or failures that are difficult to track down.

**Example**:
```java
// Bad Example - Test depends on previous test state
@Test
public void testAddUser() {
    UserManager manager = new UserManager();
    manager.addUser("user1");
    assertEquals(1, manager.getUserCount());
}

@Test
public void testAddAnotherUser() {
    UserManager manager = new UserManager(); // This should not rely on previous test's state
    manager.addUser("user2");
    assertEquals(2, manager.getUserCount()); // Fails if testAddUser hasn't run
}

// Good Example - Independent tests
@Test
public void testAddUser() {
    UserManager manager = new UserManager();
    manager.addUser("user1");
    assertEquals(1, manager.getUserCount());
}

@Test
public void testAddAnotherUserIndependently() {
    UserManager manager = new UserManager();
    manager.addUser("user2");
    assertEquals(1, manager.getUserCount()); // Works independently
}
```

### 5. Tests Should Be Repeatable
Tests should produce the same result every time they are run, regardless of the environment or conditions. Flaky tests—tests that sometimes pass and sometimes fail—undermine the trust in the test suite. Ensure that your tests run consistently by avoiding dependencies on external systems, like databases or network services, unless they are properly mocked.

**Example**:
```java
// Bad Example - Test depends on an external resource (network)
@Test
public void testNetworkConnection() {
    NetworkConnection conn = new NetworkConnection();
    assertTrue(conn.connect());
}

// Good Example - Test is repeatable by mocking external dependencies
@Test
public void testNetworkConnectionWithMock() {
    NetworkConnection conn = mock(NetworkConnection.class);
    when(conn.connect()).thenReturn(true);
    assertTrue(conn.connect());
}
```

### 6. Use Descriptive Names
The names of your tests should describe the behavior being tested. Descriptive names make it easier to understand what is being tested without having to read the code inside the test.

**Example**:
```java
// Bad Example - Vague test name
@Test
public void testSomething() {
    // test logic
}

// Good Example - Descriptive test name
@Test
public void shouldReturnTrueWhenConditionIsMet() {
    // test logic
}
```

### 7. Avoid Logic in Tests
Tests should be straightforward and avoid logic such as loops or conditionals. If your tests contain logic, they may themselves be prone to errors, which can undermine the reliability of the test suite. The goal is to write simple, declarative tests that verify the behavior of your code.

**Example**:
```java
// Bad Example - Test contains logic
@Test
public void testWithLogic() {
    for (int i = 0; i < 5; i++) {
        assertTrue(doSomething(i));
    }
}

// Good Example - Test is simple and declarative
@Test
public void shouldHandleSpecificCase() {
    assertTrue(doSomething(1));
    assertTrue(doSomething(2));
    assertTrue(doSomething(3));
}
```

### 8. Test Edge Cases
Good unit tests cover edge cases and unusual situations. This ensures that your code is robust and behaves correctly even in unexpected scenarios. Always consider boundary conditions, null inputs, and invalid states when writing tests.

**Example**:
```java
// Good Example - Test for edge cases
@Test
public void shouldHandleEmptyList() {
    List<String> emptyList = new ArrayList<>();
    assertEquals(0, emptyList.size());
}

@Test(expected = IllegalArgumentException.class)
public void shouldThrowExceptionForInvalidInput() {
    Validator.validate(null); // Test for invalid input
}
```

## Chapter 10: Classes

### Introduction
Classes are fundamental building blocks in object-oriented programming. A well-designed class should be small, focused, and have a clear responsibility. This chapter emphasizes the importance of keeping classes simple, cohesive, and properly structured to ensure that they are easy to maintain, understand, and extend.

### 1. Classes Should Be Small
Small classes are easier to understand and maintain. A class should have a clear, single responsibility, and its size should be driven by the need to fulfill this responsibility—nothing more. If a class becomes too large, it often indicates that it has too many responsibilities and should be split into smaller classes.

**Example**:
```java
// Bad Example - Large class with multiple responsibilities
public class UserManager {
    public void addUser(User user) { /* code */ }
    public void removeUser(User user) { /* code */ }
    public void sendNotification(User user, String message) { /* code */ }
    public void calculateUserStats(User user) { /* code */ }
}

// Good Example - Smaller classes with single responsibilities
public class UserManager {
    public void addUser(User user) { /* code */ }
    public void removeUser(User user) { /* code */ }
}

public class NotificationService {
    public void sendNotification(User user, String message) { /* code */ }
}

public class UserStatistics {
    public void calculateStats(User user) { /* code */ }
}
```

### 2. Single Responsibility Principle (SRP)
A class should have only one reason to change, meaning it should only have one responsibility. By adhering to the Single Responsibility Principle (SRP), you ensure that each class has a focused purpose, making it easier to manage and modify without affecting unrelated functionality.

**Example**:
```java
// Bad Example - Violating SRP by managing users and sending notifications
public class UserManager {
    public void addUser(User user) { /* code */ }
    public void sendNotification(User user, String message) { /* code */ }
}

// Good Example - Following SRP by separating concerns
public class UserManager {
    public void addUser(User user) { /* code */ }
}

public class NotificationService {
    public void sendNotification(User user, String message) { /* code */ }
}
```

### 3. Cohesion
A class should be cohesive, meaning that all its methods and variables should work together to fulfill a single purpose. High cohesion within a class ensures that it is focused and all the pieces of the class are related to one another.

**Example**:
```java
// Bad Example - Low cohesion, unrelated methods in the same class
public class ReportManager {
    public void generateReport() { /* code */ }
    public void sendEmail() { /* code */ }
    public void logReportDetails() { /* code */ }
}

// Good Example - High cohesion, methods are focused on report generation
public class ReportManager {
    public void generateReport() { /* code */ }
    public void logReportDetails() { /* code */ }
}

public class EmailService {
    public void sendEmail(String message) { /* code */ }
}
```

### 4. Encapsulation
Encapsulation refers to hiding the internal details of a class and exposing only what is necessary. This protects the internal state of the object from being corrupted by external code. Well-encapsulated classes make it easier to change the internal implementation without affecting the code that uses the class.

**Example**:
```java
// Bad Example - Exposing internal state
public class User {
    public String name;
    public String email;
}

// Good Example - Encapsulating internal state
public class User {
    private String name;
    private String email;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }
}
```

### 5. Open/Closed Principle (OCP)
Classes should be **open for extension** but **closed for modification**. This means you should be able to extend a class’s behavior without modifying its existing code. This principle helps prevent breaking existing functionality when adding new features.

**Example**:
```java
// Bad Example - Modifying the class for new functionality
public class PaymentService {
    public void processPayment(String paymentType) {
        if (paymentType.equals("CreditCard")) {
            // process credit card
        } else if (paymentType.equals("PayPal")) {
            // process PayPal
        }
    }
}

// Good Example - Using inheritance to extend functionality
public abstract class PaymentService {
    public abstract void processPayment();
}

public class CreditCardPayment extends PaymentService {
    @Override
    public void processPayment() {
        // process credit card
    }
}

public class PayPalPayment extends PaymentService {
    @Override
    public void processPayment() {
        // process PayPal
    }
}
```

### 6. Dependency Inversion Principle (DIP)
High-level classes should not depend on low-level classes. Both should depend on abstractions. This principle encourages decoupling of code, making it easier to test and maintain.

**Example**:
```java
// Bad Example - High-level module depends on a low-level class
public class PaymentProcessor {
    private PayPalService payPalService;

    public PaymentProcessor() {
        this.payPalService = new PayPalService();
    }

    public void process() {
        payPalService.makePayment();
    }
}

// Good Example - Both high- and low-level modules depend on an abstraction
public interface PaymentService {
    void makePayment();
}

public class PayPalService implements PaymentService {
    @Override
    public void makePayment() {
        // process PayPal payment
    }
}

public class PaymentProcessor {
    private PaymentService paymentService;

    public PaymentProcessor(PaymentService paymentService) {
        this.paymentService = paymentService;
    }

    public void process() {
        paymentService.makePayment();
    }
}
```

### 7. Prefer Composition Over Inheritance
While inheritance can be useful, it often leads to tightly coupled code that is hard to maintain. In many cases, composition (where one class uses another class) is a better approach because it promotes flexibility and decouples the implementation.

**Example**:
```java
// Bad Example - Using inheritance unnecessarily
public class ElectricCar extends Car {
    // inherits properties and methods from Car
}

// Good Example - Using composition instead
public class Car {
    private Engine engine;

    public Car(Engine engine) {
        this.engine = engine;
    }

    public void start() {
        engine.start();
    }
}
```

### 8. Avoid God Classes
A "God Class" is a class that knows too much or does too much. It tends to centralize too many responsibilities, making it hard to manage, understand, and maintain. Avoid such classes by distributing responsibilities across smaller, more focused classes.

**Example**:
```java
// Bad Example - God Class with too many responsibilities
public class ApplicationManager {
    public void startApplication() { /* code */ }
    public void stopApplication() { /* code */ }
    public void manageUserSessions() { /* code */ }
    public void manageFiles() { /* code */ }
}

// Good Example - Breaking responsibilities into smaller classes
public class ApplicationManager {
    public void startApplication() { /* code */ }
    public void stopApplication() { /* code */ }
}

public class SessionManager {
    public void manageUserSessions() { /* code */ }
}

public class FileManager {
    public void manageFiles() { /* code */ }
}
```

## Chapter 11: Systems
### Introduction
Building and maintaining a system is different from writing small programs or components. Systems are composed of many interacting parts, and the way these parts communicate and cooperate affects the system's performance, maintainability, and reliability. A well-designed system should be flexible, maintainable, and easy to understand. This chapter focuses on creating systems that are both robust and maintainable by keeping their complexity manageable.

### 1. Separate Constructing a System from Using It
A key practice in building systems is separating the creation of objects and their usage. The construction of a system should be isolated from the logic that operates within it. This allows you to change how objects are constructed without affecting the behavior of the system.

**Example**:
```java
// Bad Example - Direct object creation inside the logic
public class OrderProcessor {
    public void processOrder() {
        Order order = new Order();
        // process order
    }
}

// Good Example - Separate construction from use
public class OrderProcessor {
    private final OrderFactory orderFactory;

    public OrderProcessor(OrderFactory orderFactory) {
        this.orderFactory = orderFactory;
    }

    public void processOrder() {
        Order order = orderFactory.createOrder();
        // process order
    }
}
```

By isolating the creation logic (in this case, through `OrderFactory`), you make it easier to modify or swap out how objects are created, for example, when moving to a different order system.

### 2. Dependency Injection
Dependency Injection (DI) is a design pattern that allows you to decouple the construction of a system’s components from the system's logic. Instead of creating objects directly within a class, dependencies are "injected" into the class, usually through the constructor, method, or field. DI improves flexibility, testability, and maintainability.

**Example**:
```java
// Bad Example - No Dependency Injection
public class UserService {
    private EmailService emailService = new EmailService();

    public void notifyUser(User user) {
        emailService.sendEmail(user.getEmail());
    }
}

// Good Example - Using Dependency Injection
public class UserService {
    private EmailService emailService;

    public UserService(EmailService emailService) {
        this.emailService = emailService;
    }

    public void notifyUser(User user) {
        emailService.sendEmail(user.getEmail());
    }
}
```

With DI, you can easily swap out `EmailService` for a different implementation (e.g., a mock for testing), which makes the system more flexible.

### 3. Use Factories to Manage Object Creation
Factories are a powerful way to manage object creation, especially when creating complex objects that involve multiple dependencies. By centralizing object creation in factories, you make it easier to control how objects are created and manage changes in the creation process.

**Example**:
```java
// Factory for creating complex objects
public class OrderFactory {
    public Order createOrder() {
        PaymentService paymentService = new PaymentService();
        InventoryService inventoryService = new InventoryService();
        return new Order(paymentService, inventoryService);
    }
}
```

By using a factory, the details of how `Order` objects are constructed are encapsulated, and if the object’s dependencies change in the future, only the factory needs to be updated, not the entire system.

### 4. Build Systems Using Dependency Injection Frameworks
Many modern systems rely on Dependency Injection frameworks (such as Spring or Guice) to manage dependencies. These frameworks allow you to define how objects are constructed and injected automatically, making the system easier to configure and more maintainable over time.

**Example with Spring Framework**:
```java
// Defining a bean with Spring framework
@Service
public class UserService {
    private final EmailService emailService;

    @Autowired
    public UserService(EmailService emailService) {
        this.emailService = emailService;
    }

    public void notifyUser(User user) {
        emailService.sendEmail(user.getEmail());
    }
}
```

In this case, Spring automatically injects the `EmailService` dependency into `UserService`, removing the need for manual object creation and wiring. This simplifies configuration and helps manage the complexity of the system.

### 5. Avoid Global States
Global states introduce hidden dependencies between components, making the system more difficult to understand and maintain. They also increase the risk of side effects, where one component inadvertently affects another due to shared state. Avoid global state wherever possible by passing objects explicitly or using Dependency Injection.

**Example**:
```java
// Bad Example - Global state with static variables
public class GlobalState {
    public static DatabaseConnection dbConnection = new DatabaseConnection();
}

// Good Example - Avoiding global state by using dependency injection
public class OrderProcessor {
    private final DatabaseConnection dbConnection;

    public OrderProcessor(DatabaseConnection dbConnection) {
        this.dbConnection = dbConnection;
    }

    public void processOrder(Order order) {
        // process order using dbConnection
    }
}
```

By avoiding global state, you reduce unexpected side effects and make it easier to track the flow of data through the system.

### 6. Keep Configuration at a Minimum
Configuration should be kept as simple as possible. Overly complex configuration adds another layer of difficulty when setting up or maintaining a system. By using sane defaults, minimizing configuration options, and automating where possible (for instance, by using convention over configuration), you can simplify the setup process.

**Example**:
```java
// Bad Example - Too much manual configuration
OrderProcessor processor = new OrderProcessor();
processor.setInventoryService(new InventoryService());
processor.setPaymentService(new PaymentService());

// Good Example - Automated configuration via constructor or dependency injection
public class OrderProcessor {
    private final InventoryService inventoryService;
    private final PaymentService paymentService;

    public OrderProcessor(InventoryService inventoryService, PaymentService paymentService) {
        this.inventoryService = inventoryService;
        this.paymentService = paymentService;
    }
}
```

### 7. Use Interfaces to Define Boundaries
When building systems, it’s important to define clear boundaries between components. Using interfaces to abstract implementation details provides flexibility, as you can easily swap out one implementation for another without affecting the system's overall behavior.

**Example**:
```java
// Bad Example - Tightly coupled classes
public class OrderProcessor {
    private PaymentService paymentService = new PaymentService();

    public void processOrder() {
        paymentService.processPayment();
    }
}

// Good Example - Using interfaces to define boundaries
public interface PaymentService {
    void processPayment();
}

public class OrderProcessor {
    private PaymentService paymentService;

    public OrderProcessor(PaymentService paymentService) {
        this.paymentService = paymentService;
    }

    public void processOrder() {
        paymentService.processPayment();
    }
}
```

By defining the `PaymentService` interface, you make it easy to swap in different payment processing mechanisms, improving flexibility.

### 8. Testing the System
It’s important to test systems at multiple levels. Unit tests focus on small, isolated pieces of functionality, but for a system, you also need integration and system tests. These tests ensure that components work together as expected.

- **Unit Tests**: Test individual components in isolation.
- **Integration Tests**: Test interactions between components.
- **System Tests**: Test the behavior of the system as a whole.

**Example**:
```java
// Integration test to verify interaction between components
@Test
public void testOrderProcessing() {
    PaymentService paymentService = mock(PaymentService.class);
    InventoryService inventoryService = mock(InventoryService.class);

    OrderProcessor orderProcessor = new OrderProcessor(paymentService, inventoryService);
    orderProcessor.processOrder(new Order());

    verify(paymentService).processPayment();
    verify(inventoryService).updateStock();
}
```

## Chapter 12: Emergence
### Introduction
Emergent design is a concept that allows a system's design to evolve through continuous refactoring and improvement rather than being completely defined upfront. In clean code, emergence happens as a result of following best practices, writing tests, and continuously improving the code. This chapter emphasizes how simple rules and principles can lead to a robust and flexible design that grows with the system’s needs.

### 1. Simple Design
The foundation of emergent design is keeping things simple. Complex designs are harder to maintain, understand, and change over time. A simple design that meets the current requirements is preferable to an overly complicated one that attempts to predict future needs.

The four rules of simple design are:
1. **Runs all the tests**.
2. **Contains no duplication**.
3. **Expresses the intent of the programmer**.
4. **Minimizes the number of classes and methods**.

These rules help ensure that the design evolves naturally, focusing on functionality and clarity rather than unnecessary complexity.

### 2. Runs All the Tests
A system is only as good as its ability to pass its tests. A core principle of emergent design is ensuring that the design allows for complete and comprehensive testing. Writing tests for every feature and behavior ensures that the system behaves correctly and that changes made to the code can be validated instantly.

- Write unit tests for small components.
- Write integration tests to verify components work together.
- Write system tests to ensure the entire system functions as expected.

By running all the tests regularly, you prevent regressions and ensure the code remains reliable as it evolves.

**Example**:
```java
// Example of a unit test ensuring that functionality works as intended
@Test
public void shouldCalculateOrderTotal() {
    Order order = new Order();
    order.addItem(new Item("Laptop", 1000));
    order.addItem(new Item("Mouse", 50));

    assertEquals(1050, order.getTotal());
}
```

### 3. No Duplication (DRY Principle)
Duplication is a sign of poor design. The presence of duplicated code makes the system harder to maintain and increases the risk of inconsistencies. Every piece of knowledge in the system should have a single, unambiguous representation. Refactoring code to remove duplication leads to cleaner, more maintainable code and encourages reuse of components.

Common sources of duplication:
- Repeating the same logic in multiple places.
- Duplicating data structures or methods across different parts of the code.
- Copying and pasting code instead of extracting reusable methods or classes.

**Example**:
```java
// Bad Example - Duplicate logic across methods
public class DiscountService {
    public double calculateDiscountForLoyalCustomer(double total) {
        return total * 0.9; // 10% discount
    }

    public double calculateDiscountForEmployee(double total) {
        return total * 0.9; // 10% discount
    }
}

// Good Example - Remove duplication by using a shared method
public class DiscountService {
    public double applyDiscount(double total, double discountRate) {
        return total * discountRate;
    }
}
```

### 4. Expresses the Programmer’s Intent
The code should clearly express the intention behind it. Code that is difficult to read or understand is prone to errors and difficult to maintain. Code clarity and readability are key to ensuring that anyone working on the code can easily understand what it is doing.

To express intent:
- Use meaningful names for classes, methods, and variables.
- Write code that is easy to follow and does not require comments to explain its purpose.
- Keep functions small and focused, doing one thing only.

**Example**:
```java
// Bad Example - Unclear method names and variables
public void process(int x, int y) {
    if (x > y) {
        // process something
    }
}

// Good Example - Clear method names and variables
public void processOrder(int orderTotal, int customerCredit) {
    if (orderTotal > customerCredit) {
        // handle insufficient credit
    }
}
```

### 5. Minimize the Number of Classes and Methods
Having too many classes or methods can lead to over-complication, making the system harder to understand and maintain. Each class and method should have a clear purpose and be used only when necessary. Keeping the system lean by minimizing the number of unnecessary classes or methods simplifies the design and improves overall readability.

This doesn’t mean you should avoid creating new classes or methods entirely; it means you should strive to balance between simplicity and maintainability.

**Example**:
```java
// Bad Example - Too many small, unnecessary classes
public class DiscountCalculator {
    public double applyDiscount(double total, double rate) {
        return total * rate;
    }
}

public class OrderProcessor {
    private DiscountCalculator calculator = new DiscountCalculator();

    public double processOrder(double total) {
        return calculator.applyDiscount(total, 0.9);
    }
}

// Good Example - Minimize unnecessary classes
public class OrderProcessor {
    public double processOrder(double total, double discountRate) {
        return total * discountRate;
    }
}
```

### 6. Continuous Refactoring
Refactoring is a vital practice in emergent design. Code is rarely perfect on the first attempt, and requirements change over time. Continuous refactoring ensures that the system remains clean and flexible as it evolves. By frequently revisiting the code and improving it, you maintain a high level of quality.

Key refactoring practices:
- Simplify complex logic.
- Remove code smells (e.g., long methods, large classes, duplication).
- Improve method names and variable names for better readability.

**Example**:
```java
// Refactoring a long method into smaller methods
public void processOrder(Order order) {
    validateOrder(order);
    applyDiscount(order);
    completePayment(order);
    sendOrderConfirmation(order);
}

private void validateOrder(Order order) { /* code */ }
private void applyDiscount(Order order) { /* code */ }
private void completePayment(Order order) { /* code */ }
private void sendOrderConfirmation(Order order) { /* code */ }
```


## Chapter 13: Concurrency
### Introduction
Concurrency allows multiple tasks to run simultaneously, which can improve a system’s efficiency and performance. However, it introduces complexity in terms of managing shared resources, synchronization, and ensuring that code behaves correctly in a concurrent environment. In this chapter, we explore the principles of writing clean, reliable, and maintainable concurrent code, while also discussing how to avoid common concurrency pitfalls.

### 1. Why Concurrency is Important
Concurrency enables systems to perform multiple operations at the same time, which is essential for handling tasks such as:
- Running background tasks (e.g., data processing, logging).
- Handling multiple user requests simultaneously in web applications.
- Performing I/O operations like reading from disk or making network requests without blocking the main execution thread.

Well-implemented concurrency can significantly improve the performance and responsiveness of your system.

### 2. Complexity of Concurrency
While concurrency brings many benefits, it also adds complexity to the code. Issues such as race conditions, deadlocks, and synchronization problems can arise if concurrency is not managed correctly. Clean concurrency requires careful design to avoid these pitfalls and ensure that the system remains maintainable.

Common challenges include:
- **Race Conditions**: When two or more threads access shared data at the same time, leading to inconsistent or unexpected results.
- **Deadlocks**: When two or more threads are waiting for each other to release resources, leading to a standstill.
- **Livelocks**: When threads continuously change their states in response to each other but fail to make progress.

### 3. Keep Synchronized Code Blocks Small
Synchronization is essential in concurrent programs to ensure that shared resources are accessed safely by multiple threads. However, large synchronized blocks reduce concurrency and can lead to performance bottlenecks. The key is to keep synchronized sections as small and focused as possible, protecting only the critical parts that need synchronization.

**Example**:
```java
// Bad Example - Large synchronized block
public synchronized void updateBalance(int amount) {
    balance += amount;
    logTransaction();
    notifyUser();
}

// Good Example - Smaller synchronized block
public void updateBalance(int amount) {
    synchronized (this) {
        balance += amount;
    }
    logTransaction();
    notifyUser();
}
```

In the good example, only the update to the `balance` is synchronized, allowing the other operations (`logTransaction()` and `notifyUser()`) to run concurrently without locking.

### 4. Minimize Shared Data
Concurrency problems often arise when multiple threads share data. One way to avoid these problems is to minimize the use of shared data between threads. When possible, give each thread its own copy of the data or pass immutable objects between threads to prevent accidental modification.

**Example**:
```java
// Bad Example - Sharing mutable data between threads
public class SharedCounter {
    public int counter = 0;
}

SharedCounter counter = new SharedCounter();
Thread t1 = new Thread(() -> counter.counter++);
Thread t2 = new Thread(() -> counter.counter++);

// Good Example - Using thread-local data
ThreadLocal<Integer> threadCounter = ThreadLocal.withInitial(() -> 0);

Thread t1 = new Thread(() -> threadCounter.set(threadCounter.get() + 1));
Thread t2 = new Thread(() -> threadCounter.set(threadCounter.get() + 1));
```

In the good example, each thread has its own copy of the `counter` value, reducing the likelihood of concurrency issues.

### 5. Use Immutable Objects
Immutable objects are inherently thread-safe because they cannot be modified after they are created. By using immutable objects, you eliminate the risk of data being altered by multiple threads simultaneously, which makes concurrency management easier.

**Example**:
```java
// Immutable class
public final class User {
    private final String name;
    private final String email;

    public User(String name, String email) {
        this.name = name;
        this.email = email;
    }

    public String getName() {
        return name;
    }

    public String getEmail() {
        return email;
    }
}
```

Because the `User` class is immutable, it is safe to share instances of `User` across multiple threads without worrying about synchronization.

### 6. Use Libraries and Frameworks
When dealing with concurrency, it’s often better to use well-established libraries and frameworks rather than reinventing concurrency mechanisms from scratch. Java’s `java.util.concurrent` package provides many utilities, such as `Executors`, `CountDownLatch`, `Semaphore`, and `ConcurrentHashMap`, that simplify concurrency management.

**Example**:
```java
// Using ExecutorService for managing threads
ExecutorService executorService = Executors.newFixedThreadPool(5);

for (int i = 0; i < 10; i++) {
    executorService.submit(() -> {
        System.out.println("Task executed by: " + Thread.currentThread().getName());
    });
}

executorService.shutdown();
```

Using the `ExecutorService` framework abstracts away many of the complexities of manually creating and managing threads, leading to cleaner and more maintainable concurrent code.

### 7. Avoid Using `Thread.sleep()` for Synchronization
Using `Thread.sleep()` to control the timing of threads is generally unreliable and can lead to non-deterministic behavior. Instead of relying on arbitrary delays, use proper synchronization mechanisms such as locks, semaphores, or latches to coordinate the timing between threads.

**Example**:
```java
// Bad Example - Using Thread.sleep for synchronization
Thread t1 = new Thread(() -> {
    doWork();
    try {
        Thread.sleep(1000); // hoping the other thread completes by then
    } catch (InterruptedException e) {
        e.printStackTrace();
    }
    continueWork();
});

// Good Example - Using CountDownLatch for synchronization
CountDownLatch latch = new CountDownLatch(1);

Thread t1 = new Thread(() -> {
    doWork();
    latch.countDown(); // signal that work is done
});

Thread t2 = new Thread(() -> {
    try {
        latch.await(); // wait for t1 to finish
    } catch (InterruptedException e) {
        e.printStackTrace();
    }
    continueWork();
});
```

By using `CountDownLatch`, the threads synchronize in a more predictable way, ensuring proper coordination without arbitrary sleep delays.

### 8. Know the Risks of Concurrent Code
Concurrency introduces the risk of bugs that can be difficult to reproduce and debug, such as race conditions and deadlocks. Testing concurrent code is challenging because errors may not appear consistently. To mitigate these risks:
- Use stress tests to detect issues under heavy load.
- Carefully design thread interactions.
- Use proper tools (e.g., debuggers or profilers) to track down issues when they occur.

### 9. Avoid Premature Optimization
Concurrency can enhance performance, but optimizing for concurrency too early can introduce unnecessary complexity. Before introducing concurrency, ensure that it is needed by identifying performance bottlenecks. Focus first on writing clear, maintainable code and apply concurrency only where it provides a clear benefit.


## Chapter 14: Successive Refinement
### Introduction
Successive refinement is a process of continuously improving and polishing your code over time. The idea is that code is not written perfectly on the first attempt, but instead evolves through regular refactoring and improvements. This chapter emphasizes the importance of iterative improvements to make code cleaner, more readable, and more maintainable.

### 1. Clean Code Is Evolved, Not Written
Writing clean code is a process that happens over time. Instead of expecting to write perfect code on the first pass, developers should focus on creating a working solution first and then refining it through successive iterations. Continuous refinement leads to better design, improved structure, and increased readability.

**Example**:
```java
// Initial, working but not clean code
public double calculateDiscount(double price, boolean isLoyalCustomer) {
    if (isLoyalCustomer) {
        return price * 0.9;
    } else {
        return price;
    }
}

// Refined code after successive iterations
public double calculateDiscount(double price, boolean isLoyalCustomer) {
    return isLoyalCustomer ? price * 0.9 : price;
}
```

### 2. Refactoring Is a Continuous Process
Refactoring is a key element of successive refinement. It involves restructuring existing code without changing its external behavior to improve its internal structure. Refactoring should be done regularly, and it helps eliminate technical debt, improve code clarity, and keep the codebase healthy.

**Common Refactoring Practices**:
- **Rename variables and methods** for clarity.
- **Extract methods** to simplify long methods or reduce duplication.
- **Remove dead code** that is no longer used.
- **Consolidate duplicate logic** into shared methods.

**Example**:
```java
// Before refactoring - method doing too much
public void processOrder(Order order) {
    // validate order
    if (order.isValid()) {
        // process payment
        processPayment(order);
        // send confirmation
        sendConfirmation(order);
    }
}

// After refactoring - cleaner, smaller methods
public void processOrder(Order order) {
    if (order.isValid()) {
        processPayment(order);
        sendConfirmation(order);
    }
}
```

### 3. The Importance of Feedback
Feedback is essential for successive refinement. Testing, both automated and manual, provides immediate feedback about the behavior of the code and helps ensure that refactoring does not introduce new bugs. Unit tests, integration tests, and code reviews are all important feedback mechanisms.

- **Unit Tests**: Ensure that small pieces of functionality work as intended.
- **Integration Tests**: Verify that different parts of the system work together.
- **Code Reviews**: Offer feedback on code structure, readability, and adherence to best practices.

The process of refining code should be backed by reliable tests to catch any potential errors introduced during refactoring.

### 4. Small, Incremental Changes
It’s easier to refine code by making small, incremental changes rather than attempting large-scale rewrites. Small changes are easier to test, understand, and review. Incremental improvements allow for safer, more controlled development and make it easier to identify and fix issues.

**Example**:
```java
// Small change improving readability and reusability
public void sendConfirmationEmail(Order order) {
    EmailService.send(order.getCustomerEmail(), "Your order has been processed.");
}
```

### 5. Avoid Big Rewrites
Big rewrites are often tempting when the codebase becomes cluttered, but they carry a high risk of introducing bugs and losing important context. Instead, focus on gradual improvements through refactoring. Over time, the codebase will become more manageable and cleaner without needing a complete overhaul.

**Reasons to Avoid Big Rewrites**:
- **Loss of context**: Understanding why certain decisions were made in the original code might be lost.
- **Risk of introducing bugs**: A rewrite might overlook edge cases or business logic that was already accounted for.
- **Time-consuming**: Big rewrites take considerable time and may slow down progress.

### 6. Working Code Is the Foundation
Always start with a working solution before refactoring. The goal of successive refinement is to improve upon what already works. Trying to refactor broken or incomplete code makes it harder to identify issues and introduces unnecessary complexity.

**Steps for Successive Refinement**:
1. Write a working solution.
2. Ensure it is covered by tests.
3. Refactor to improve readability, reduce complexity, and remove duplication.
4. Continuously test after each small refactoring step.

### 7. Don’t Sacrifice Readability for Performance
It’s easy to be tempted by performance optimizations, but they should never come at the expense of code readability or maintainability. Premature optimization can introduce complexity and make the code harder to understand. Always prioritize clean code and only optimize performance when necessary, and when you have evidence that it’s needed.

**Example**:
```java
// Bad Example - Optimized but unreadable code
public int sumArray(int[] numbers) {
    int sum = 0;
    for (int i = 0; i < numbers.length; i++) sum += numbers[i];
    return sum;
}

// Good Example - Readable, maintainable code
public int sumArray(int[] numbers) {
    int sum = 0;
    for (int number : numbers) {
        sum += number;
    }
    return sum;
}
```

### 8. Embrace Iteration
Successive refinement is an iterative process. You might not know the perfect design right away, but through regular, iterative improvements, the code becomes cleaner, simpler, and more aligned with best practices. This iterative mindset allows developers to constantly adapt and evolve the system as requirements change.

## Chapter 15: JUnit Internals
### Introduction
JUnit is one of the most widely used testing frameworks for Java. It provides developers with the tools to write automated unit tests, which are essential for ensuring code correctness and reliability. This chapter explores the internals of JUnit, giving insight into how it works behind the scenes, and discusses how to write effective and efficient unit tests using JUnit.

### 1. The Anatomy of a JUnit Test
JUnit tests are typically composed of a few key parts:
- **Annotations**: JUnit uses annotations to indicate the role of each method in a test class.
- **Assertions**: Assertions verify that the expected outcome matches the actual result.
- **Test Runner**: The test runner executes the tests and reports the results.

**Common Annotations**:
- `@Test`: Marks a method as a test method.
- `@Before`: Executes before each test to set up the environment.
- `@After`: Executes after each test to clean up resources.
- `@BeforeClass`: Executes once before any test methods are run.
- `@AfterClass`: Executes once after all test methods are finished.

**Example**:
```java
public class CalculatorTest {

    private Calculator calculator;

    @Before
    public void setUp() {
        calculator = new Calculator();
    }

    @Test
    public void testAdd() {
        int result = calculator.add(2, 3);
        assertEquals(5, result);
    }

    @After
    public void tearDown() {
        calculator = null;
    }
}
```

### 2. Test Fixtures
A **test fixture** is a fixed state of a set of objects used as a baseline for running tests. By setting up a test fixture, you ensure that each test runs in a controlled and consistent environment. The `@Before` and `@After` annotations help set up and tear down these test fixtures.

- `@Before` is used to initialize objects or set up test data before each test method.
- `@After` is used to clean up resources, such as closing files or clearing caches, after each test.

**Example**:
```java
@Before
public void setUp() {
    calculator = new Calculator();
}

@After
public void tearDown() {
    // Clean up resources
    calculator = null;
}
```

### 3. Assertions
Assertions are a crucial part of JUnit tests as they determine whether the actual result matches the expected result. JUnit provides several assertion methods to verify different conditions, such as equality, null values, and exceptions.

**Common Assertions**:
- `assertEquals(expected, actual)`: Checks if two values are equal.
- `assertTrue(condition)`: Verifies that a condition is true.
- `assertFalse(condition)`: Verifies that a condition is false.
- `assertNotNull(object)`: Verifies that an object is not `null`.
- `assertThrows(exceptionClass, () -> code)`: Asserts that an exception is thrown.

**Example**:
```java
@Test
public void testDivision() {
    int result = calculator.divide(10, 2);
    assertEquals(5, result);
}

@Test(expected = ArithmeticException.class)
public void testDivisionByZero() {
    calculator.divide(10, 0);
}
```

### 4. Parameterized Tests
JUnit supports **parameterized tests**, which allow you to run the same test logic with different input values. This is useful for testing a method with various combinations of inputs and expected outputs without writing multiple test methods.

To use parameterized tests, you can annotate a test class with `@RunWith(Parameterized.class)` and define a set of parameters.

**Example**:
```java
@RunWith(Parameterized.class)
public class ParameterizedTest {

    private int input1;
    private int input2;
    private int expected;

    public ParameterizedTest(int input1, int input2, int expected) {
        this.input1 = input1;
        this.input2 = input2;
        this.expected = expected;
    }

    @Parameterized.Parameters
    public static Collection<Object[]> data() {
        return Arrays.asList(new Object[][] {
            {1, 2, 3}, {2, 3, 5}, {3, 4, 7}
        });
    }

    @Test
    public void testAdd() {
        assertEquals(expected, new Calculator().add(input1, input2));
    }
}
```

### 5. Test Suites
A **test suite** is a collection of test classes that can be run together. Test suites allow you to group related tests, making it easier to organize and run multiple tests at once.

You create a test suite using the `@RunWith(Suite.class)` annotation and the `@Suite.SuiteClasses` annotation to specify the test classes.

**Example**:
```java
@RunWith(Suite.class)
@Suite.SuiteClasses({
    CalculatorTest.class,
    AdvancedCalculatorTest.class
})
public class CalculatorTestSuite {
    // This class remains empty; it is used only as a holder for the above annotations
}
```

### 6. Exception Testing
Sometimes, you need to test that certain methods throw specific exceptions under certain conditions. JUnit provides built-in support for testing exceptions using the `@Test(expected = Exception.class)` annotation or `assertThrows()`.

**Example**:
```java
@Test(expected = ArithmeticException.class)
public void testDivisionByZero() {
    calculator.divide(10, 0);
}

@Test
public void testDivideWithAssertThrows() {
    assertThrows(ArithmeticException.class, () -> calculator.divide(10, 0));
}
```

### 7. The Importance of Isolation in Unit Tests
Unit tests should be isolated from external dependencies such as databases, file systems, or networks. If a test interacts with external systems, it may be harder to maintain and slower to execute. Use mocking frameworks (e.g., Mockito) to simulate external dependencies in unit tests.

**Example** using Mockito:
```java
@Test
public void testOrderProcessing() {
    PaymentService paymentService = mock(PaymentService.class);
    OrderService orderService = new OrderService(paymentService);

    when(paymentService.processPayment(anyDouble())).thenReturn(true);

    boolean result = orderService.processOrder(100.0);
    assertTrue(result);
    verify(paymentService).processPayment(100.0);
}
```

### 8. Test-Driven Development (TDD) and JUnit
JUnit is often used as part of a **Test-Driven Development (TDD)** workflow. TDD encourages writing tests before writing the actual code, guiding the development process and ensuring that all code is testable and serves a specific purpose.

**The TDD Cycle**:
1. **Write a failing test**: Start by writing a test that defines the desired behavior but fails because the code is not implemented yet.
2. **Write the simplest code** to make the test pass.
3. **Refactor** the code to improve its structure while ensuring that all tests still pass.

**Example**:
```java
// Step 1: Write a failing test
@Test
public void testMultiply() {
    Calculator calculator = new Calculator();
    assertEquals(20, calculator.multiply(4, 5)); // Test fails because multiply() is not implemented
}

// Step 2: Write code to pass the test
public int multiply(int a, int b) {
    return a * b;
}

// Step 3: Refactor if necessary
```

## Chapter 16: Refactoring
### Introduction
Refactoring is the process of improving the design of existing code without changing its external behavior. It helps to enhance code readability, maintainability, and performance by removing technical debt and cleaning up messy or inefficient code. In this chapter, we focus on the principles and strategies for effective refactoring, ensuring your codebase stays clean and easy to modify over time.

### 1. The Purpose of Refactoring
Refactoring is essential for keeping your codebase clean and adaptable. As code evolves, complexity tends to increase, making it harder to understand and maintain. Refactoring helps reduce complexity, eliminate duplication, and improve the design of the code. It should be a continuous process throughout the lifecycle of a project.

Reasons to refactor:
- Improve code readability.
- Simplify complex code.
- Reduce duplication.
- Make future modifications easier.
- Eliminate code smells.

### 2. Refactor Continuously
Refactoring should be done regularly and incrementally as part of your daily development routine, not saved for a big "cleanup" at the end. Small, frequent refactoring ensures the codebase remains clean and manageable without the risk of introducing large-scale bugs.

**Example**:
```java
// Before Refactoring - Long, complex method
public void calculateTotalOrderPrice(Order order) {
    double total = 0;
    for (Item item : order.getItems()) {
        if (item.isOnSale()) {
            total += item.getPrice() * 0.9; // apply discount
        } else {
            total += item.getPrice();
        }
    }
    System.out.println("Total price: " + total);
}

// After Refactoring - Break down into smaller methods
public void calculateTotalOrderPrice(Order order) {
    double total = order.getItems().stream().mapToDouble(this::calculateItemPrice).sum();
    System.out.println("Total price: " + total);
}

private double calculateItemPrice(Item item) {
    return item.isOnSale() ? item.getPrice() * 0.9 : item.getPrice();
}
```

### 3. Code Smells
"Code smells" are indicators of potential problems in your code that suggest it needs refactoring. Code smells are not bugs, but they can lead to poor design, making the code harder to maintain and extend.

**Common Code Smells**:
- **Long Methods**: Methods that do too much and are difficult to understand.
- **Duplicated Code**: Repeated logic that should be extracted into a reusable method or class.
- **Large Classes**: Classes with too many responsibilities.
- **Switch Statements**: Frequent switch statements that could be replaced with polymorphism.
- **Long Parameter Lists**: Methods with too many parameters, making them harder to understand and maintain.
- **Comments**: If comments are required to explain code, it may indicate the code is unclear and needs refactoring.

**Example** (Code Smell: Long Method):
```java
// Long method with too much responsibility
public void processOrder(Order order) {
    double total = 0;
    for (Item item : order.getItems()) {
        total += item.getPrice();
    }
    if (order.isPriority()) {
        shipPriorityOrder(order);
    } else {
        shipStandardOrder(order);
    }
    order.markAsProcessed();
}
```

**Refactored**:
```java
// Refactored code with smaller, focused methods
public void processOrder(Order order) {
    double total = calculateTotalPrice(order);
    shipOrder(order);
    order.markAsProcessed();
}

private double calculateTotalPrice(Order order) {
    return order.getItems().stream().mapToDouble(Item::getPrice).sum();
}

private void shipOrder(Order order) {
    if (order.isPriority()) {
        shipPriorityOrder(order);
    } else {
        shipStandardOrder(order);
    }
}
```

### 4. Common Refactoring Techniques

#### Extract Method
If a method is doing too much or is difficult to understand, you can refactor by breaking it down into smaller, more focused methods.

**Example**:
```java
// Before refactoring - one large method
public void generateReport() {
    // code to gather data
    // code to format data
    // code to output report
}

// After refactoring - separate methods for each responsibility
public void generateReport() {
    gatherData();
    formatData();
    outputReport();
}

private void gatherData() { /* ... */ }
private void formatData() { /* ... */ }
private void outputReport() { /* ... */ }
```

#### Replace Magic Numbers with Constants
Using magic numbers directly in your code can make it hard to understand and modify. Instead, replace them with named constants.

**Example**:
```java
// Before - magic number
public double applyDiscount(double price) {
    return price * 0.9;
}

// After - use a constant for clarity
private static final double DISCOUNT_RATE = 0.9;

public double applyDiscount(double price) {
    return price * DISCOUNT_RATE;
}
```

#### Inline Method
If a method does very little and does not add clarity, you can inline it to simplify the code.

**Example**:
```java
// Before - unnecessary method
public int getDiscountedPrice(Item item) {
    return item.getPrice() * 0.9;
}

// After - inlined method for simplicity
public int getDiscountedPrice(Item item) {
    return item.getPrice() * 0.9; // Directly calculate the discount
}
```

#### Remove Dead Code
Unused code, such as outdated methods or variables, should be removed to avoid confusion and reduce the codebase size.

**Example**:
```java
// Before - unused method
public void oldMethod() {
    // deprecated code
}

// After - method removed
```

#### Encapsulate Field
Directly exposing fields can lead to unintended modifications. Encapsulate fields by using getter and setter methods to control access.

**Example**:
```java
// Before - direct field access
public class User {
    public String name;
}

// After - encapsulated field
public class User {
    private String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

### 5. Benefits of Refactoring
Refactoring brings many benefits to a codebase, including:
- **Improved Readability**: Code becomes easier to understand and follow.
- **Better Maintainability**: Refactoring simplifies code, making future modifications easier.
- **Reduced Complexity**: Refactoring breaks down complex logic into smaller, more manageable pieces.
- **Increased Reusability**: By removing duplication and creating reusable methods, code can be reused in multiple places.
- **Reduced Technical Debt**: Regular refactoring prevents technical debt from building up over time.

### 6. Refactoring Safely
To refactor safely and avoid introducing bugs, follow these best practices:
- **Test Before Refactoring**: Make sure your code works before you start refactoring.
- **Refactor in Small Steps**: Refactor small pieces of code incrementally and frequently.
- **Run Tests After Each Change**: Ensure the behavior of the system remains unchanged by running tests after each refactoring step.
- **Use Version Control**: Keep track of your refactoring changes with version control so you can roll back if something goes wrong.

### 7. Test-Driven Refactoring
Refactoring works best in conjunction with **Test-Driven Development (TDD)**. By writing tests first, you ensure that you have full test coverage. This allows you to confidently refactor code while knowing that if you break anything, your tests will catch it.

**Example**:
```java
// Step 1: Write tests for the current functionality
@Test
public void testCalculateTotal() {
    // ensure tests pass before refactoring
}

// Step 2: Refactor the code
public double calculateTotal(List<Item> items) {
    return items.stream().mapToDouble(Item::getPrice).sum();
}

// Step 3: Run tests again to ensure the behavior remains unchanged
```

## Chapter 17: Smells and Heuristics
### Introduction
Code "smells" are indicators of potential issues in your code that suggest it may need refactoring. These smells are not necessarily bugs, but they point to deeper design problems that can lead to unmaintainable, inefficient, or confusing code. This chapter discusses common code smells and heuristics, which are patterns or principles that help you identify problems and guide you toward cleaner code.

### 1. Code Smells Overview
Code smells are typically signs that the code structure needs improvement. While code may still function correctly, code smells suggest deeper problems that could lead to issues as the codebase grows. Recognizing and addressing these smells early can save you from technical debt, making the system easier to maintain and extend.

### 2. Common Code Smells

#### 1. **Duplicated Code**
Duplicated code occurs when the same or very similar code appears in multiple places. This increases the maintenance cost because any changes must be applied to all the duplicated sections, making the code harder to maintain and prone to errors.

**Example**:
```java
// Bad Example - Duplicated code in multiple methods
public void processOrder(Order order) {
    double total = order.getTotal();
    if (order.isPriority()) {
        total *= 0.9; // apply discount
    }
    shipOrder(order, total);
}

public void processReturn(Return orderReturn) {
    double total = orderReturn.getTotal();
    if (orderReturn.isPriority()) {
        total *= 0.9; // apply discount
    }
    processRefund(orderReturn, total);
}

// Good Example - Removing duplication by extracting method
public void processOrder(Order order) {
    double total = calculateTotal(order);
    shipOrder(order, total);
}

public void processReturn(Return orderReturn) {
    double total = calculateTotal(orderReturn);
    processRefund(orderReturn, total);
}

private double calculateTotal(Purchase purchase) {
    double total = purchase.getTotal();
    if (purchase.isPriority()) {
        total *= 0.9;
    }
    return total;
}
```

#### 2. **Long Methods**
Methods that are too long tend to be difficult to understand and maintain. They often try to do too much, violating the **Single Responsibility Principle**. Long methods can be refactored by breaking them into smaller, more focused methods.

**Example**:
```java
// Bad Example - Long method doing too much
public void processPayment(Payment payment) {
    if (payment.isCreditCard()) {
        processCreditCard(payment);
    } else if (payment.isPayPal()) {
        processPayPal(payment);
    }
    logTransaction(payment);
    sendReceipt(payment);
}

// Good Example - Shorter, refactored methods
public void processPayment(Payment payment) {
    handlePaymentMethod(payment);
    logTransaction(payment);
    sendReceipt(payment);
}

private void handlePaymentMethod(Payment payment) {
    if (payment.isCreditCard()) {
        processCreditCard(payment);
    } else if (payment.isPayPal()) {
        processPayPal(payment);
    }
}
```

#### 3. **Large Classes**
A large class often indicates that it has too many responsibilities. These classes violate the **Single Responsibility Principle** and are difficult to understand, test, and maintain. Large classes can be refactored by splitting them into smaller, more focused classes with distinct responsibilities.

**Example**:
```java
// Bad Example - Large class doing too much
public class OrderManager {
    public void addOrder(Order order) { /* code */ }
    public void removeOrder(Order order) { /* code */ }
    public void sendInvoice(Order order) { /* code */ }
    public void calculateOrderStats(Order order) { /* code */ }
}

// Good Example - Breaking up responsibilities into smaller classes
public class OrderManager {
    public void addOrder(Order order) { /* code */ }
    public void removeOrder(Order order) { /* code */ }
}

public class InvoiceService {
    public void sendInvoice(Order order) { /* code */ }
}

public class OrderStatistics {
    public void calculateOrderStats(Order order) { /* code */ }
}
```

#### 4. **Switch Statements**
Switch statements are often a sign that the code could benefit from polymorphism. Instead of using a switch to determine the behavior based on a type, you can use object-oriented techniques like inheritance or interfaces to delegate behavior to the appropriate class.

**Example**:
```java
// Bad Example - Using switch statement for type checking
public void processPayment(Payment payment) {
    switch (payment.getType()) {
        case "creditCard":
            processCreditCard(payment);
            break;
        case "paypal":
            processPayPal(payment);
            break;
    }
}

// Good Example - Replacing switch with polymorphism
public void processPayment(Payment payment) {
    payment.process(); // Each payment type has its own process method
}

public abstract class Payment {
    public abstract void process();
}

public class CreditCardPayment extends Payment {
    @Override
    public void process() {
        // process credit card payment
    }
}

public class PayPalPayment extends Payment {
    @Override
    public void process() {
        // process PayPal payment
    }
}
```

#### 5. **Data Clumps**
Data clumps refer to a group of variables that are often found together in multiple places. These can usually be replaced by introducing a class that encapsulates these related variables.

**Example**:
```java
// Bad Example - Data clumps with repeated parameters
public void bookFlight(String firstName, String lastName, String passportNumber) {
    // code
}

public void checkIn(String firstName, String lastName, String passportNumber) {
    // code
}

// Good Example - Using a class to encapsulate related data
public void bookFlight(Passenger passenger) {
    // code
}

public void checkIn(Passenger passenger) {
    // code
}

public class Passenger {
    private String firstName;
    private String lastName;
    private String passportNumber;

    // Constructor, getters, and setters
}
```

#### 6. **Primitive Obsession**
Primitive obsession refers to overusing primitive types to represent domain concepts, such as using integers, strings, or floats instead of creating meaningful classes. Replacing primitives with domain-specific classes makes the code more expressive and reduces the chances of invalid values.

**Example**:
```java
// Bad Example - Using primitives for domain concepts
public void createAccount(String accountNumber, double balance) {
    // code
}

// Good Example - Replacing primitives with value objects
public void createAccount(AccountNumber accountNumber, Money balance) {
    // code
}

public class AccountNumber {
    private String value;
    // constructor, validation, and other methods
}

public class Money {
    private double amount;
    // constructor and validation
}
```

### 3. Heuristics for Clean Code

#### 1. **Single Responsibility Principle (SRP)**
A class or method should have only one reason to change, meaning it should only be responsible for one thing. Following SRP makes the code easier to maintain, test, and extend.

#### 2. **Open/Closed Principle**
Classes and methods should be **open for extension** but **closed for modification**. You should be able to extend the behavior of a class without modifying its existing code. This principle is often achieved using polymorphism or interfaces.

#### 3. **DRY (Don’t Repeat Yourself)**
Avoid duplication in your code. Whenever you find the same or similar code in multiple places, it’s a sign that the code could be refactored. DRY reduces redundancy and the chance of inconsistencies across the codebase.

#### 4. **YAGNI (You Aren’t Gonna Need It)**
Don’t add functionality until you actually need it. Avoid the temptation to write code that may be useful later. This keeps the codebase simple and focused on the current requirements.

#### 5. **KISS (Keep It Simple, Stupid)**
Keep your code as simple as possible. Avoid over-engineering or adding unnecessary complexity. Simple code is easier to understand, maintain, and extend.

### 4. Refactoring to Remove Code Smells
Refactoring is the process of improving the internal structure of the code without changing its behavior. You should refactor regularly to eliminate code smells, following best practices like breaking up large classes, reducing method complexity, and simplifying conditionals.

**Example**:
```java
// Before Refactoring - Long method, multiple responsibilities
public void processTransaction(Transaction transaction) {
    double amount = transaction.getAmount();
    if (transaction.getType() == "credit") {
        // handle credit transaction
    } else if (transaction.getType() == "debit") {
        // handle debit transaction
    }
    logTransaction(transaction);
    sendConfirmation(transaction);
}

// After Refactoring - Split responsibilities
public void processTransaction(Transaction transaction) {
    handleTransactionType(transaction);
    logTransaction(transaction);
    sendConfirmation(transaction);
}

private void handleTransactionType(Transaction transaction) {
    if (transaction.isCredit()) {
        processCredit(transaction);
    } else {
        processDebit(transaction);
    }
}
```