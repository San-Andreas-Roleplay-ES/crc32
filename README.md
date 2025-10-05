# SA-MP CRC32 Hash Calculator

A CRC32 hash calculator specifically for SA-MP 0.3DL files that computes checksums compatible with the algorithm used by San Andreas Multiplayer.

## 📋 Description

This project implements the SA-MP specific CRC32 algorithm to calculate hashes of `.dff` and `.txd` files used in SA-MP 0.3DL servers. The algorithm exactly replicates the `GetFileCRC32Checksum` function from the SA-MP source code.

### What does it do?

- 🔍 Calculates CRC32 hashes compatible with SA-MP 0.3DL
- 📁 Processes `.dff` (3D models) and `.txd` (textures) files
- ✅ Verifies that files match expected hashes
- 🔄 Reads files in 1024-byte chunks (same as SA-MP)

## 🚀 Installation

### Prerequisites

- Node.js (version 16 or higher)
- Yarn package manager

### Initial Setup

```bash
# Clone the repository
git clone https://github.com/San-Andreas-Roleplay-ES/crc32.git
cd crc32

# Install dependencies
yarn install

# Compile TypeScript
yarn build
```

## 📦 Available Commands

```bash
# Install dependencies
yarn install

# Compile the TypeScript project
yarn build

# Run the project (after compiling)
yarn start

# Run in development mode (ts-node)
yarn dev

# Clean compiled files
yarn clean
```

## 📁 Project Structure

```
crc32/
├── src/
│   └── index.ts          # Main code with CRC32 algorithm
├── assets/               # Test files (.dff, .txd)
│   ├── cesar.dff
│   ├── cesar.txd
│   ├── fam1.dff
│   ├── fam1.txd
│   ├── wmyammo.dff
│   └── wmyammo.txd
├── package.json
├── tsconfig.json
└── README.md
```

## 🔧 Usage

### Verify existing files

The script automatically verifies all files in the `assets/` folder and compares their CRC32 hashes with expected values:

```bash
yarn start
```

Expected output:

```
✅ cesar.dff OK: expected 2F363354, got 2F363354
✅ cesar.txd OK: expected 4BCE378B, got 4BCE378B
✅ fam1.dff OK: expected 2CB8FD7E, got 2CB8FD7E
✅ fam1.txd OK: expected 4E76581E, got 4E76581E
✅ wmyammo.dff OK: expected 8EC07DC0, got 8EC07DC0
✅ wmyammo.txd OK: expected 27B61A89, got 27B61A89

✅ All hashes match!
```

### Use as module

```typescript
import { getSAMPCRC32 } from "./src/index";

// Calculate CRC32 of a file
const hash = await getSAMPCRC32("./assets/example.dff");
console.log(`CRC32 Hash: ${hash}`);
```

## 🔬 Algorithm

The project implements the exact SA-MP CRC32 algorithm:

```typescript
// Based on the original SA-MP C++ code:
// Source: https://github.com/openmultiplayer/open.mp/blob/master/Server/Components/CustomModels/crc32.hpp
static uint32_t CRC32(uint32_t checksum, uint8_t* buffer, int length)
{
    checksum = ~checksum;
    while (length--)
    {
        checksum = crc32Table[(checksum ^ *buffer++) & 0xff] ^ (checksum >> 8);
    }
    return ~checksum;
}
```

### Key Features:

- ✅ Uses the standard CRC32 table
- ✅ Processes files in 1024-byte chunks
- ✅ Correctly handles 32-bit unsigned numbers in JavaScript
- ✅ 100% compatible with SA-MP 0.3DL algorithm

## 🧪 Test Files

The files in `assets/` are real SA-MP files with known hashes:

| File          | CRC32 Hash | Type    |
| ------------- | ---------- | ------- |
| `cesar.dff`   | `2F363354` | Model   |
| `cesar.txd`   | `4BCE378B` | Texture |
| `fam1.dff`    | `2CB8FD7E` | Model   |
| `fam1.txd`    | `4E76581E` | Texture |
| `wmyammo.dff` | `8EC07DC0` | Model   |
| `wmyammo.txd` | `27B61A89` | Texture |

## 🤝 Contributing

1. Fork the project
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is under the MIT License. See the `LICENSE` file for more details.
