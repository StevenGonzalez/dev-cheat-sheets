# Developer Cheat Sheets 📚

> A comprehensive collection of developer cheat sheets and quick-reference guides for essential tools and workflows.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![GitHub stars](https://img.shields.io/github/stars/StevenGonzalez/dev-cheat-sheets?style=social)](https://github.com/StevenGonzalez/dev-cheat-sheets/stargazers)

This repository contains carefully crafted cheat sheets for the most commonly used developer tools and technologies. Each guide is designed to be both beginner-friendly and valuable for experienced developers who need quick reference materials.

## 🎯 Purpose

Whether you're a junior developer learning the ropes or a senior engineer who needs a quick reminder of syntax and commands, these cheat sheets provide:

- **Quick Reference**: Find what you need fast
- **Practical Examples**: Real-world code snippets and use cases
- **Best Practices**: Learn the right way to use each tool
- **Comprehensive Coverage**: From basics to advanced features
- **Copy-Paste Ready**: All examples are tested and ready to use

## 📋 Available Cheat Sheets

### Core Developer Tools

| Guide                                       | Description                     | Key Topics                                                          |
| ------------------------------------------- | ------------------------------- | ------------------------------------------------------------------- |
| [**Git Cheat Sheet**](./git.md)             | Version control with Git        | Commands, branching, merging, workflows, best practices             |
| [**Docker Cheat Sheet**](./docker.md)       | Containerization and deployment | Images, containers, Dockerfile, Docker Compose, best practices      |
| [**Bash Scripting Cheat Sheet**](./bash.md) | Shell scripting and automation  | Variables, loops, functions, file operations, debugging             |
| [**Regex Cheat Sheet**](./regex.md)         | Pattern matching for text       | Character classes, quantifiers, groups, lookaround, common patterns |

### Documentation and Editing

| Guide                                     | Description                     | Key Topics                                      |
| ----------------------------------------- | ------------------------------- | ----------------------------------------------- |
| [**Markdown Cheat Sheet**](./markdown.md) | Document formatting and writing | Syntax, tables, links, GitHub flavored markdown |
| [**VS Code Cheat Sheet**](./vscode.md)    | Code editor productivity        | Shortcuts, extensions, debugging, customization |

## 🚀 Quick Start

### Browse Online

Simply click on any of the cheat sheet links above to view them directly on GitHub.

### Clone Locally

```bash
# Clone the repository
git clone https://github.com/StevenGonzalez/dev-cheat-sheets.git

# Navigate to the directory
cd dev-cheat-sheets

# Open in your preferred editor
code .  # VS Code
vim .   # Vim
```

### Download Individual Files

Right-click on any `.md` file in the repository and select "Save link as" to download individual cheat sheets.

## 📖 How to Use

Each cheat sheet is structured for maximum usability:

1. **Table of Contents** - Navigate quickly to specific topics
2. **Code Examples** - Copy-paste ready snippets
3. **Explanations** - Context and usage notes
4. **Tips & Best Practices** - Professional insights
5. **Troubleshooting** - Common issues and solutions

### Example Usage

Need to remember Git commands?

```bash
# Quick reference from git.md
git status                    # Check repository status
git add .                     # Stage all changes
git commit -m "Your message"  # Commit with message
git push origin main          # Push to remote
```

Setting up a Docker container?

```bash
# From docker.md
docker run -d -p 3000:3000 --name myapp node:16-alpine
docker logs myapp
docker exec -it myapp /bin/sh
```

## 🤝 Contributing

We welcome contributions! Here's how you can help:

### Adding New Cheat Sheets

1. Fork the repository
2. Create a new `.md` file following our template structure
3. Include a comprehensive table of contents
4. Add practical examples and best practices
5. Submit a pull request

### Improving Existing Guides

- Fix typos or errors
- Add new examples or commands
- Update outdated information
- Improve explanations

### Cheat Sheet Template

```markdown
# Tool Name Cheat Sheet

## Table of Contents

- [Basic Usage](#basic-usage)
- [Advanced Features](#advanced-features)
- [Best Practices](#best-practices)
- [Troubleshooting](#troubleshooting)

## Basic Usage

<!-- Content here -->

## Advanced Features

<!-- Content here -->

## Best Practices

<!-- Content here -->

## Troubleshooting

<!-- Content here -->
```

### Guidelines

- Keep examples practical and tested
- Use consistent formatting
- Include both beginner and advanced content
- Add explanations for complex commands
- Follow markdown best practices

## 📝 Format Standards

All cheat sheets follow these standards:

- **Markdown Format**: Easy to read and edit
- **Code Blocks**: Syntax highlighted examples
- **Tables**: For comparing options or shortcuts
- **Links**: Internal navigation and external resources
- **Emojis**: Visual cues for better scanning

## 🔧 Local Development

To contribute or customize these cheat sheets:

1. **Prerequisites**

   - Git installed
   - Markdown editor (VS Code recommended)
   - Basic knowledge of the tool you're documenting

2. **Setup**

   ```bash
   git clone https://github.com/StevenGonzalez/dev-cheat-sheets.git
   cd dev-cheat-sheets
   ```

3. **Preview Changes**

   - Use VS Code's built-in markdown preview (`Ctrl+Shift+V`)
   - Or any markdown preview tool

4. **Test Examples**
   - Verify all code examples work
   - Test commands in appropriate environments

## 📊 What's Next?

Planned additions:

- [x] Regex Cheat Sheet ([view](./regex.md))
- [ ] Python Cheat Sheet
- [ ] JavaScript/Node.js Cheat Sheet
- [ ] SQL Cheat Sheet
- [ ] Linux Commands Cheat Sheet
- [ ] HTTP Status Codes Reference

## 💡 Tips for Maximum Benefit

1. **Bookmark**: Add this repository to your browser bookmarks
2. **Star**: Star the repository to keep track of updates
3. **Local Copy**: Clone for offline access
4. **Print**: Some developers prefer printed references
5. **Contribute**: Share your own tips and improvements

## 🌟 Why These Tools?

The tools covered in this repository represent the core of modern software development:

- **Git**: Essential for version control and collaboration
- **Docker**: Critical for containerization and deployment
- **Bash**: Fundamental for automation and system administration
- **Markdown**: Standard for documentation and README files
- **VS Code**: Popular editor with extensive capabilities

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Inspired by the developer community's need for quick, reliable references
- Built with feedback from developers of all skill levels
- Continuously updated based on industry best practices

## 📞 Contact

- **GitHub Issues**: For bugs, questions, or suggestions about the cheat sheets
- **Pull Requests**: For contributions and improvements
- **Discussions**: For general questions and community interaction

---

**Happy coding!** 🚀 If you find these cheat sheets helpful, please consider starring the repository and sharing it with other developers.
