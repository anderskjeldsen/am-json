# JSON Viewer Example

This example demonstrates how to use the AmLang JSON library to load, parse, and display complex JSON data structures in a formatted way.

## Features Demonstrated

- **File I/O**: Loading JSON files from disk using AmLang's `File` class
- **JSON Parsing**: Using `JsonParser` with `TextParser` to parse JSON strings into structured data
- **Type Safety**: Accessing JSON values with proper type checking
- **Nested Structures**: Handling complex nested objects and arrays
- **Pretty Printing**: Displaying JSON data with proper indentation and formatting
- **Error Handling**: Graceful handling of file and parsing errors

## Sample Data

The example uses a complex JSON file (`company-data.json`) that contains:

- **Company Information**: Basic company details
- **Nested Objects**: Headquarters with address and coordinates
- **Arrays**: Departments, projects, technologies, team members
- **Multiple Data Types**: Strings, numbers, booleans, nulls
- **Deep Nesting**: Projects within departments, coordinates within headquarters

## Building and Running

### Prerequisites

1. AmLang compiler (`amlc.jar`) in the same directory
2. AmLang core library properly set up
3. AmLang JSON library built and available

### Quick Start

```bash
# Show available commands
make help

# Build and run the example
make run

# Just build (without running)
make build

# Clean build artifacts
make clean
```

### Manual Build

```bash
# Build the project
java -jar amlc.jar build . -bt linux-x64

# Copy the data file
cp resources/company-data.json builds/bin/linux-x64/

# Run the executable
cd builds/bin/linux-x64 && ./app
```

## Expected Output

The program will display the JSON data in a structured, indented format:

```
=== AmLang JSON Viewer Example ===

Loading JSON file: company-data.json
File size: 2847 characters

Parsing completed successfully!
JSON Type: object

Object {
  "company": 
    Object {
      "name": "Tech Innovations Inc"
      "founded": 2010
      "employees": 150
      "headquarters": 
        Object {
          "address": "123 Innovation Drive"
          "city": "Silicon Valley"
          "state": "CA"
          "zipCode": "94041"
          "coordinates": 
            Object {
              "latitude": 37.4419
              "longitude": -122.1430
            }
        }
      "departments": 
        Array [
          [0]: 
            Object {
              "name": "Engineering"
              "headCount": 85
              "budget": 5000000
              "isActive": true
              "projects": 
                Array [
                  [0]: 
                    Object {
                      "name": "AmLang Compiler"
                      "status": "active"
                      "priority": "high"
                      "team": 
                        Array [
                          [0]: "Alice"
                          [1]: "Bob"
                          [2]: "Charlie"
                        ]
                      "deadline": "2025-12-31"
                    }
                  [1]: 
                    Object {
                      "name": "JSON Parser"
                      "status": "completed"
                      "priority": "medium"
                      "team": 
                        Array [
                          [0]: "David"
                          [1]: "Eve"
                        ]
                      "deadline": "2025-06-30"
                    }
                ]
            }
          [1]: 
            Object {
              "name": "Marketing"
              ...
            }
          [2]: 
            Object {
              "name": "Research"
              ...
            }
        ]
      "technologies": 
        Array [
          [0]: "C"
          [1]: "AmLang"
          [2]: "JSON"
          [3]: "Docker"
          [4]: "Linux"
        ]
      ...
    }
}
```

## Code Structure

### Main Program (`JsonViewer/Program.aml`)

- **`main()`**: Entry point that loads and parses the JSON file
- **`displayJson()`**: Recursive function that pretty-prints JSON structures
- **`displaySimpleValue()`**: Handles display of primitive JSON values
- **`getIndent()`**: Creates indentation strings for formatting

### Key AmLang JSON Library Usage

```amlang
// Required imports
import Am.IO
import Am.Json
import Am.Util.Parsers.Text

// File loading
var file = new File("company-data.json")
var jsonContent = String.readFromFile(file.toString())

// JSON parsing - NOTE: JsonParser requires a TextParser argument
var textParser = new TextParser(jsonContent)
var parser = new JsonParser(textParser)
var json = parser.parse()

// Type checking and value access
switch (json.valueType) {
    case JsonValueType.object:
        var obj = json.asObject()
        var keys = obj.getKeys()
        
    case JsonValueType.array:
        var arr = json.asArray()
        var item = arr.get(i)
        
    case JsonValueType.string:
        var text = json.asString()
        
    case JsonValueType.number:
        var num = json.asInt()  // or asLong(), asDouble(), etc.
        
    case JsonValueType.boolean:
        var flag = json.asBool()
}
```

## Customization

You can modify this example to:

1. **Load different JSON files**: Change the filename in `main()`
2. **Add filtering**: Show only specific parts of the JSON structure
3. **Add search**: Find specific keys or values in the JSON
4. **Change formatting**: Modify the indentation or display style
5. **Add validation**: Check for required fields or data types
6. **Convert formats**: Transform JSON to other formats

## Error Handling

The example includes proper error handling for:

- **File not found**: Checks if the JSON file exists before reading
- **Parse errors**: Catches exceptions during JSON parsing
- **Type errors**: Uses proper type checking before value access

## Learning Outcomes

After studying this example, you'll understand:

1. How to structure AmLang applications with proper imports and namespaces
2. File I/O operations in AmLang
3. JSON parsing and manipulation using the AmLang JSON library
4. Recursive data structure traversal
5. String formatting and output in AmLang
6. Error handling patterns
7. Switch statements and type checking
8. Building and packaging AmLang applications

This example serves as a foundation for building more complex JSON-processing applications in AmLang.