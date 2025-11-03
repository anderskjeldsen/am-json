# AmLang JSON Viewer Example
# Demonstrates parsing and displaying complex JSON structures

# AmLang compiler
AMLC := java -jar amlc.jar
TARGET := linux-x64

.PHONY: build run clean help

help:
	@echo "AmLang JSON Viewer Example"
	@echo "=========================="
	@echo ""
	@echo "Available targets:"
	@echo "  build   - Compile the JSON viewer example"
	@echo "  run     - Build and run the example"
	@echo "  clean   - Clean build artifacts"
	@echo "  help    - Show this help message"
	@echo ""
	@echo "This example demonstrates:"
	@echo "  - Loading JSON files from disk"
	@echo "  - Parsing complex nested JSON structures"
	@echo "  - Traversing JSON objects and arrays"
	@echo "  - Pretty-printing JSON data with indentation"
	@echo "  - Type-safe JSON value access"

build:
	@echo "Building JSON Viewer example..."
	$(AMLC) build . -bt $(TARGET) -maxOneError -ll 5 -rdc
	@echo "Copying JSON data file to binary directory..."
	@cp resources/company-data.json builds/bin/$(TARGET)/
	@echo "Build complete!"	

run: build
	@echo "Running JSON Viewer example..."
	@echo "==============================="
	@cd builds/bin/$(TARGET) && ./app

clean:
	@echo "Cleaning build artifacts..."
	@rm -rf builds/
	@echo "Clean complete!"

# Development helpers
debug: build
	@echo "Running with debug information..."
	@cd builds/bin/$(TARGET) && gdb ./app

test-json:
	@echo "Testing JSON file validity..."
	@python3 -m json.tool resources/company-data.json > /dev/null && echo "JSON file is valid!" || echo "JSON file has syntax errors!"

.DEFAULT_GOAL := help