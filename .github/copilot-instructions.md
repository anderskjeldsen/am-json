# AmLang JSON Library (am-json)

This repository contains the JSON parsing and manipulation library for the AmLang programming language ecosystem. AmLang is a modern object-oriented programming language designed for systems programming with cross-platform compatibility, particularly targeting niche platforms like AmigaOS, MorphOS, and legacy systems.

## Repository Overview

**am-json** provides comprehensive JSON parsing, generation, and manipulation capabilities for AmLang applications. The library is designed to work seamlessly across all AmLang-supported platforms while maintaining high performance and low memory usage.

### Key Features

- **Complete JSON Parsing**: Parse JSON strings into structured AmLang objects
- **Type-Safe API**: Strong typing with `JsonValue`, `JsonObject`, `JsonArray` classes
- **Text Parser Integration**: Uses AmLang's `TextParser` for efficient string processing
- **Cross-Platform**: Works on all AmLang target platforms (Linux, macOS, AmigaOS, MorphOS, etc.)
- **Memory Efficient**: Designed for embedded and resource-constrained environments
- **Error Handling**: Comprehensive exception handling for malformed JSON

### Core Classes

- **`JsonParser`**: Main parser class for converting JSON strings to objects
- **`JsonValue`**: Base class for all JSON values with type checking
- **`JsonObject`**: Represents JSON objects with key-value pairs
- **`JsonArray`**: Represents JSON arrays with indexed access
- **`JsonValueType`**: Enumeration of JSON value types

## API Usage Patterns

### Basic JSON Parsing

```amlang
import Am.Json
import Am.Util.Parsers.Text

// IMPORTANT: JsonParser requires a TextParser argument
var jsonContent = "{\"name\":\"John\",\"age\":30}"
var textParser = new TextParser(jsonContent)
var jsonParser = new JsonParser(textParser)
var jsonRoot = jsonParser.parse()

// Type-safe access
if (jsonRoot.isObject()) {
    var obj = jsonRoot.asObject()
    var name = obj.getString("name")
    var age = obj.getInt("age")
}
```

### Working with Arrays

```amlang
var jsonArray = "[\"apple\",\"banana\",\"cherry\"]"
var textParser = new TextParser(jsonArray)
var parser = new JsonParser(textParser)
var array = parser.parse().asArray()

for (i = 0 to array.size()) {
    var item = array.getString(i)
    item.println()
}
```

### Type Checking and Safety

```amlang
var value = jsonObject.getValue("someKey")
switch (value.getType()) {
    case JsonValueType.stringType:
        var text = value.asString()
    case JsonValueType.numberType:
        var number = value.asInt()
    case JsonValueType.boolType:
        var flag = value.asBool()
    case JsonValueType.objectType:
        var nestedObj = value.asObject()
    case JsonValueType.arrayType:
        var nestedArray = value.asArray()
    case JsonValueType.nullType:
        // Handle null value
}
```

## Project Structure

```
src/am-lang/Am/Json/
├── JsonParser.aml          # Main JSON parser
├── JsonValue.aml           # Base value class
├── JsonObject.aml          # JSON object implementation
├── JsonArray.aml           # JSON array implementation
├── JsonValueType.aml       # Type enumeration
└── JsonTextParser.aml      # Text parsing utilities

tests/
├── JsonParserTest.aml      # Basic parsing tests
├── JsonTest.aml            # Value manipulation tests
├── Am/Json/Tests/          # Comprehensive test suite
│   ├── JsonNumberTest.aml  # Number parsing tests
│   ├── JsonFileParseTest.aml # File loading tests
│   └── ...

examples/
└── json-viewer/            # Complete JSON viewing application
    ├── src/am-lang/JsonViewer/Program.aml
    ├── resources/company-data.json
    └── README.md
```

## Building and Testing

### Prerequisites

- AmLang compiler (`amlc`) v0.6.4 or later
- AmLang core library (`am-lang-core`) as dependency
- `TextParser` from `Am.Util.Parsers.Text` namespace

### Build Commands

```bash
# Build the library
make build

# Run all tests
make test

# Run tests with detailed output
make test-rl

# Clean build artifacts
make clean
```

### Manual Build

```bash
# Build library
java -jar amlc.jar build . -bt linux-x64

# Run tests
java -jar amlc.jar test . -bt linux-x64
```

## Development Guidelines

### Critical API Requirements

1. **JsonParser Constructor**: ALWAYS requires a `TextParser` argument
   ```amlang
   // CORRECT:
   var textParser = new TextParser(jsonString)
   var parser = new JsonParser(textParser)
   
   // WRONG:
   var parser = new JsonParser()  // Missing TextParser argument
   ```

2. **Import Requirements**: Always include required imports
   ```amlang
   import Am.Json                    // Core JSON classes
   import Am.Util.Parsers.Text      // TextParser class
   import Am.Lang                   // Basic language features
   ```

3. **Type Safety**: Always check types before casting
   ```amlang
   if (value.isObject()) {
       var obj = value.asObject()
   }
   ```

### Error Handling Patterns

```amlang
try {
    var parser = new JsonParser(textParser)
    var json = parser.parse()
    // Process JSON...
} catch (e: Exception) {
    "JSON parsing failed: ${e.message}".println()
}
```

### Testing Best Practices

- Test with various JSON structures (objects, arrays, nested data)
- Test edge cases (empty objects, null values, malformed JSON)
- Verify proper exception handling for invalid JSON
- Test cross-platform compatibility

## Platform Support

| Platform | Status | Notes |
|----------|---------|-------|
| Linux x64 | ✅ Full | Primary development platform |
| Linux ARM64 | ✅ Full | Raspberry Pi and ARM servers |
| macOS x64 | ✅ Full | Intel Macs |
| macOS ARM64 | ✅ Full | Apple Silicon Macs |
| AmigaOS 68k | ✅ Full | Via Docker cross-compilation |
| MorphOS PPC | ✅ Full | Via Docker cross-compilation |
| AROS x86-64 | ✅ Full | Via Docker cross-compilation |
| Windows x64 | 🚧 Partial | Core library support pending |

## Dependencies

- **am-lang-core**: Core AmLang standard library
  - `Am.Lang.*`: Basic types and functionality
  - `Am.Util.Parsers.Text.TextParser`: String parsing utilities
  - `Am.IO.*`: File operations (for file-based JSON loading)

## Common Issues and Solutions

### JsonParser Constructor Error
**Problem**: "JsonParser constructor requires arguments"
**Solution**: Pass a `TextParser` instance to the constructor

### TextParser Import Missing
**Problem**: "TextParser not found"
**Solution**: Add `import Am.Util.Parsers.Text`

### Type Casting Errors
**Problem**: Runtime errors when accessing wrong value types
**Solution**: Always use type checking (`isObject()`, `isArray()`, etc.) before casting

### Memory Issues on Embedded Platforms
**Problem**: High memory usage with large JSON files
**Solution**: Process JSON in chunks or use streaming approaches for very large files

## Examples and Learning Resources

1. **json-viewer Example**: Complete application showing file loading, parsing, and pretty-printing
2. **Test Suite**: Comprehensive examples in `tests/` directory
3. **API Documentation**: Inline documentation in source files

## Contributing Guidelines

1. **Maintain API Consistency**: Follow existing patterns for method naming and signatures
2. **Cross-Platform Compatibility**: Test on multiple platforms when possible
3. **Comprehensive Testing**: Add tests for any new functionality
4. **Documentation**: Update examples and documentation for API changes
5. **Performance**: Consider memory usage on embedded/legacy platforms

## Version Compatibility

- **AmLang Compiler**: Requires v0.6.3+ for proper JSON functionality
- **am-lang-core**: Must be compatible version with matching ABI
- **Backwards Compatibility**: Maintained within major versions

---

This library is part of the AmLang ecosystem. For broader context and cross-repository development, see the main AmLang workspace documentation.