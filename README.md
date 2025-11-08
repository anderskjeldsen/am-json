# Am-JSON

A comprehensive JSON parsing and serialization library for AmLang, providing robust support for JSON data manipulation with full type safety and cross-platform compatibility.

## Features

- **Full JSON Support**: Parse and serialize complete JSON documents including objects, arrays, strings, numbers, booleans, and null values
- **Type-Safe API**: Strongly typed methods for all JSON operations with compile-time type checking
- **Cross-Platform**: Works on all AmLang-supported platforms (Linux, macOS, Windows, AmigaOS, etc.)
- **Memory Safe**: Automatic reference counting with no memory leaks
- **Comprehensive Type Support**: Built-in support for all AmLang primitive types including integers, floating-point numbers, strings, and booleans
- **Flexible Parsing**: Robust JSON parser that handles whitespace, escaping, and edge cases correctly
- **Easy Serialization**: Simple API to convert AmLang objects to JSON strings

## Installation

Add am-json as a dependency in your `package.yml`:

```yaml
dependencies:
  - id: am-json
    realm: github
    type: git-repo
    tag: latest
    url: https://github.com/anderskjeldsen/am-json.git
```

## Quick Start

### Parsing JSON

```amlang
import Am.Json
import Am.Util.Parsers.Text

// Parse a JSON string
var jsonText = """{"name": "John", "age": 30, "active": true}"""
var parser = TextParser(jsonText)
var jsonParser = JsonParser(parser)
var result = jsonParser.parse()

// Access the parsed JSON object
var jsonObj = result.asObject()
var name = jsonObj.getString("name")        // "John"
var age = jsonObj.getInt("age")            // 30
var isActive = jsonObj.getBool("active")   // true
```

### Creating JSON Objects

```amlang
import Am.Json

// Create a new JSON object
var person = JsonObject()
person.putString("name", "Jane Doe")
person.putInt("age", 25)
person.putBool("active", true)

// Create nested objects
var address = JsonObject()
address.putString("street", "123 Main St")
address.putString("city", "Springfield")
person.putObject("address", address)

// Convert to JSON string
var jsonString = person.toString()
```

### Working with JSON Arrays

```amlang
import Am.Json

// Create a JSON array
var numbers = JsonArray()
numbers.addInt(1)
numbers.addInt(2)
numbers.addInt(3)

// Create array of objects
var people = JsonArray()
var person1 = JsonObject()
person1.putString("name", "Alice")
person1.putInt("age", 28)
people.addObject(person1)

var person2 = JsonObject()
person2.putString("name", "Bob")
person2.putInt("age", 32)
people.addObject(person2)

// Access array elements
var firstPerson = people.getObject(0)
var firstName = firstPerson.getString("name") // "Alice"
```

## API Reference

### JsonValue

The core class representing any JSON value.

**Types:**
- `JsonValueType.stringType` - JSON string
- `JsonValueType.numberType` - JSON number
- `JsonValueType.boolType` - JSON boolean
- `JsonValueType.nullType` - JSON null
- `JsonValueType.objectType` - JSON object
- `JsonValueType.arrayType` - JSON array

**Factory Methods:**
```amlang
JsonValue.fromString(value: String): JsonValue
JsonValue.fromInteger(value: Int): JsonValue
JsonValue.fromLong(value: Long): JsonValue
JsonValue.fromByte(value: Byte): JsonValue
JsonValue.fromShort(value: Short): JsonValue
JsonValue.fromUInt(value: UInt): JsonValue
JsonValue.fromULong(value: ULong): JsonValue
JsonValue.fromUShort(value: UShort): JsonValue
JsonValue.fromUByte(value: UByte): JsonValue
JsonValue.fromBool(value: Bool): JsonValue
JsonValue.fromObject(value: JsonObject): JsonValue
JsonValue.fromArray(value: JsonArray): JsonValue
JsonValue.createNull(): JsonValue
```

**Accessor Methods:**
```amlang
asString(): String
asInt(): Int
asLong(): Long
asBool(): Bool
asObject(): JsonObject
asArray(): JsonArray
```

**Type Checking:**
```amlang
isString(): Bool
isNumber(): Bool
isBool(): Bool
isNull(): Bool
isObject(): Bool
isArray(): Bool
```

### JsonObject

Represents a JSON object (key-value pairs).

**Put Methods:**
```amlang
putString(key: String, value: String)
putInt(key: String, value: Int)
putLong(key: String, value: Long)
putByte(key: String, value: Byte)
putShort(key: String, value: Short)
putUInt(key: String, value: UInt)
putULong(key: String, value: ULong)
putUShort(key: String, value: UShort)
putUByte(key: String, value: UByte)
putBool(key: String, value: Bool)
putObject(key: String, value: JsonObject)
putArray(key: String, value: JsonArray)
putNull(key: String)
```

**Get Methods:**
```amlang
getString(key: String): String
getInt(key: String): Int
getLong(key: String): Long
getByte(key: String): Byte
getShort(key: String): Short
getUInt(key: String): UInt
getULong(key: String): ULong
getUShort(key: String): UShort
getUByte(key: String): UByte
getBool(key: String): Bool
getObject(key: String): JsonObject
getArray(key: String): JsonArray
```

**Utility Methods:**
```amlang
has(key: String): Bool
remove(key: String)
getKeys(): List<String>
toString(): String
```

### JsonArray

Represents a JSON array (ordered list of values).

**Add Methods:**
```amlang
addString(value: String)
addInt(value: Int)
addLong(value: Long)
addByte(value: Byte)
addShort(value: Short)
addUInt(value: UInt)
addULong(value: ULong)
addUShort(value: UShort)
addUByte(value: UByte)
addBool(value: Bool)
addObject(value: JsonObject)
addArray(value: JsonArray)
addNull()
```

**Get Methods:**
```amlang
getString(index: Int): String
getInt(index: Int): Int
getLong(index: Int): Long
getByte(index: Int): Byte
getShort(index: Int): Short
getUInt(index: Int): UInt
getULong(index: Int): ULong
getUShort(index: Int): UShort
getUByte(index: Int): UByte
getBool(index: Int): Bool
getObject(index: Int): JsonObject
getArray(index: Int): JsonArray
```

**Utility Methods:**
```amlang
size(): Int
remove(index: Int)
toString(): String
```

### JsonParser

Parses JSON text into JsonValue objects.

```amlang
JsonParser(parser: TextParser)
parse(): JsonValue
```

## Examples

### Complex JSON Document

```amlang
import Am.Json
import Am.Util.Parsers.Text

// Parse complex JSON
var complexJson = """{
    "users": [
        {
            "id": 1,
            "name": "Alice Johnson",
            "email": "alice@example.com",
            "settings": {
                "theme": "dark",
                "notifications": true,
                "language": "en-US"
            }
        },
        {
            "id": 2,
            "name": "Bob Smith", 
            "email": "bob@example.com",
            "settings": {
                "theme": "light",
                "notifications": false,
                "language": "fr-FR"
            }
        }
    ],
    "meta": {
        "version": "1.0",
        "updated": "2024-01-15T10:30:00Z"
    }
}"""

var parser = TextParser(complexJson)
var jsonParser = JsonParser(parser)
var document = jsonParser.parse().asObject()

// Navigate the structure
var users = document.getArray("users")
var firstUser = users.getObject(0)
var userName = firstUser.getString("name")
var userSettings = firstUser.getObject("settings")
var theme = userSettings.getString("theme")
```

### Building JSON Programmatically

```amlang
import Am.Json

// Create the same structure programmatically
var document = JsonObject()

// Add users array
var users = JsonArray()

// First user
var user1 = JsonObject()
user1.putInt("id", 1)
user1.putString("name", "Alice Johnson")
user1.putString("email", "alice@example.com")

var settings1 = JsonObject()
settings1.putString("theme", "dark")
settings1.putBool("notifications", true)
settings1.putString("language", "en-US")
user1.putObject("settings", settings1)

users.addObject(user1)

// Second user
var user2 = JsonObject()
user2.putInt("id", 2)
user2.putString("name", "Bob Smith")
user2.putString("email", "bob@example.com")

var settings2 = JsonObject()
settings2.putString("theme", "light")
settings2.putBool("notifications", false)
settings2.putString("language", "fr-FR")
user2.putObject("settings", settings2)

users.addObject(user2)

document.putArray("users", users)

// Add metadata
var meta = JsonObject()
meta.putString("version", "1.0")
meta.putString("updated", "2024-01-15T10:30:00Z")
document.putObject("meta", meta)

// Convert to JSON string
var jsonOutput = document.toString()
```

## Testing

Run the test suite:

```bash
amlc test
```

The library includes comprehensive tests covering:
- JSON parsing edge cases
- Type conversion accuracy
- Error handling
- Complex nested structures
- String escaping and Unicode support

## Cross-Platform Support

Am-JSON works seamlessly across all AmLang-supported platforms:

- **Linux** (x64, ARM64)
- **macOS** (Intel, Apple Silicon)  
- **Windows**
- **AmigaOS**
- **MorphOS**
- **AROS**

## Dependencies

- **am-lang-core**: Core AmLang runtime and standard library
- **am-tests** (test-only): Testing framework

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Add tests for your changes
4. Ensure all tests pass (`amlc test`)
5. Commit your changes (`git commit -m 'Add amazing feature'`)
6. Push to the branch (`git push origin feature/amazing-feature`)
7. Open a Pull Request

## License

This project is part of the AmLang ecosystem. See the LICENSE file for details.

## Related Projects

- [am-lang-core](https://github.com/anderskjeldsen/am-lang-core) - Core AmLang runtime
- [am-lang-compiler](https://github.com/anderskjeldsen/am-lang-compiler) - AmLang compiler
- [am-ui](https://github.com/anderskjeldsen/am-ui) - UI framework for AmLang
- [am-net](https://github.com/anderskjeldsen/am-net) - Networking library for AmLang