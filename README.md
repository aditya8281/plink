# plink - Peer-to-Peer File Transfer


plink is a secure, efficient peer-to-peer file transfer tool that enables direct file sharing between devices without relying on centralized servers. Built with modularity and security in mind.

## Features

-  **Multiple Connection Methods**: Direct connection, UPnP, NAT hole punching, and role reversal
-  **End-to-End Encryption**: AES-256 encryption with secure key exchange
-  **Smart Chunking**: Efficient data chunking for large file transfers
-  **Cross-Platform**: Works on Windows, macOS, and Linux
-  **Secure by Default**: All transfers are encrypted and verified

## Project Structure

```
plink/
├── README.md
├── requirements.txt
├── main.py
├── .gitignore
├── docs/
├── backend/
│   ├── init.py
│   ├── networking/
│   │   ├── init.py
│   │   ├── analyze_network.py
│   │   ├── strategies/
│   │   │   ├── init.py
│   │   │   ├── direct_connection.py
│   │   │   ├── FC_to_FC.py
│   │   │   ├── FC_to_PRC.py
│   │   │   ├── FC_to_RC.py
│   │   │   ├── FC_to_SYM.py
│   │   │   ├── PRC_to_PRC.py
│   │   │   ├── RC_to_PRC.py
│   │   │   ├── RC_to_RC.py
│   │   │   └── RC_to_SYM.py
│   │   └── utils/
│   │       ├── init.py
│   │       ├── network_utils.py
│   │       └── port_scanning.py
│   └── cryptography/
│       ├── init.py
│       ├── core/
│       │   ├── init.py
│       │   └── cipher.py
│       ├── data/
│       │   ├── init.py
│       │   ├── receiver/
│       │   │    ├── init.py
│       │   │    ├── chunk_manager.py
│       │   │    ├── compression.py
│       │   │    └── metadata.py
│       │   └── sender/
│       │        ├── init.py
│       │        ├── chunk_manager.py
│       │        ├── compression.py
│       │        └── metadata.py
│       └── utils/
│           └── key_generation.py
├── frontend/
├── init.py
├── cli/
│   ├── init.py
│   ├── main.py
│   ├── receiver/
│   │    └── argument_parser.py
│   └── sender/
│        └── argument_parser.py
└── test/
└── argument_parser.py
├── utils/
├── init.py
├── link.py
├── logging.py
└── plink_file.py
└── test/
├── backend/
│   └── cryptography/
│       └── data/
│           ├── test_chunk_manager.py
│           ├── test_compression.py
│           └── test_metadata.py
└── frontend/
└── argument_parser.py

```

### Prerequisites

- Python 3.8 or higher
- pip package manager

## Quick Start

### Basic File Transfer

**Sender:**
```bash
plink send /path/to/file
```

**Receiver:**
```bash
plink receive /path/to/store
```

## Command Line Interface

### Sender Commands / WIP

```bash
plink send <file_path> [OPTIONS]

OPTIONS:
  --method, -m          Connection method (direct, upnp, hole-punch, role-reverse)
  --encryption, -e     Encryption method (aes256, chacha20)
  --chunk-size, -c     Chunk size in KB (default: 1024)
  --password           Set transfer password
  --timeout            Connection timeout in seconds
  --resume             Resume interrupted transfer
```

### Receiver Commands / WIP

```bash
plink receive [OPTIONS]

OPTIONS:
  --output-dir, -o     Output directory (default: current directory)
  --method, -m         Preferred connection method
  --password           Transfer password
  --max-size           Maximum file size to accept (MB)
```

## Connection Methods

### 1. Direct Connection
- **Use Case**: Same network, known IP addresses
- **Advantages**: Fastest, most reliable
- **Requirements**: Open ports, direct network access

### 2. UPnP (Universal Plug and Play)
- **Use Case**: Behind NAT with UPnP-enabled router
- **Advantages**: Automatic port forwarding
- **Requirements**: UPnP-enabled router

### 3. NAT Hole Punching
- **Use Case**: Both peers behind NAT
- **Advantages**: Works through most NAT configurations
- **Requirements**: STUN server access

### 4. Role Reversal
- **Use Case**: Asymmetric NAT situations
- **Advantages**: Fallback when other methods fail
- **Requirements**: One peer with open connectivity

### Pull Request Process

1. Create a feature branch from `main`
2. Make virtual environments and install requirements.txt
3. Make your changes with appropriate tests
4. Update documentation and requirement.txt if needed
5. Ensure all tests pass
6. Submit pull request with clear description
