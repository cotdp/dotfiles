# Personal Dotfiles & Development Configuration

A curated collection of development environment configurations and Cursor IDE rules designed to enhance productivity and maintain consistency across software engineering projects.

## 🚀 Overview

This repository contains my personal dotfiles and development configurations, with a focus on **Cursor IDE rules** and **Claude Code slash commands** that provide AI-assisted coding with best practices built-in. The configurations are designed for modern software development using TypeScript, Python, Next.js, and AI/LLM applications.

### Key Features

- 🤖 **AI-Enhanced Development**: Cursor IDE rules that guide AI assistants to follow best practices
- ⚡ **Claude Code Slash Commands**: Systematic development workflow with `/plan`, `/cook`, `/continue`, `/release`
- 📋 **TODO.md-Driven Development**: Centralized project roadmaps with progress tracking
- 🎯 **Technology-Specific Rules**: Tailored configurations for TypeScript, Python, Next.js, and more
- 🔒 **Security-First**: Built-in security practices and OWASP compliance
- ⚡ **Performance-Optimized**: Configuration focused on clean, performant code
- 🧪 **Type-Safe**: Strict typing standards across all languages
- ♿ **Accessibility**: WCAG 2.1 AA compliance by default
- 📦 **Modern Tooling**: Support for latest package managers (bun, uv) and frameworks

## 📁 Repository Structure

```
dotfiles/
├── README.md                    # This file
├── claude-code/                 # Claude Code configuration & slash commands
│   ├── README.md               # Claude Code system overview
│   ├── CLAUDE.md               # Core configuration and coding standards
│   └── commands/               # Custom slash commands
│       ├── README.md           # Detailed command documentation
│       ├── plan.md             # /plan - Technical documentation analysis
│       ├── cook.md             # /cook - Implementation execution
│       ├── continue.md         # /continue - Resume interrupted work
│       └── release.md          # /release - Production release preparation
└── cursorrules/                 # Cursor IDE rules collection
    ├── README.md               # Cursor rules overview
    ├── 1_GENERAL.md           # Core development principles & git workflow
    ├── 2_TYPESCRIPT.md        # TypeScript/Next.js specific rules
    ├── 3_PYTHON.md            # Python development standards
    ├── 4_AI_MODELS.md         # AI model selection guidelines
    ├── 5_TOOLS.md             # Command-line tools documentation
    └── 6_NEXTJS.md            # Next.js 15 breaking changes & best practices
```

## 🛠️ Configuration Files

### Core Development Standards (`1_GENERAL.md`)
- **Code Quality Principles**: Minimal, self-documenting, type-exact, secure, performant
- **Development Process**: Planning methodology with `<thinking>` tags
- **Git Workflow**: Conventional commits, branch strategy, and automated workflows
- **Security Best Practices**: Input validation, environment management, HTTPS enforcement
- **Project Planning**: TODO.md methodology for task tracking
- **NanoID Usage**: Guidelines for public-facing unique identifiers

### TypeScript Development (`2_TYPESCRIPT.md`)
- **Package Management**: bun-first approach with locked dependencies
- **Next.js 15**: App Router, src directory structure, Vercel deployment
- **Code Quality**: ESLint, Prettier, import organization
- **Architecture**: Feature-based organization, dependency injection
- **State Management**: Zustand with persistence patterns
- **Database**: Drizzle ORM with PostgreSQL integration

### Python Development (`3_PYTHON.md`)
- **Package Management**: uv-first with virtual environments
- **Framework Standards**: FastAPI with Pydantic v2, async patterns
- **Code Quality**: Ruff for formatting and linting, mypy for type checking
- **AI/LLM Integration**: LangChain v0.3+ with streaming support
- **Project Structure**: src-layout with clear separation of concerns
- **Testing**: pytest with comprehensive coverage requirements

### AI Model Selection (`4_AI_MODELS.md`)
- **Cost-Effective Models**: gpt-5-nano, gpt-5-mini for general tasks
- **Reasoning Models**: o3-mini, o4-mini for complex problem-solving
- **Multimodal**: gpt-5, gpt-4o-mini for image and mixed content
- **Search Integration**: Perplexity models for real-time information
- **Claude Models**: claude-sonnet-4 for coding agents and workflows

### Command-Line Tools (`5_TOOLS.md`)
- **ImageMagick**: Image conversion and favicon generation
- **Advanced Usage**: Multi-size support, transparency handling
- **Common Patterns**: SVG to ICO conversion, background removal

### Next.js Specifics (`6_NEXTJS.md`)
- **Breaking Changes**: React 19 requirements, async request APIs
- **Migration Guide**: cookies(), headers(), params await patterns
- **Best Practices**: Server Components, client-side optimization
- **Performance**: Code splitting, lazy loading, caching strategies

## 🎯 Claude Code Configuration System

The `claude-code/` directory contains a comprehensive Claude Code configuration system designed for systematic software development workflows.

### Core Configuration (`CLAUDE.md`)
- **Code Quality Standards**: Minimal, self-documenting, type-exact, secure, performant principles
- **Technology Stack Preferences**: TypeScript/Next.js with bun, Python with uv, AI model selection
- **Git Workflow Management**: Conventional commits and proactive remote synchronization
- **Context-Aware Development**: Planning process with `<thinking>` tags and requirement analysis

### Slash Commands System (`commands/`)

| Command | Purpose | Usage |
|---------|---------|-------|
| `/plan` | Analyze documentation and create comprehensive TODO.md implementation plans | `/plan "Building a real-time chat application"` |
| `/cook` | Execute tasks from TODO.md systematically with quality enforcement | `/cook "Focus on authentication features"` |
| `/continue` | Resume interrupted work by assessing current state and completing tasks | `/continue "Fix failing tests and complete API"` |
| `/release` | Prepare production releases with quality checks and version management | `/release "Urgent security patch"` |

### Workflow Integration
- **TODO.md-Driven Development**: Central implementation roadmap managed by all commands
- **Dependency-Aware Execution**: Intelligent task ordering and prerequisite handling
- **Quality Checkpoints**: Non-negotiable code standards enforced throughout
- **Context-Guided AI**: Optional context arguments focus AI efforts on specific priorities

### Key Features
- **Systematic Development**: Plan → Cook → Continue → Release workflow
- **Progress Tracking**: Real-time TODO.md updates with completion timestamps
- **Quality Enforcement**: Built-in standards for security, performance, and maintainability
- **Technology Integration**: Support for TypeScript/Next.js and Python project patterns

## 🚀 Getting Started

### Prerequisites

- [Cursor IDE](https://cursor.sh/) - AI-first code editor
- [Claude Code](https://claude.com/claude-code) - AI-powered development environment (for slash commands)
- [bun](https://bun.sh/) - Fast JavaScript runtime and package manager
- [uv](https://github.com/astral-sh/uv) - Fast Python package manager
- [Git](https://git-scm.com/) - Version control system

### Installation

1. **Clone the repository**:
   ```bash
   git clone https://github.com/yourusername/dotfiles.git ~/dotfiles
   cd ~/dotfiles
   ```

2. **Use in your projects**:

   **For general development**:
   ```bash
   cp ~/dotfiles/cursorrules/1_GENERAL.md /path/to/your/project/.cursorrules
   ```

   **For TypeScript/Next.js projects**:
   ```bash
   cat ~/dotfiles/cursorrules/1_GENERAL.md ~/dotfiles/cursorrules/2_TYPESCRIPT.md > /path/to/your/project/.cursorrules
   ```

   **For Python projects**:
   ```bash
   cat ~/dotfiles/cursorrules/1_GENERAL.md ~/dotfiles/cursorrules/3_PYTHON.md > /path/to/your/project/.cursorrules
   ```

3. **Claude Code Configuration** (optional, for slash commands):
   ```bash
   # Copy Claude Code configuration to your project
   cp -r ~/dotfiles/claude-code /path/to/your/project/.claude
   ```

4. **Cursor IDE will automatically detect and apply** the rules when you open the project.

### Project-Specific Setup

Create a `.cursorrules` file in your project root by combining relevant configuration files:

```bash
# Example: Full-stack TypeScript project with AI features
cat ~/dotfiles/cursorrules/1_GENERAL.md \
    ~/dotfiles/cursorrules/2_TYPESCRIPT.md \
    ~/dotfiles/cursorrules/4_AI_MODELS.md \
    ~/dotfiles/cursorrules/6_NEXTJS.md > .cursorrules
```

## 💡 Usage Examples

### Starting a New TypeScript Project

```bash
# Initialize project
mkdir my-awesome-app && cd my-awesome-app
bun init

# Apply cursor rules
cat ~/dotfiles/cursorrules/1_GENERAL.md ~/dotfiles/cursorrules/2_TYPESCRIPT.md > .cursorrules

# Initialize git with conventional commits
git init
git add .
git commit -m "feat: initial project setup"
```

### Starting a New Python Project

```bash
# Initialize project
mkdir my-python-service && cd my-python-service
uv init

# Apply cursor rules
cat ~/dotfiles/cursorrules/1_GENERAL.md ~/dotfiles/cursorrules/3_PYTHON.md > .cursorrules

# Setup virtual environment
uv venv
source .venv/bin/activate  # or .venv\Scripts\activate on Windows

# Initial commit
git init
git add .
git commit -m "feat: initial Python project setup"
```

### Claude Code Slash Commands Workflow

```bash
# 1. Setup Claude Code configuration
cp -r ~/dotfiles/claude-code .claude

# 2. Analyze requirements and create implementation plan
/plan "Building a REST API with user authentication and real-time features"

# 3. Execute tasks systematically from TODO.md
/cook "Focus on database setup and authentication first"

# 4. Resume work after interruptions
/continue "Complete the API endpoints and fix failing tests"

# 5. Prepare for production release
/release "Ready for production deployment"
```

## 🎯 Key Principles

### Code Quality Hierarchy
1. **Minimal**: Write only what's necessary
2. **Self-documenting**: Code explains itself through naming and structure
3. **Type-exact**: Comprehensive typing throughout
4. **Secure**: Built-in security practices
5. **Performant**: Optimized without premature complexity
6. **Accessible**: WCAG 2.1 AA compliance by default
7. **Testable**: Designed for easy testing and maintenance

### Development Workflow
- **Planning**: Use `<thinking>` tags to analyze requirements or `/plan` for comprehensive roadmaps
- **Implementation**: Systematic execution with `/cook` for TODO.md-driven development
- **Continuation**: Resume interrupted work with `/continue` for intelligent task completion
- **Release**: Production preparation with `/release` for quality-assured deployments
- **Version Control**: Conventional commits with automatic git workflows
- **Documentation**: Central `TODO.md` roadmaps with progress tracking
- **Quality**: ESLint, Prettier, Ruff, and type checking enforced
- **Security**: Input validation, environment management, secure defaults

## 🔧 Customization

### Adding New Rules

1. Create a new `.md` file in the `cursorrules/` directory
2. Follow the existing pattern and structure
3. Update this README with the new configuration
4. Test with sample projects before committing

### Modifying Existing Rules

1. Edit the relevant configuration file
2. Test changes in a sample project
3. Update documentation if needed
4. Commit with descriptive message

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/new-config`
3. Make your changes following the existing patterns
4. Test thoroughly with sample projects
5. Submit a pull request with detailed description

## 📚 References

- [Claude Code Documentation](https://claude.com/claude-code) - AI-powered development environment
- [Cursor IDE Documentation](https://cursor.sh/docs) - AI-first code editor
- [Awesome Cursor Rules](https://github.com/PatrickJS/awesome-cursorrules) - Community cursor rules
- [Conventional Commits](https://www.conventionalcommits.org/) - Standardized commit messages
- [Next.js Documentation](https://nextjs.org/docs) - React framework
- [TypeScript Handbook](https://www.typescriptlang.org/docs/) - Type-safe JavaScript
- [Python Best Practices](https://docs.python.org/3/tutorial/) - Python development
- [WCAG 2.1 Guidelines](https://www.w3.org/WAI/WCAG21/quickref/) - Accessibility standards

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- [Patrick JS](https://github.com/PatrickJS) for the awesome-cursorrules collection
- The Cursor IDE team for creating an amazing AI-first development environment
- The open source community for continuous inspiration and best practices

---

**Note**: These configurations are opinionated and reflect personal development preferences optimized for modern software engineering practices. Feel free to adapt them to your specific needs and workflow.