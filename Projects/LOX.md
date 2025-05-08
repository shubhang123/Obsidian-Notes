Below is an example Markdown document that explains the code in detail:

---

# Lox Scanner Documentation

This document describes the design, functionality, and structure of the Lox scanner implemented in C++. The scanner is responsible for tokenizing the input source code according to the Lox language specification. It supports single-character tokens, two-character tokens (like `==`, `!=`, etc.), string literals, comments, and error reporting with line numbers.

---

## Table of Contents

- [Overview](#overview)
- [File Structure and Entry Point](#file-structure-and-entry-point)
- [Main Components](#main-components)
  - [Helper Functions](#helper-functions)
  - [The `Scanner` Class](#the-scanner-class)
- [Tokenization Process](#tokenization-process)
- [Error Handling](#error-handling)
- [Usage](#usage)
- [Extensibility](#extensibility)

---

## Overview

The scanner reads an entire file and converts its content into tokens. A token represents a logical unit (e.g., a parenthesis, operator, identifier, or literal) and is printed to standard output in a specific format. Errors during scanning (for instance, unexpected characters or unterminated strings) are printed to standard error with line numbers. If any errors occur, the program exits with code 65; otherwise, it exits with 0.

---

## File Structure and Entry Point

The entire scanner is implemented in a single C++ source file. The entry point of the program is the `main` function, which:

1. Disables output buffering.
2. Checks the command-line arguments.
3. Reads the input file content.
4. Invokes the tokenization process.
5. Exits with the appropriate code based on whether any lexical errors were encountered.

---

## Main Components

### Helper Functions

#### `readFileContents`

```cpp
std::string readFileContents(const std::string &filename);
```

- **Purpose:**  
  Reads the entire contents of the specified file and returns it as a single `std::string`.
  
- **Behavior:**  
  If the file cannot be opened, it prints an error message to `stderr` and exits the program.

#### `printUsageAndExit`

```cpp
void printUsageAndExit(const std::string &programName);
```

- **Purpose:**  
  Prints the correct usage of the program to `stderr` and exits.
  
- **Usage:**  
  Called when the command-line arguments are insufficient or incorrect.

#### Overloaded `addToken` Functions

```cpp
void addToken(const std::string &type, const std::string &lexeme);
void addToken(const std::string &type, const std::string &lexeme, const std::string &literal);
```

- **Purpose:**  
  Print tokens to `stdout` in a specific format.
  
- **Parameters:**
  - `type`: The token type (e.g., `"LEFT_PAREN"`, `"STRING"`).
  - `lexeme`: The actual text from the source code, which may include surrounding characters (like quotes for strings).
  - `literal`: (Optional) The literal value of the token (for example, the inner content of a string).

---

### The `Scanner` Class

The `Scanner` class encapsulates the tokenization logic and maintains state during the scan.

#### Class Declaration

```cpp
class Scanner {
public:
    Scanner(const std::string &source);
    bool scanTokens();
    
private:
    // Source code and scanning state.
    const std::string source;
    int start;     // Start of the current lexeme.
    int current;   // Current position in the source.
    int line;      // Current line number.
    bool hadError; // Tracks if any error has occurred.
    
    // Utility methods.
    bool isAtEnd() const;
    char advance();
    char peek() const;
    bool match(char expected);
    
    // Token scanning methods.
    void scanToken();
    void scanString();
    
    // Methods for emitting tokens.
    void addToken(const std::string &type, const std::string &lexeme);
    void addToken(const std::string &type, const std::string &lexeme, const std::string &literal);
};
```

#### Key Methods

- **Constructor:**  
  Initializes the scanner with the input source and sets the starting state (e.g., `line = 1`).

- **`scanTokens`:**  
  Main method that repeatedly calls `scanToken()` until the end of the source is reached. At the end, an EOF token is emitted. Returns `true` if any lexical errors occurred.

- **Utility Methods:**
  - `isAtEnd()`: Checks if the current position is at or past the end of the source.
  - `advance()`: Consumes and returns the current character, incrementing the current position.
  - `peek()`: Returns the current character without consuming it.
  - `match(char expected)`: Checks if the next character matches the expected one and consumes it if it does.

- **`scanToken`:**  
  Processes a single character and determines the appropriate action:
  - **Single-character tokens:** Directly adds tokens (e.g., `(`, `)`, `{`, `}`).
  - **Two-character tokens:** Uses `match` to check and process operators like `==`, `!=`, `<=`, `>=`.
  - **Comments:** When encountering `/`, checks for a second `/` and skips characters until the end of the line.
  - **String literals:** Calls `scanString` to collect all characters until the closing quote.

- **`scanString`:**  
  Collects characters until a closing quote (`"`) is encountered. If a newline is found within the string, the line counter is incremented. If the end of input is reached without a closing quote, an error is reported.

- **Token Emission:**  
  The methods `addToken` inside the class output tokens in the required format. Overloaded versions allow for tokens with and without literal values.

---

## Tokenization Process

1. **Initialization:**  
   The scanner is instantiated with the source code. Initial state variables (`start`, `current`, `line`) are set.

2. **Scanning Loop:**  
   The scanner loops over each character using `scanToken()`, which:
   - Advances the current position.
   - Checks the character and categorizes it (e.g., operator, punctuation, string literal).
   - Handles multi-character tokens using the `match` utility.
   - Increases the line counter for newline characters.
   - Skips comments (i.e., ignores characters following `//` until a newline).

3. **EOF Token:**  
   After all characters are processed, an EOF token is emitted.

4. **Error Reporting:**  
   Any unexpected character is reported with its line number in the format `[line N] Error: Unexpected character: <char>`. If any errors occur, the scanner returns `true` so the program exits with code 65.

---

## Error Handling

- **Lexical Errors:**  
  When encountering an unexpected character or an unterminated string, an error message is printed to `stderr` with the current line number.

- **Exit Codes:**  
  - `65`: Returned if any lexical errors are encountered.
  - `0`: Returned if tokenization completes without errors.

---

## Usage

To run the scanner, compile the C++ code and run it with the following command-line arguments:

```bash
./your_program tokenize <filename>
```

- **Example:**

  If `test.lox` contains:
  ```lox
  ()// This is a comment
  ```
  The expected output to `stdout` might be:
  ```
  LEFT_PAREN ( null
  RIGHT_PAREN ) null
  EOF  null
  ```
  And any errors (if present) will be printed to `stderr` with line numbers.

---

## Extensibility

The code is organized for maintainability and can be extended as follows:
- **Adding New Token Types:**  
  Extend the `scanToken()` method with additional cases as required.
- **Multi-line Comments:**  
  Update the comment-handling logic to support multi-line block comments if needed.
- **Error Recovery:**  
  Enhance error handling to allow recovery and continue scanning after errors.

---

## Conclusion

This scanner is designed to be modular, well-factored, and easily extendable. By encapsulating scanning logic within the `Scanner` class and using helper functions, the code remains clean and maintainable. The documentation provided here should help understand the design decisions and how the code flows from reading the file to producing tokens and handling errors.

--- 

*End of Documentation*