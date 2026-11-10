# Java Source Code Metrics Tool

A console application for examining Java source through abstract syntax trees and token-level measurements. The project connects compiler tooling to software-maintenance metrics, exposing how source structure becomes quantitative information.

## Measurements

- **Cyclomatic complexity:** increments a method-level counter for selected decision and loop constructs.
- **Line metrics:** reports total lines, physical code lines, logical statements, whitespace lines, and comment lines.
- **Halstead metrics:** derives vocabulary, volume, difficulty, and effort from operator and operand counts.
- **Method discovery:** prints method names while traversing the compilation unit.

## Architecture

```text
Java source → Eclipse JDT ASTParser → AST visitors → Complexity and line metrics
     |
     └────────────────────────────→ Halstead operator/operand analysis
```

[Operation.java](src/othersPackage/Operation.java) configures Eclipse JDT's parser, walks declarations and statements, counts comments, and prints results. [Halstead.java](src/othersPackage/Halstead.java) implements the operator/operand analysis and derived formulas. `mainPackage.MainClass` coordinates execution.

The bundled sample, [Saal.java](src/sourcePackage/Saal.java), is the input selected by the driver.

## Run

Use a Java IDE with a JDK and Eclipse JDT Core plus its Eclipse runtime dependencies on the classpath. Mark `src/` as the source root and launch `mainPackage.MainClass` from the repository root. The tool reads `src/sourcePackage/Saal.java` and prints the measurement sections to the console.

Inspect the visitors in `Operation` to see how `if`, loops, switch cases, statements, and comments contribute to their respective measures. The parser uses the `AST.JLS3` configuration recorded in the implementation.

## Engineering focus

AST visitor design, source-position-based comment accounting, per-method traversal, and direct implementation of Halstead formulas demonstrate practical static-analysis techniques for software measurement.
