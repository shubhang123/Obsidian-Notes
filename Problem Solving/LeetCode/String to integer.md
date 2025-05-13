
```cpp
#include <iostream>
#include <string>
#include <cctype>
#include <limits>

using namespace std;

int myAtoi(const string& str) {
    int i = 0;                 // Index to track the current position in the string
    int sign = 1;             // Variable to store the sign of the number (1 for positive, -1 for negative)
    long long result = 0;     // Use long long to handle overflow during conversion

    // Skip leading whitespace characters
    while (i < str.size() && isspace(str[i])) {
        i++;
    }
    
    // Handle optional sign character
    if (i < str.size() && (str[i] == '-' || str[i] == '+')) {
        sign = (str[i] == '-') ? -1 : 1; // Set sign based on character
        i++; // Move to the next character
    }

    // Convert digits to integer
    while (i < str.size() && isdigit(str[i])) {
        result = result * 10 + (str[i] - '0'); // Build the number

        // Check for overflow and underflow conditions
        if (result * sign > numeric_limits<int>::max()) return numeric_limits<int>::max();   // Overflow
        if (result * sign < numeric_limits<int>::min()) return numeric_limits<int>::min();   // Underflow

        i++; // Move to the next character
    }

    return static_cast<int>(result * sign); // Return the final result with the correct sign
}

int main() {
    string input = "   -42"; // Example input with leading whitespace
    int output = myAtoi(input); // Call myAtoi function
    cout << output << endl; // Output: -42
    return 0;
}
```

### Key Changes and Comments:
- **Using `namespace std`**: This allows you to use standard library components without needing to prefix them with `std::`.
- **Detailed Comments**: Each section of the code now has comments explaining its purpose and functionality, making it easier to understand.
- **Variable Names**: The variable names remain unchanged as they are already descriptive. 

This should provide clarity on how the function works while maintaining good coding practices.

