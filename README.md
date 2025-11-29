# IRC Server

A fully functional IRC (Internet Relay Chat) server implementation in C++98, compliant with RFC 1459 protocol specifications.

## Overview

This project implements a multi-client IRC server capable of handling authentication, channels, private messaging, and various IRC commands. Built using socket programming and the `poll()` multiplexing system, it ensures efficient concurrent client management.

## Features

### Core Functionality
- **Multi-client support** with non-blocking I/O operations
- **Authentication system** with password protection
- **Channel management** with operators and user privileges
- **Private messaging** between users
- **Real-time communication** using TCP sockets

### Supported IRC Commands

| Command | Description |
|---------|-------------|
| `PASS` | Server password authentication |
| `NICK` | Set or change nickname |
| `USER` | Set username and realname |
| `JOIN` | Join a channel |
| `PART` | Leave a channel |
| `PRIVMSG` | Send private messages to users or channels |
| `KICK` | Kick a user from a channel (operator only) |
| `INVITE` | Invite a user to a channel |
| `TOPIC` | View or change channel topic |
| `MODE` | Change channel modes |
| `PING` | Keep-alive mechanism |
| `QUIT` | Disconnect from server |

### Channel Modes
- **i** (invite-only): Channel requires invitation to join
- **t** (topic restriction): Only operators can change the topic
- **k** (password): Channel requires a password to join
- **o** (operator): Grant/revoke channel operator privileges
- **l** (user limit): Set maximum number of users in channel

### Bonus Feature
- **IRC Bot**: An automated bot that sends humorous programming-related messages to channels at regular intervals

## Architecture

The project follows an object-oriented design with clear separation of concerns:

```
.
├── includes/           # Header files
│   ├── Server.hpp     # Main server class
│   ├── Client.hpp     # Client representation
│   ├── Channel.hpp    # Channel management
│   ├── Bot.hpp        # Bot implementation
│   ├── ICommand.hpp   # Command interface
│   └── *Command.hpp   # Individual command implementations
│
├── sources/           # Implementation files
│   ├── Server.cpp     # Core server logic
│   ├── Client.cpp     # Client handling
│   ├── Channel.cpp    # Channel operations
│   ├── Bot.cpp        # Bot behavior
│   ├── *Command.cpp   # Command implementations
│   └── main.cpp       # Entry point
│
└── Makefile          # Build configuration
```

### Design Patterns
- **Command Pattern**: Each IRC command is encapsulated in its own class implementing the `ICommand` interface
- **Singleton Pattern**: Server instance with signal handling
- **Observer Pattern**: Broadcasting messages to channel members

## Technical Implementation

### Socket Programming
- TCP sockets with IPv4 (AF_INET)
- Non-blocking I/O using `fcntl()` with `O_NONBLOCK`
- `poll()` for efficient multiplexing of multiple client connections
- Proper signal handling (SIGINT, SIGTERM)

### Memory Management
- RAII principles with proper resource cleanup
- No memory leaks (all allocated resources are freed in destructors)
- Exception-safe allocation in constructors

### Protocol Compliance
- Messages terminated with `\r\n` (CRLF) as per RFC 1459
- Numeric replies for server responses
- Proper error handling and client notifications

## Building and Running

### Prerequisites
- C++ compiler with C++98 support (g++, clang++)
- Make
- Unix-like operating system (Linux, macOS)

### Compilation

```bash
make
```

This will compile the project and generate the `ircserv` executable.

### Usage

```bash
./ircserv <port> <password>
```

**Parameters:**
- `port`: Port number (1024-65535)
- `password`: Server password for client authentication

**Example:**
```bash
./ircserv 6667 mySecretPassword
```

### Connecting with an IRC Client

You can connect to the server using any standard IRC client (e.g., IRSSI, WeeChat, HexChat):

```bash
# Using IRSSI
irssi -c localhost -p 6667 -w mySecretPassword

# Using netcat for testing
nc localhost 6667
PASS mySecretPassword
NICK alice
USER alice 0 * :Alice Wonder
JOIN #general
```

## Development

### Compilation Flags
```
-Wall -Wextra -Werror -std=c++98
```

### Available Make Targets
- `make` or `make all`: Build the project
- `make clean`: Remove object files
- `make fclean`: Remove object files and executable
- `make re`: Clean and rebuild

### Testing
Test the server with multiple clients simultaneously to verify:
- Concurrent connection handling
- Message broadcasting in channels
- Private messaging
- Channel modes and operator commands
- Authentication system
- Bot functionality

## Project Constraints

- **Language**: C++98 standard
- **Allowed Functions**: socket, close, setsockopt, getsockname, getprotobyname, gethostbyname, getaddrinfo, freeaddrinfo, bind, connect, listen, accept, htons, htonl, ntohs, ntohl, inet_addr, inet_ntoa, send, recv, signal, sigaction, lseek, fstat, fcntl, poll
- **Forbidden**: fork, threads, boost libraries

## Error Handling

The server handles various error scenarios:
- Invalid port numbers
- Socket creation failures
- Client disconnections
- Invalid commands or syntax
- Permission errors (non-operators trying restricted actions)
- Resource allocation failures

## Future Improvements

Potential enhancements:
- SSL/TLS support for encrypted connections
- File transfer capabilities (DCC)
- User registration and authentication database
- Channel persistence
- More sophisticated bot commands
- IPv6 support
- Server-to-server linking

## Author

Developed as part of the 42 School curriculum.

## License

This project is part of an educational curriculum and is intended for learning purposes.
