# Functions

Functions are the cornerstone of code organization and readability. Here are essential principles and practices to follow for effective function design:

## Keep Functions Small

Functions should be small and focused. As a rule of thumb:

- **First Rule**: Functions should be small.
- **Second Rule**: Functions should be smaller than that.

### Example

```cpp
// Bad: Large function with multiple responsibilities
void processTransaction() {
    // Code for validating transaction
    // Code for processing payment
    // Code for updating account balance
    // Code for logging transaction details
}

// Good: Small function focusing on one responsibility
void validateTransaction() {
    // Code for validating transaction
}

void processPayment() {
    // Code for processing payment
}

void updateAccountBalance() {
    // Code for updating account balance
}

void logTransactionDetails() {
    // Code for logging transaction details
}
```

## Blocks and Indenting

Blocks within control structures (e.g., `if`, `while`) should be concise, ideally consisting of a single line that calls a function. This keeps functions short and adds clarity.

### Example

```cpp
// Bad: Multiple lines of logic within an if statement
void processCustomerOrder(Customer& customer) {
    if (customer.isEligibleForDiscount()) {
        double discount = calculateDiscount(customer);
        customer.applyDiscount(discount);
        updateCustomerRecord(customer);
        sendDiscountNotification(customer);
    } else {
        updateCustomerRecord(customer);
        sendStandardNotification(customer);
    }
}

// Good: Simplified blocks using function calls
void processCustomerOrder(Customer& customer) {
    if (customer.isEligibleForDiscount()) {
        applyDiscountAndNotify(customer);
    } else {
        updateRecordAndNotify(customer);
    }
}

void applyDiscountAndNotify(Customer& customer) {
    double discount = calculateDiscount(customer);
    customer.applyDiscount(discount);
    updateCustomerRecord(customer);
    sendDiscountNotification(customer);
}

void updateRecordAndNotify(Customer& customer) {
    updateCustomerRecord(customer);
    sendStandardNotification(customer);
}
```

### Example in C++
#### Violation
```cpp
void processOrder(Order& order) {
    // Validate the order
    if (!order.isValid()) {
        throw std::invalid_argument("Invalid order");
    }

    // Calculate the total price
    double totalPrice = 0.0;
    for (const auto& item : order.getItems()) {
        totalPrice += item.getPrice();
    }

    // Apply discount if applicable
    if (order.isEligibleForDiscount()) {
        double discount = calculateDiscount(order);
        totalPrice -= discount;
    }

    // Charge the customer
    chargeCustomer(order.getCustomer(), totalPrice);

    // Send confirmation email
    sendConfirmationEmail(order.getCustomer());
}
```

#### Correction

```cpp
void processOrder(Order& order) {
    validateOrder(order);
    double totalPrice = calculateTotalPrice(order);
    applyDiscountIfEligible(order, totalPrice);
    chargeCustomer(order.getCustomer(), totalPrice);
    sendConfirmationEmail(order.getCustomer());
}

void validateOrder(const Order& order) {
    if (!order.isValid()) {
        throw std::invalid_argument("Invalid order");
    }
}

double calculateTotalPrice(const Order& order) {
    double totalPrice = 0.0;
    for (const auto& item : order.getItems()) {
        totalPrice += item.getPrice();
    }
    return totalPrice;
}

void applyDiscountIfEligible(const Order& order, double& totalPrice) {
    if (order.isEligibleForDiscount()) {
        double discount = calculateDiscount(order);
        totalPrice -= discount;
    }
}
```

### Explanation:

- Violation: The `processOrder` function is doing multiple things: validating the order, calculating the total price, applying discounts, charging the customer, and sending a confirmation email. This violates the "Do One Thing" principle, making the function harder to understand and maintain.

- Correction: The function is refactored so that `processOrder` delegates each task to a separate function. Now, each function (`validateOrder`, `calculateTotalPrice`, `applyDiscountIfEligible`, `chargeCustomer`, `sendConfirmationEmail`) does only one thing, adhering to the principle. This makes the code more modular, easier to read, and simpler to maintain.

## One Level of Abstraction per Function

Ensure that all statements within a function are at the same level of abstraction. This keeps the function focused and easier to understand.

### Example

```cpp
// Bad: Mixing levels of abstraction
void processOrder() {
    if (order.isValid()) {
        // High-level operation
        calculateTotal();
        
        // Low-level operation
        for (Item item : items) {
            processItem(item);
        }
    }
}

// Good: Single level of abstraction
void processOrder() {
    if (order.isValid()) {
        calculateTotal();
        processItems();
    }
}

void processItems() {
    for (Item item : items) {
        processItem(item);
    }
}
```

## Reading Code from Top to Bottom: The Stepdown Rule

Code should be readable as a top-down narrative. Functions should be arranged so that you read them in a logical sequence, with higher-level functions calling lower-level ones.

### Example

```cpp
// Good: Logical flow
void setup() {
    setup();
    loop();
    destroy();
}

void setup() {
    // Code to include setup
}

void loop() {
    // Code to include loop
}

void destroy() {
    // Code to include destroy
}
```

## Switch Statements

Switch statements can be complex and should be avoided **if possible**. Use polymorphism to manage multiple cases instead.

### Example

```cpp
// Bad: Complex switch statement
switch (status) {
    case PENDING:
        handlePending();
        break;
    case CLOSED:
        handleClosed();
        break;
    case CANCELED:
        handleCanceled();
        break;
}

// Good: Using polymorphism
class StatusHandler {
public:
    virtual void handle() = 0;
};

class PendingHandler : public StatusHandler {
public:
    void handle() override {
        // Handle pending
    }
};

class ClosedHandler : public StatusHandler {
public:
    void handle() override {
        // Handle closed
    }
};
```

## Use Descriptive Names

Function names should clearly indicate what the function does. A descriptive name makes the function’s purpose immediately apparent.

### Example

```cpp
// Bad: Ambiguous function name
void process();  

// Good: Descriptive function name
void processOrder();  
```

## Function Arguments

Keep the number of function arguments minimal. Prefer **zero**, **one**, or **two** arguments. Avoid more than three arguments where possible.

### Example

```cpp
// Bad: Function with multiple arguments
void drawRectangle(int x, int y, int width, int height);

// Good: Function with fewer arguments
struct Point {
    int x;
    int y;
};

struct Size {
    int width;
    int height;
}

void drawRectangle(Point topLeft, Size dimensions);
```

## Avoid Flag Arguments

Avoid using boolean flags as function arguments as they indicate the function is doing multiple things.

### Example

```cpp
// Bad: Function with flag argument
void processOrder(bool isUrgent);

// Good: Separate functions for different actions
void processOrderUrgently();
void processOrderNormally();
```

## Common Monadic Forms

There are two very common reasons to pass a single argument into a function. You may be asking a question about that argument, as in boolean `fileExists(“MyFile”)` . Or you may be operating on that argument, transforming it into something else and returning it. In both cases, you should choose names that make the distinction clear, and always use the two forms in a consistent context.

### Example in C++

1. **Monadic Form 1**: Asking a Question

    ```cpp
    bool isFileOpen(const std::string& fileName) {
        std::ifstream file(fileName);
        return file.is_open();
    }
    ```

    **Explanation**:

   - **Purpose**: This function asks a question about the argument: "Is the file open?"
   - **Naming**: The function name `isFileOpen` forms a clear verb-noun pair with the argument fileName, making the code easy to understand.

2. **Monadic Form 2:** Transforming an Argument

    ```cpp
    std::string toUpperCase(const std::string& input) {
        std::string result = input;
        std::transform(result.begin(), result.end(), result.begin(), ::toupper);
        return result;
    }
    ```

    **Explanation**:

   - **Purpose**: This function transforms the input string into an uppercase version and returns the result.
   - **Naming**: The function name `toUpperCase` clearly indicates the transformation being applied to the argument input.

## Flag Arguments

Avoid passing boolean flags. Instead, use separate functions or more descriptive names.

### Example

```cpp
// Bad: Flag argument
void setConfiguration(bool useAdvancedFeatures);

// Good: Separate functions
void enableAdvancedFeatures();
void disableAdvancedFeatures();
```

## Dyadic Functions

Functions with two arguments are acceptable but should be used carefully. Prefer making one argument a member variable if applicable.

### Example

```cpp
// Bad: Two arguments
void writeField(OutputStream outputStream, const std::string& fieldName);

// Good: Reduced argument count
void writeField(const std::string& fieldName);
```

### Triadic Functions

Functions with three arguments are harder to understand. Use with caution and consider refactoring.

### Example

```cpp
// Bad: Three arguments
void createReport(const std::string& title, const std::string& author, const std::string& content);

// Good: Using argument objects
void createReport(ReportDetails details);

struct ReportDetails {
    std::string title;
    std::string author;
    std::string content;
};
```

## Output Arguments

Avoid using output arguments. Instead, modify the state of an object or return the result directly.

### Example

```cpp
// Bad: Output argument
void processOrder(Order& order, bool& success);

// Good: Return result
bool processOrder(const Order& order);
```

## Command Query Separation

Functions should either modify state (commands) or return information (queries), but not both.

### Example

```cpp
// Bad: Mixed command and query
bool updateAndCheckStatus(Order& order);

// Good: Separate command and query
void updateOrder(Order& order);
bool checkOrderStatus(const Order& order);
```

## Prefer Exceptions to Returning Error Codes

When designing functions, it's generally better to throw exceptions when encountering errors rather than returning error codes. This approach helps avoid complex error-handling logic and makes the code cleaner and more readable.

### Violation: Returning Error Codes

```cpp
int openFile(const std::string& fileName) {
    std::ifstream file(fileName);
    if (!file.is_open()) {
        return -1;  // Error code for "file not opened"
    }
    // Process the file
    return 0;  // Success
}

int main() {
    int result = openFile("data.txt");
    if (result == -1) {
        std::cout << "Error: Could not open file." << std::endl;
        // Handle error
    } else {
        std::cout << "File opened successfully." << std::endl;
        // Continue processing
    }
    return 0;
}
```

#### Issues

- **Error Codes:** The function returns an error code (-1) to indicate failure, which requires the caller to remember to check the return value and handle errors manually.
- **Cumbersome Error Handling:** The caller (main function) has to include logic to check the return value and decide what to do next, leading to cluttered and less readable code.

### Correction: Throwing Exceptions

```cpp
void openFile(const std::string& fileName) {
    std::ifstream file(fileName);
    if (!file.is_open()) {
        throw std::runtime_error("Error: Could not open file " + fileName);
    }
    // Process the file
}

int main() {
    try {
        openFile("data.txt");
        std::cout << "File opened successfully." << std::endl;
        // Continue processing
    } catch (const std::runtime_error& e) {
        std::cerr << e.what() << std::endl;
        // Handle error (e.g., log it, retry, etc.)
    }
    return 0;
}
```

#### Corrections

- **Exceptions:** The function `openFile` throws a `std::runtime_error` exception if it cannot open the file, which avoids the need for error codes.
- **Cleaner Error Handling:** The main function handles the exception using a `try-catch` block. This approach centralizes error handling, making the code cleaner and easier to read.
- **Descriptive Error Messages:** The exception provides a detailed error message that can be logged or displayed, making it easier to diagnose issues.

## Don't Repeat Yourself (DRY)

Avoid code duplication by following the DRY (Don't Repeat Yourself) principle.

### Example

```cpp
// Bad: Duplicated logic
void processOrder() {
    // Code to validate order
    // Code to process payment
}

void processInvoice() {
    // Code to validate invoice
    // Code to process payment
}

// Good: Reuse common functionality
void validateAndProcess(Validator& validator, Processor& processor) {
    validator.validate();
    processor.process();
}
```