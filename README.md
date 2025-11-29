<div align="center">

# 💬 IRC Server

*A fully functional IRC server implementation in C++98 compliant with RFC 1459*

![C++](https://img.shields.io/badge/C++-98-00599C?style=for-the-badge&logo=c%2B%2B&logoColor=white)
![Status](https://img.shields.io/badge/Status-Complete-success?style=for-the-badge)

</div>

---

## 📋 Overview

A multi-client IRC server capable of handling authentication, channels, private messaging, and various IRC commands. Built using socket programming and the `poll()` multiplexing system for efficient concurrent client management.

---

## 🛠️ Technologies

<div align="center">

[![C++](https://img.shields.io/badge/C++-00599C?style=for-the-badge&logo=c%2B%2B&logoColor=white)](https://isocpp.org/)
[![Socket.io](https://img.shields.io/badge/Socket-Programming-010101?style=for-the-badge&logo=socket.io&logoColor=white)](https://en.wikipedia.org/wiki/Berkeley_sockets)
[![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)](https://www.linux.org/)
[![Make](https://img.shields.io/badge/Make-Building-6D00CC?style=for-the-badge&logo=cmake&logoColor=white)](https://www.gnu.org/software/make/)

**Key Concepts:** TCP/IP • Non-blocking I/O • Poll Multiplexing • RFC 1459 Protocol

</div>

---

## ✨ Features

### Core Functionality
- Multi-client support with non-blocking I/O
- Password-based authentication
- Channel management with operators
- Private messaging between users
- Real-time communication via TCP sockets

### Supported Commands

| Command | Description |
|---------|-------------|
| `PASS` | Server authentication |
| `NICK` | Set/change nickname |
| `USER` | Set user information |
| `JOIN` | Join a channel |
| `PART` | Leave a channel |
| `PRIVMSG` | Send messages |
| `KICK` | Kick user (operator) |
| `INVITE` | Invite user to channel |
| `TOPIC` | View/change topic |
| `MODE` | Change channel modes |
| `PING` | Keep-alive |
| `QUIT` | Disconnect |

### Channel Modes
- `+i` - Invite-only
- `+t` - Topic restriction (operators only)
- `+k` - Password protected
- `+o` - Operator privileges
- `+l` - User limit

### 🤖 Bonus
An IRC bot that sends humorous programming messages to channels at regular intervals.

---

## 🏗️ Architecture

```
.
├── includes/           # Header files
│   ├── Server.hpp     # Main server class
│   ├── Client.hpp     # Client representation
│   ├── Channel.hpp    # Channel management
│   ├── Bot.hpp        # Bot implementation
│   ├── ICommand.hpp   # Command interface
│   └── *Command.hpp   # Command implementations
│
├── sources/           # Source files
│   ├── Server.cpp
│   ├── Client.cpp
│   ├── Channel.cpp
│   ├── Bot.cpp
│   ├── *Command.cpp
│   └── main.cpp
│
└── Makefile
```

**Design Patterns:**
- Command Pattern (encapsulated IRC commands)
- Observer Pattern (message broadcasting)

---

## 🚀 Usage

### Build

```bash
make
```

### Run

```bash
./ircserv <port> <password>
```

**Example:**
```bash
./ircserv 6667 myPassword
```

### Connect

Using any IRC client (IRSSI, WeeChat, HexChat):

```bash
irssi -c localhost -p 6667 -w myPassword
```

Or with netcat:
```bash
nc localhost 6667
PASS myPassword
NICK alice
USER alice 0 * :Alice
JOIN #general
```

---

## 🔧 Technical Details

### Socket Programming
- TCP sockets with IPv4 (`AF_INET`)
- Non-blocking I/O (`fcntl` with `O_NONBLOCK`)
- `poll()` for multiplexing connections
- Signal handling (`SIGINT`, `SIGTERM`)

### Memory Management
- RAII principles
- No memory leaks
- Exception-safe allocation

### Protocol
- RFC 1459 compliant
- Messages terminated with `\r\n` (CRLF)
- Numeric replies for server responses

---

## 📝 Development

### Make Commands
- `make` - Build project
- `make clean` - Remove objects
- `make fclean` - Remove all generated files
- `make re` - Rebuild

### Compilation Flags
```
-Wall -Wextra -Werror -std=c++98
```

### Constraints
- **Language:** C++98
- **Allowed:** socket, close, setsockopt, bind, connect, listen, accept, send, recv, poll, fcntl, signal
- **Forbidden:** fork, threads, boost

---

## 👥 Authors

<div align="center">

Made with ❤️ by

**[@mmilliot](https://github.com/mmilliot)** & **[@mcotonea](https://github.com/mcotonea42)**

</div>

---

<div align="center">

### ⭐ If you found this project useful, please consider giving it a star!

**Happy coding!** 🎉

</div>
