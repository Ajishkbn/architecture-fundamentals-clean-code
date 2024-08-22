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
