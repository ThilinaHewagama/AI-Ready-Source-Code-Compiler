
# AI - Ready | Source Code Compiler

This repository hosts a bash script designed to compile source code files from a specified directory into a single file. The script is useful for iOS and React Native developers who want to gather their source code for analysis, review, or other purposes without manually copying and pasting files.

## Script Overview

The script does the following:
- Identifies the directory where it is located.
- Searches for specific file types (e.g., `.swift`, `.ts`, `.tsx`) within this directory.
- Ignores specified folders (e.g., `node_modules`, `ios`, `android`, `__tests__`).
- Compiles the contents of the identified files into a single output file named `full_source_code.txt`.

## Getting Started

### Prerequisites

Ensure you have the following installed:
- Bash (commonly available on macOS and Linux)
- Necessary permissions to execute scripts in your working directory

### Installation

1. Clone this repository to your local machine:
   ```bash
   git clone https://github.com/yourusername/AI-Ready-Source-Code-Compiler.git
   cd AI-Ready-Source-Code-Compiler
   ```

2. Make the script executable:
   ```bash
   chmod +x compile_source_code.sh
   ```

### Usage

Run the script with the following command:
```bash
./compile_source_code.sh
```

This will generate a `full_source_code.txt` file in the same directory, containing all the relevant source code files concatenated together.

## Configuration

### File Types

The script searches for the following file types by default:
- `.swift` (for iOS development)
- `.ts` (TypeScript)
- `.tsx` (TypeScript with JSX)

You can modify the `file_types` array in the script to include other file types as needed.

### Ignored Folders

The script ignores the following folders by default:
- `node_modules` (common in JavaScript/TypeScript projects)
- `ios` (generated files in React Native projects)
- `android` (generated files in React Native projects)
- `__tests__` (test files)

You can modify the `ignored_folders` array in the script to ignore other directories as needed.

## Tips for iOS Developers

- **Ignored Folders**: Ensure that folders like `ios` are ignored to avoid including generated or platform-specific files.
- **File Types**: Include `.swift` files for Swift source code.

## Tips for React Native Developers

- **Ignored Folders**: Make sure to ignore `node_modules`, `ios`, `android`, and `__tests__` folders to exclude dependencies, platform-specific, and test files.
- **File Types**: Include `.ts` and `.tsx` files for TypeScript source code.

## Contributing

Contributions are welcome! Please open an issue or submit a pull request for any improvements or suggestions.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
