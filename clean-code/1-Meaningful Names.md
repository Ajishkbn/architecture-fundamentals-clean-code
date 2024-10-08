# Meaningful Names

Craft names that clearly convey the purpose and usage of variables, functions, and classes. Meaningful names make your code self-explanatory, reducing the need for additional documentation and improving overall readability.

## Intention-Revealing Names

Names in your code should clearly convey the purpose and usage of a variable, function, or class. This makes your code more understandable and maintainable.

### Example in C++

#### Violation

```cpp
int d; //elapsed time in days
```

#### Correction

```cpp
int elapsedTimeInDays;  // Clear and descriptive
```

### Explanation

- `d` is ambiguous and doesn't tell the reader what it represents.
- `elapsedTimeInDays` immediately tells you that the variable tracks time in days, making the code self-explanatory.

## Avoid Disinformation

Names should not mislead the reader about the purpose or behavior of the variable, function, or class. Misleading names can cause confusion and errors in your code.

### Example in C++

#### Violation

```cpp
int accountList;  // Actually holds a count accounts
std::list<Account> accounts; //Actually holds a list of accounts
```

#### Correction

```cpp
int accountCount;  // Actually holds a count accounts
std::list<Account> accountList; //Actually holds a list of accounts
```

### Explanation

- Do not refer to a grouping of accounts as an `accountList` unless it's actually a `List`

## Make Meaningful Distinctions

Names should clearly differentiate between different concepts or entities. Avoid using names that are similar but do not convey distinct meanings, as this can lead to confusion and reduce code clarity.

### Example in C++

#### Violation

```cpp
int dataInfo;   // Unclear distinction from 'data'
int data;       // Both names are too similar
```

#### Correction

```cpp
int userInfo;   // Clear and distinct from 'data'
int rawData;    // Specifies that this is raw data, making the distinction meaningful
```

### Explanation

- `dataInfo` and `data` are too similar, making it unclear how they differ or what each represents.
- `userInfo` and `rawData` clearly distinguish between the type of data each variable holds, making the code more understandable and reducing the chance of errors.

## Use Pronounceable Names

Names in your code should be easy to pronounce, which helps in communication and discussion among developers. Using pronounceable names improves the readability and maintainability of the code.

### Example in C++

#### Violation

```cpp
int genymdhms;  // Unpronounceable abbreviation for generation year, month, day, hour, minute, second
```

#### Correction

```cpp
int generationTimestamp;  // Clear and easy to pronounce
```

### Explanation

- `genymdhms` is a cryptic abbreviation that is difficult to pronounce and understand, making discussions about the code harder.
- `generationTimestamp` is clear, descriptive, and easy to pronounce, facilitating better communication among developers and improving overall code readability.

## Use Searchable Names

Names should be easy to locate in the codebase. Using meaningful and descriptive names makes searching for variables, functions, or classes easier, especially in large codebases.

### Example in C++

#### Violation

```cpp
int x;  // What does 'x' represent?
```

#### Correction

```cpp
int maxUserLimit;  // Descriptive and easy to search for
```

### Explanation

- `x` is too generic and difficult to search for in the code, especially when there are many occurrences of the same letter or similar names.
- `maxUserLimit` is a specific, descriptive name that can be easily searched, making it simpler to find where this variable is used or defined in the code, thereby improving maintainability.

## Avoid Encoding

Names should not include unnecessary prefixes, suffixes, or other forms of encoding. Encoded names can be harder to read, understand, and maintain. The code should be self-explanatory without relying on naming conventions that include type or scope information.

### Example in C++

#### Violation

```cpp
class IShape { // Encoded with 'I' for Interface
public:
    virtual void draw() = 0;
};

class CRectangle : public IShape { // Encoded with 'C' for Class
public:
    void draw() override;
};
```

#### Correction

```cpp
class Shape { // Simple and descriptive
public:
    virtual void draw() = 0;
};

class Rectangle : public Shape { // Clear and straightforward
public:
    void draw() override;
};
```

### Explanation

- `IShape` and `CRectangle` use encoding to differentiate between interfaces and classes, which can make names less intuitive and harder to understand, especially for newcomers to the codebase.
- `Shape` and `Rectangle` are descriptive without encoding, making the code easier to read and maintain. Modern development practices and tools provide sufficient context to distinguish between interfaces and implementations without relying on encoding in names.

## Avoid Mental Mapping

Names should be self-explanatory and not require the reader to infer meaning or perform mental mapping. Code should be clear and intuitive, reducing the need for extra effort to understand what names represent.

### Example in C++

#### Violation

```cpp
int b;  // What does 'b' represent?
```

#### Correction

```cpp
int balance;  // Clear and self-explanatory
```

### Explanation

- `b` is ambiguous and requires the reader to mentally map or guess its purpose, which can lead to misunderstandings and increased cognitive load.
- `balance` clearly describes what the variable represents, making the code easier to understand at a glance and reducing the need for additional explanation or mental effort.

## Use Meaningful Class Names

Class names should be descriptive and convey the role or purpose of the class. Avoid generic names or abbreviations that require additional context to understand. This improves readability and helps maintain clarity in your code.

### Example in C++

#### Violation

```cpp
class DataProcessor {  // Too generic
public:
    void process();
};
```

#### Correction

```cpp
class UserAccountManager {  // Clear and specific
public:
    void createAccount();
    void deleteAccount();
};
```

### Explanation

- `DataProcessor` is a generic name that does not convey the specific role or responsibilities of the class, making it less clear what the class is actually responsible for.
- `UserAccountManager` is a meaningful name that clearly indicates the class manages user accounts, making it immediately apparent what the class does and improving code readability and maintainability.

## Use Meaningful Function Names

Function names should clearly describe what the function does. Avoid vague or generic names that require additional context or explanation. This helps in understanding the purpose of the function at a glance.

### Examples in C++

1. **Use Verbs**

   Function and method names should be action-oriented, using verbs to describe what they do. A verb in the name provides an instant clue about the operation being performed. For instance:

   ```cpp
   void getPrice();  // Retrieves the price of something
   void postPayment();  // Responsible for posting payments
   ```

2. **Predicate Names for Boolean Functions**

    When a function returns a boolean value, it's advisable to name it like a predicate, which makes it more natural to use in conditional statements. For example:

    ```cpp
    bool isAuthorized();  // Reads like a question, enhancing readability in conditions
    ```

3. **Use "get" for Accessors**

    Accessors, which are methods used to retrieve the value of an attribute, should follow a consistent naming convention. Using the prefix "get" before the attribute's name helps identify their role. For example:

    ```cpp
    std::string getName();  // Retrieves the name of an entity
    double getAccountBalance();  // Retrieves an account's balance
    ```

4. **Use "set" for Mutators**

    Mutators, or setter methods, are used to modify the value of an attribute. Using the prefix "set" before the attribute's name clearly indicates their purpose. For example:

    ```cpp
    void setName(const std::string& name);  // Sets the name of an entity
    void setAccountBalance(double balance);  // Sets the account's balance
    ```

## Variable Naming Conventions

Well-chosen variable names can significantly enhance the readability and maintainability of your code. Here are some fundamental principles and examples for naming variables effectively:

1. **Nouns and Noun Phrases**

    Variables should typically be named using nouns or noun phrases that convey the purpose and content of the variable. These names should be clear and descriptive, making it easy for other developers (including your future self) to understand the variable's role in the code:

    ```cpp
    // Represents an account object
    Account account;  

    // A list that contains customer objects
    std::vector<Customer> customerList;  

    // Holds the total amount of something
    double totalAmount;
    ```  

2. **Boolean Variables and Predicates**

    Boolean variables are often used in conditional statements, where their names should be structured as predicates. This naming convention makes the code more natural to read and understand:

    ```cpp
    bool isEmpty = true;  // Indicates if something is empty

    if (isEmpty) {
        // Code to execute if the variable is true
    }

    // Determines if something is valid
    bool isValid = checkValidity();

    if (isValid) {
        // Code to execute if the variable is true
    }
    ```

3. **Enums and Adjectives**

    For enum types, which represent a set of constant values, it's a common convention to use adjectives in the enum values. This helps to add context and meaning to the code:

    ```cpp
    enum Status {
        PENDING,    // Indicates a pending status
        CLOSED,     // Indicates a closed status
        CANCELED    // Indicates a canceled status
    };
    ```

## Don’t Be Cute

Names in your code should be straightforward and unambiguous, avoiding playful or obscure names that can lead to confusion. Stick to clear and descriptive names that convey the exact purpose of the code elements.

### Example in C++

#### Violation

```cpp
class holyHandGranade {
public:
    void whack() { /*...*/ }
};
```

#### Correction

```cpp
class ItemDeleter {
public:
    void deleteItems() { /*...*/ }
};
```

### Explanation

- `holyHandGranade` is a playful name that does not clearly indicate its function, leading to confusion.
- `ItemDeleter` and `deleteItems` are straightforward names that clearly describe the purpose of the class and method, improving code clarity.

## Pick One Word Per Concept

Use a single word consistently for a specific concept across your codebase. Avoid mixing synonyms or similar terms for the same concept, as this can cause confusion.

### Example in C++

#### Violation

```cpp
class DataManager {
public:
    void fetchData() { /*...*/ }
    void retrieveData() { /*...*/ }
    void getData() { /*...*/ }
};
```

#### Correction

```cpp
class DataManager {
public:
    void getData() { /*...*/ }
};
```

### Explanation

- Using `fetch`, `retrieve`, and `get` interchangeably can be confusing as they represent the same concept.
- Choosing a single term like `getData` and using it consistently makes the code easier to understand and maintain.

## Don’t Pun

Avoid using the same term for different purposes. Using the same name for different concepts or operations can be confusing and lead to errors.

### Example in C++
#### Violation
```cpp
class DataContainer {
public:
    void add(int value) { /*...*/ }  // Adds a value to a collection
};

class Calculation {
public:
    void add(int a, int b) { /*...*/ }  // Performs addition of two numbers
};
```

### Correction
```cpp
class DataContainer {
public:
    void insert(int value) { /*...*/ }  // Adds a value to a collection
};

class Calculation {
public:
    void addNumbers(int a, int b) { /*...*/ }  // Performs addition of two numbers
};
```

### Explanation

- Using `add` for different purposes in different classes can cause confusion.
- Using distinct terms like `insert` and `addNumbers` clarifies the specific actions and improves code readability.


## Use Solution Domain Names

Utilize terminology from computer science, algorithms, patterns, or mathematical concepts when naming elements in your code. This practice makes the code more precise and understandable to other programmers.

### Example in C++

#### Violation

```cpp
class DataProcessor {
public:
    void doOperation() { /*...*/ }
};
```

#### Correction
```cpp
class Sorter {
public:
    void sortItems() { /*...*/ }
};
```

### Explanation
- `doOperation` is vague and does not specify the nature of the operation.
- `Sorter` and `sortItems` use precise CS terminology, making the purpose of the class and method clear to developers familiar with sorting algorithms.

## Use Problem Domain Names

When applicable, use terms from the problem domain instead of technical jargon. This approach ensures that names are meaningful in the context of the domain and can be understood by domain experts.

### Example in C++

#### Violation

```cpp
class ProductManager {
public:
    void createProduct() { /*...*/ }
};
```

#### Correction

```cpp
class InventoryManager {
public:
    void addProductToInventory() { /*...*/ }
};
```

### Explanation
- `ProductManager` is a general name and may not immediately convey its purpose.
- `InventoryManager` and `addProductToInventory` use domain-specific terms, making it clear that the class manages inventory-related actions.

## Add Meaningful Context

Provide context to names by enclosing them in well-named classes, functions, or namespaces. Use prefixes only if necessary to clarify the role of the variables or methods.

### Example in C++

#### Violation

```cpp
int state;  // Alone, the meaning of 'state' is unclear
```

#### Correction

```cpp
class Address {
public:
    int addrState;  // Context added by naming the class Address
};
```

### Explanation
- `state` alone does not provide enough context and can be ambiguous.
- `addrState` within the `Address` class adds meaningful context, making it clear that it pertains to the `address` structure.

## Don’t Add Gratuitous Context

Avoid adding unnecessary prefixes or context that makes names overly verbose. Instead, aim for names that are concise yet clear.

### Example in C++

#### Violation

```cpp
class GSDAccountAddress {
public:
    void update() { /*...*/ }
};
```

#### Correction

```cpp
class AccountAddress {
public:
    void update() { /*...*/ }
};
```

### Explanation

- `GSDAccountAddress` is unnecessarily verbose and adds a prefix that does not contribute meaningfully.
- `AccountAddress` is concise and directly describes the class, making it easier to read and understand.
