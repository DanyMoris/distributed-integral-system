# Distributed Integral System

Client-server system for distributed numerical integration of the function:

\[
f(x) = \frac{1}{\ln(x)}
\]

The system distributes computation across multiple network clients and fully utilizes available CPU cores on each machine.

---

# 📌 Features

- C++17 standard
- Cross-platform (Windows/Linux)
- CMake build system
- Protobuf serialization
- Multithreaded computation
- Dynamic task distribution
- Logging support
- Modular architecture
- Ready for containerization (Docker support can be added)

---

# 🏗 Architecture Overview

The system consists of three main components:

## 1️⃣ Server
- Accepts client connections
- Receives integration parameters from user
- Splits the task proportionally to CPU cores of connected clients
- Sends serialized tasks via TCP
- Aggregates partial results
- Outputs final result

## 2️⃣ Client
- Connects to server
- Reports number of available CPU cores
- Receives integration sub-task
- Executes parallel numerical integration
- Sends partial result back to server

## 3️⃣ Common Module
- Protobuf message definitions
- Shared data structures
- Utility functions

---

# 🔄 Communication Protocol

All data is serialized using **Protocol Buffers**.

## Messages

- `RegisterClient`
- `Task`
- `Result`

Communication is performed over TCP sockets.

---

# 🧮 Numerical Integration

The function:

\[
\int_a^b \frac{1}{\ln(x)} dx
\]

⚠ Important:
- The function is undefined at `x = 1`
- The integral has no elementary closed-form solution
- The system uses numerical methods (e.g., Simpson’s rule)

Each client:
- Splits its assigned interval across available CPU cores
- Computes partial sums in parallel
- Uses synchronized reduction
- Returns aggregated result to server

---

# 📂 Project Structure
DistributedIntegral/
│
├── CMakeLists.txt
├── README.md
├── .gitignore
│
├── common/
│ ├── proto/
│ ├── include/
│ └── src/
│
├── server/
│ └── src/
│
├── client/
│ └── src/
│
└── tests/
└── src/

---

# ⚙️ Requirements

- C++17 compatible compiler
- CMake ≥ 3.16
- Protobuf
- Visual Studio 2022 (recommended for Windows)
- Git

---

# 🔨 Build Instructions

```bash
git clone <repo_url>
cd DistributedIntegral

mkdir build
cd build
cmake ..
cmake --build .