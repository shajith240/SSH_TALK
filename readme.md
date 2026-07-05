# Call of SSH 

> A fully decentralized, peer-to-peer, end-to-end encrypted terminal messaging application. 

## The Vision
Most modern messaging applications route traffic through centralized servers owned by massive tech giants. **SSH_TALK** eliminates the middleman. By leveraging raw POSIX sockets and secure SSH tunneling, this application allows two local machines to discover each other, connect directly, and exchange encrypted messages peer-to-peer (P2P), entirely from the terminal. 

This project demonstrates a deep understanding of network programming, concurrency, cryptography, and operating system-level APIs.

## Tech Stack & Dependencies
* **Language:** C++ (using C++17/C++20 standards)
* **Networking:** POSIX Sockets (`<sys/socket.h>`)
* **Concurrency:** C++ `std::thread`, `std::mutex`, `std::async`
* **Encryption:** `libssh` or `libssh2` (C/C++ libraries for SSH protocol)
* **UI Interface:** `ncurses` (for building the terminal layout)
* **Environment:** Ubuntu / Linux (WSL is perfect for local testing)

---

## Development Roadmap & Phase Details

### Phase 1: Local Sockets & Basic Networking (The Foundation)
**Goal:** Establish a basic, unencrypted, blocking connection between two terminal windows on the same machine.
* **What to build:** A basic TCP Client and TCP Server. The server listens on a specific port; the client connects to `127.0.0.1` (localhost) on that port. Send a "Hello World" string across the connection.
* **Concepts to learn:** TCP/IP stack, Socket creation, Binding, Listening, Accepting, and Data transmission (`send()` and `recv()`).
* **Why it matters:** Your competitive programming background will give you an edge in structuring the data payloads and handling the buffers here, but mastering the socket API is essential before adding complexity.

### Phase 2: Concurrency & State Management
**Goal:** Make the chat non-blocking so users can type and receive messages simultaneously.
* **What to build:** Implement multi-threading. Thread A handles listening for incoming network packets. Thread B handles capturing user keyboard input. 
* **Concepts to learn:** Process scheduling, multi-threading, race conditions, mutex locks, and thread-safe queues.
* **Why it matters:** Tackling concurrency here is a direct practical application of the process management and memory synchronization concepts explored in architectures like xv6. 

### Phase 3: The Encryption Layer (SSH)
**Goal:** Secure the socket connection so packets cannot be intercepted or read in plain text.
* **What to build:** Integrate `libssh`. Replace the raw TCP send/receive functions with SSH-tunneled equivalents. Implement public/private key generation so the app can verify the identity of the connecting peer.
* **Concepts to learn:** Asymmetric cryptography (RSA/Ed25519), SSH handshakes, port forwarding, and secure key storage.
* **Why it matters:** Security is paramount in P2P. End-to-end encryption ensures that even if traffic is routed through external nodes later, the data remains dark.

### Phase 4: Peer Discovery & NAT Traversal (The Boss Fight)
**Goal:** Connect two laptops located on entirely different Wi-Fi networks across the internet.
* **What to build:** A mechanism to bypass standard home router firewalls. You will likely need to build a lightweight STUN (Session Traversal Utilities for NAT) server, or implement UDP Hole Punching.
* **Concepts to learn:** Network Address Translation (NAT), UDP vs. TCP for hole punching, and STUN/TURN protocols.
* **Why it matters:** This is the hardest part of the project. Successfully traversing NAT proves you understand the physical architecture of the global internet, not just local software.

### Phase 5: Minimalist Terminal UI
**Goal:** Build a clean, usable interface directly inside the terminal.
* **What to build:** Integrate the `ncurses` library to split the terminal window. Create a scrollable view for the chat history at the top, and a fixed, static input bar at the bottom.
* **Concepts to learn:** Terminal rendering, screen buffering, and event-driven UI loops.
* **Why it matters:** Translating Apple-inspired, bento-box grid principles into a text-based ncurses layout will give the application a highly polished, professional, and minimalist aesthetic. 

---

## Essential Reading & Resources
* **Beej's Guide to Network Programming:** This is the absolute gold standard for learning POSIX sockets in C/C++. Read this before you write a single line of network code.
* **Linux Man Pages:** Get comfortable typing `man socket`, `man bind`, and `man pthreads` in your Ubuntu terminal. 
* **libssh Documentation:** For integrating the SSH tunnel in Phase 3.