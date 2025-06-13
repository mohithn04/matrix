# Matrix Rain Terminal Effect 🌧️

A sleek, customizable terminal-based Matrix rain effect written in pure Bash. Experience the iconic digital rain from The Matrix right in your terminal with smooth animations and configurable characters.

## ✨ Features

- **Pure Bash Implementation** - No external dependencies required
- **Smooth Animations** - Optimized raindrop rendering with configurable speeds
- **Mixed Character Sets** - Japanese katakana, numbers, symbols, and ASCII characters
- **Terminal Compatibility** - Works across different terminal emulators
- **Responsive Design** - Automatically adapts to terminal size changes
- **Clean Exit** - Proper cleanup and signal handling
- **Lightweight** - Minimal resource usage

## 🎬 Demo

```
アイウエオ    123    !@#
  カキク    456      $%^
    ケコ    789        &*
      サ    ABC          (
        シ  DEF            )
          ス GHI            -
            テ JKL            _
              ト MNO            =
                ナ PQR            +
```

## 🚀 Quick Start

### Installation

```bash
# Clone the repository
git clone https://github.com/mohithn04/matrix.git
cd matrix

# Make the script executable
chmod +x matrix.sh

# Run the effect
./matrix.sh
```

### One-liner Installation

```bash
curl -sSL https://raw.githubusercontent.com/mohithn04/matrix/main/matrix.sh | bash
```

## 💻 Requirements

- **Bash 3.0+** (works with both Bash 3 and 4+)
- **Terminal emulator** with ANSI escape sequence support
- **Unix/Linux/macOS** environment

## 🎮 Usage

### Basic Usage

```bash
./matrix.sh
```

### Exit the Effect

- Press `Ctrl+C` to exit cleanly
- The script will automatically restore your terminal settings

### Terminal Compatibility

Tested and working on:
- ✅ GNOME Terminal
- ✅ Konsole
- ✅ iTerm2
- ✅ Terminal.app (macOS)
- ✅ Windows Terminal (WSL)
- ✅ Alacritty
- ✅ Kitty

## ⚙️ Customization

### Character Sets

The script uses a mix of characters defined in the `SYMBOLS` variable:

```bash
SYMBOLS='アイウエオカキクケコサシスセソタチツテトナニヌネノハヒフヘホマミムメモヤユヨラリルレロワヲン0123456789!@#$%^&*()-_=+[]{}|;:,.<>?abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'
```

You can modify this to use different character sets:

- **Japanese only**: `アイウエオカキクケコサシスセソタチツテトナニヌネノハヒフヘホマミムメモヤユヨラリルレロワヲン`
- **Numbers only**: `0123456789`
- **Binary**: `01`
- **Custom symbols**: `!@#$%^&*()_+-=[]{}|;:,.<>?`

### Speed and Density

Adjust these variables in the `rain()` function:

```bash
# Raindrop spawn rate (line 87)
sleep 0.1  # Decrease for more frequent drops

# Individual drop speed (line 59)
sleep "0.0$dropSpeed"  # dropSpeed ranges 1-9

# Maximum concurrent drops (line 82)
local max_jobs=$((COLUMNS / 2))  # Increase for denser rain
```

### Colors

Currently uses green (Matrix-style). To add more colors, modify the `COLORS` array:

```bash
COLORS=('102;255;102' '255;102;102' '102;102;255')  # Green, Red, Blue
```

## 🔧 Technical Details

### How It Works

1. **Terminal Initialization**: Switches to alternate screen buffer and hides cursor
2. **Raindrop Generation**: Spawns background processes for each raindrop
3. **Animation Loop**: Each raindrop renders characters moving down the screen
4. **Job Control**: Manages background processes to prevent system overload
5. **Clean Exit**: Restores terminal state and kills background jobs

### Key Features

- **Signal Handling**: Proper cleanup on `SIGINT`, `SIGTERM`, and `EXIT`
- **Window Resize**: Handles terminal resize events (`SIGWINCH`)
- **Bash Version Compatibility**: Works with both old and new Bash versions
- **Memory Efficient**: Uses background jobs instead of storing screen state

## 🐛 Troubleshooting

### Common Issues

**Characters not displaying correctly**
```bash
# Ensure your terminal supports UTF-8
export LANG=en_US.UTF-8
export LC_ALL=en_US.UTF-8
```

**Script doesn't exit cleanly**
```bash
# Force kill if needed
pkill -f matrix.sh
```

**Performance issues**
```bash
# Reduce density by increasing sleep time
# Edit line 87: change 0.1 to 0.2 or higher
```

### Debugging

Run with debug output:
```bash
bash -x matrix.sh
```

## 🤝 Contributing

Contributions are welcome! Here's how you can help:

1. **Fork** the repository to your own GitHub account
2. **Clone** your fork locally: `git clone https://github.com/mohithn04/matrix.git`
3. **Create** a feature branch: `git checkout -b feature/amazing-feature`
4. **Make** your changes and test them
5. **Commit** your changes: `git commit -m 'Add amazing feature'`
6. **Push** to your fork: `git push origin feature/amazing-feature`
7. **Open** a Pull Request from your fork to the main repository

All pull requests will be reviewed before merging to ensure code quality and compatibility.

### Ideas for Contributions

- [ ] Configuration file support
- [ ] Additional color schemes
- [ ] Sound effects integration
- [ ] Different rain patterns
- [ ] Interactive mode
- [ ] Windows PowerShell version

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Support

If you find this project useful, please consider:

- ⭐ **Starring** this repository
- 🐛 **Reporting** bugs and issues
- 💡 **Suggesting** new features
- 🔄 **Sharing** with others

## 📞 Contact

- **GitHub**: [@mohithn04](https://github.com/mohithn04)
- **Issues**: [Report a bug](https://github.com/mohithn04/matrix/issues)

---

*"Welcome to the real world, Neo."* - Morpheus

**Made with ❤️ and Bash**
