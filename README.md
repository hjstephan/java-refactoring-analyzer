# Java Refactoring Analyzer

A powerful Visual Studio Code extension that analyzes Java code structure in real-time, helping you write cleaner, more maintainable code by maximizing class separation and minimizing method length.

## Features

### Real-time Inline Metrics
- **LOC Display**: Shows lines of code next to every method declaration
- **Method Count**: Displays the number of methods next to every class declaration
- **Color-coded Warnings**: Instantly see which methods need refactoring
  - 🟢 Green: ≤10 LOC (excellent)
  - 🟡 Yellow: 11-20 LOC (warning)
  - 🔴 Red: >20 LOC (needs refactoring)

### Comprehensive Analysis Dashboard
- **Refactoring Quality Score**: Get an overall score (0-100) for your code structure
- **Detailed Metrics**: View total classes, methods, LOC, and averages
- **Top Offenders**: See the longest methods and largest classes at a glance
- **Actionable Recommendations**: Get specific suggestions for improving your code

### Goals
This extension promotes two key refactoring principles:
1. **Maximize Classes**: Encourages proper separation of concerns
2. **Minimize LOC/Method**: Promotes small, focused methods (target: <10 LOC)

## Getting Started

### Installation

1. Open Visual Studio Code
2. Press `Ctrl+P` / `Cmd+P` to open Quick Open
3. Type `ext install java-refactoring-analyzer`
4. Press Enter

### Usage

#### Real-time Analysis
Simply open any Java file, and the extension will automatically display metrics inline:
- Method LOC appears at the end of each method declaration
- Method count appears at the end of each class declaration

#### Full Analysis Report
- Press `Ctrl+Alt+R` / `Cmd+Alt+R` (or use Command Palette: "Analyze Java Refactoring Metrics")
- A detailed analysis panel will open showing:
  - Refactoring quality score
  - All metrics and statistics
  - Prioritized recommendations
  - Methods and classes sorted by size

#### Toggle Decorations
- Use Command Palette: "Toggle Real-time Decorations"
- Turns inline metrics on/off

## Extension Settings

This extension contributes the following settings:

* `javaRefactoringAnalyzer.enableRealTimeDecorations`: Enable/disable real-time inline decorations (default: `true`)
* `javaRefactoringAnalyzer.methodLocThreshold`: LOC threshold for method warnings (default: `10`)
* `javaRefactoringAnalyzer.classMethodThreshold`: Method count threshold for class warnings (default: `10`)

### Example Configuration

```json
{
  "javaRefactoringAnalyzer.enableRealTimeDecorations": true,
  "javaRefactoringAnalyzer.methodLocThreshold": 15,
  "javaRefactoringAnalyzer.classMethodThreshold": 8
}
```

## Commands

| Command | Keyboard Shortcut | Description |
|---------|------------------|-------------|
| Analyze Java Refactoring Metrics | `Ctrl+Alt+R` / `Cmd+Alt+R` | Opens the full analysis dashboard |
| Toggle Real-time Decorations | - | Enables/disables inline metrics |

## How It Works

The extension uses the `java-parser` library to build an Abstract Syntax Tree (AST) from your Java code. It then:

1. Identifies all classes, interfaces, and enums
2. Counts methods in each class
3. Calculates lines of code for each method body
4. Compares metrics against configurable thresholds
5. Displays warnings and recommendations

### What Gets Counted as LOC?
- Only non-empty lines within method bodies
- Comments and whitespace are excluded
- Only the method body is counted, not the signature

## Refactoring Tips

### Extract Method
When a method exceeds 20 lines:
```java
// Before (25 LOC)
public void processOrder(Order order) {
    // 25 lines of code...
}

// After (multiple small methods)
public void processOrder(Order order) {
    validateOrder(order);
    calculateTotal(order);
    applyDiscounts(order);
    saveOrder(order);
}
```

### Extract Class
When a class has more than 10 methods:
```java
// Before: OrderService with 15 methods
public class OrderService {
    // Order validation methods
    // Order calculation methods
    // Order persistence methods
    // Notification methods
}

// After: Split into focused classes
public class OrderValidator { ... }
public class OrderCalculator { ... }
public class OrderRepository { ... }
public class OrderNotifier { ... }
```

## Requirements

- Visual Studio Code version 1.85.0 or higher
- Java files (`.java` extension)

## Known Issues

- The parser may have difficulty with very complex generic type declarations
- Anonymous inner classes are counted but may not always display decorations correctly

## Release Notes

### Initial Release v0.0.1
- Real-time inline LOC display for methods
- Real-time method count display for classes
- Comprehensive analysis dashboard
- Configurable thresholds
- Color-coded warnings

### Quality v1.0.2
- Tests and coverage report
- Refactoring into modules

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## Acknowledgments

- Built with [java-parser](https://www.npmjs.com/package/java-parser)
- Inspired by clean code principles from Robert C. Martin's "Clean Code"
- Icon design: [Your icon attribution if applicable]

## Support

If you encounter any issues or have suggestions:
- Open an issue on [GitHub](https://github.com/hjstephan/refactorings/issues)
- Contact: hjstephan86@gmail.com

---

**Enjoy cleaner, more maintainable Java code!** 
