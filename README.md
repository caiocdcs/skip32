# Skip32 for Zig

A pure Zig implementation of the Skip32 algorithm - a 32-bit block cipher for obfuscating sequential numbers.

## What is Skip32?

Skip32 transforms sequential numbers (like database IDs) into seemingly random values while maintaining perfect 1:1 mapping. Ideal for hiding predictable ID patterns in URLs and APIs.

⚠️ **Note**: Skip32 is for obfuscation, not cryptographic security.

## Getting Started

### 1. Add Dependency

Add dependency:

```bash
.zig fetch https://github.com/caiocdcs/skip32/archive/v0.0.1.tar.gz --save
```

### 2. Configure Build

In your `build.zig`:

```zig
const skip32 = b.dependency("skip32", .{
    .target = target,
    .optimize = optimize,
});

exe.root_module.addImport("skip32", skip32.module("skip32"));
```

### 3. Fetch Dependencies

```bash
zig build --fetch
```

## Usage

```zig
const skip32 = @import("skip32");

const key = [_]u8{ 0x01, 0x02, 0x03, 0x04, 0x05, 0x06, 0x07, 0x08, 0x09, 0x0A };

const encoded = skip32.encode(&key, 12345);  // Returns obfuscated number
const decoded = skip32.decode(&key, encoded); // Returns 12345
```

## API

- `encode(key: *const [10]u8, value: u32) u32` - Encode a value
- `decode(key: *const [10]u8, value: u32) u32` - Decode a value

Key must be exactly 10 bytes. Encoding/decoding is perfectly reversible.

## Example Use Cases

- Hide sequential database IDs in URLs
- Obfuscate user IDs in APIs
- Generate non-predictable order numbers
- Create hard-to-guess tokens (with proper key management)

## Testing

```bash
zig test src/root.zig
```

## License

MIT
