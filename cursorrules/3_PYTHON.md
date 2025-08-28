# Python Development Standards

## Overview
These rules must be strictly followed when working with Python projects. They ensure consistency, performance, security, and maintainability across all AI/LLM applications and web services.

## Package Management & Environment Setup
- **Always use `uv` as the package manager** for all Python projects
- **Virtual environments**: Always activate virtual environments within the project in the `.venv` directory before performing any actions
- **Missing `.venv` directory**: If no `.venv` directory exists, create one immediately with:
  ```
  uv venv
  ```
- **Lock files**: Commit `uv.lock` to version control for reproducible builds
- **Python version**: Pin Python version in `pyproject.toml` and `.python-version`
- **Common commands**:
  - `uv sync` - Install dependencies from lock file
  - `uv add [package]` - Add new dependency
  - `uv run [command]` - Run commands in virtual environment
  - `uv run pytest` - Run tests (only when required)
  - `uv run ruff check` - Run linting
  - `uv run ruff format` - Format code

## Code Quality & Formatting
- **Formatter**: Use Ruff for code formatting (replaces Black + isort)
- **Linter**: Use Ruff for linting (replaces flake8, pylint)
- **Type Checker**: Use mypy for static type analysis
- **Configuration**: Define all tool configs in `pyproject.toml`
- **Pre-commit hooks**: Use pre-commit for automated quality checks
- **Line length**: 88 characters (Black/Ruff default)
- **Import sorting**: Automatic with Ruff, follow PEP 8 import ordering
- **Docstrings**: Use Google or NumPy style consistently

## Project Structure
```
project-name/
├── pyproject.toml          # Project configuration and dependencies
├── .python-version         # Python version specification
├── .env.example           # Environment variable template
├── README.md              # Project documentation
├── src/
│   └── project_name/
│       ├── __init__.py
│       ├── main.py        # Application entry point
│       ├── api/           # FastAPI routes and endpoints
│       ├── core/          # Core business logic
│       ├── db/            # Database models and operations
│       ├── services/      # Service layer (LLM, external APIs)
│       ├── schemas/       # Pydantic models and validation
│       ├── utils/         # Utility functions and helpers
│       └── config.py      # Configuration management
├── tests/                 # Test files mirroring src structure
├── docs/                  # Documentation files
└── scripts/               # Deployment and utility scripts
```

## Python Version & Language Features
- **Minimum compatibility**: Python 3.11+ (for improved performance and features)
- **Type hints**: Use consistently throughout all code, including generics
- **Modern syntax**: 
  - Leverage `match/case` statements where appropriate
  - Use `|` union syntax instead of `Union`
  - Use `list[str]` instead of `List[str]`
- **Async patterns**: Implement `async/await` patterns for all I/O operations
- **Error handling**: Use proper exception hierarchies and context managers
- **Data classes**: Prefer `@dataclass` or Pydantic models over plain classes

## Web API Development

### FastAPI (Preferred Framework)
- **Version**: Use FastAPI 0.100+ with latest features
- **Data validation**: Use Pydantic v2+ for all data validation and serialization
- **Documentation**: Implement comprehensive OpenAPI documentation with examples
- **Architecture patterns**:
  - Use dependency injection for database connections, services
  - Implement repository pattern for data access
  - Use service layer for business logic
  - Apply middleware for cross-cutting concerns
- **Security**:
  - Handle CORS properly for cross-origin requests
  - Implement proper authentication (JWT, OAuth2)
  - Use HTTPS in production
  - Validate all inputs with Pydantic
  - Implement rate limiting with slowapi
- **Response handling**:
  - Use appropriate HTTP status codes
  - Implement consistent error response format
  - Use streaming responses for large data
- **Performance**:
  - Use async route handlers for I/O operations
  - Implement proper caching strategies
  - Use connection pooling for databases

## Database Integration
- **ORM**: Prefer SQLAlchemy 2.0+ with async support
- **Migrations**: Use Alembic for database migrations
- **Connection management**: Implement proper connection pooling
- **Query optimization**: Use lazy loading and proper indexing
- **Transaction handling**: Use proper transaction scopes with context managers
- **Database URL**: Store connection strings in environment variables

## AI/LLM Integration

### LangChain v0.3+ (Preferred Library)
- **Architecture patterns**:
  - Use LangChain Expression Language (LCEL) for chain composition
  - Implement proper prompt templates and management
  - Use memory patterns for conversational AI
  - Implement retrieval-augmented generation (RAG) patterns
- **Performance optimization**:
  - Use streaming responses when possible for better UX
  - Implement async implementations for all LLM operations
  - Cache responses when appropriate to reduce costs and latency
  - Use connection pooling for LLM API clients
- **Error handling**:
  - Implement comprehensive error handling for API failures
  - Use exponential backoff for rate-limited APIs
  - Handle token limit exceeded errors gracefully
  - Implement fallback strategies for failed LLM calls
- **Monitoring**:
  - Track token usage and costs
  - Log LLM interactions for debugging
  - Monitor response times and error rates
  - Implement proper observability for chains

### Alternative LLM Libraries
- **OpenAI SDK**: For direct OpenAI integration
- **Anthropic SDK**: For Claude integration
- **Hugging Face Transformers**: For local model inference

## Data Processing & Validation
- **Pydantic**: Use Pydantic v2 for all data validation and serialization
- **Configuration**: Use Pydantic Settings for environment configuration
- **Custom validators**: Implement custom field validators where needed
- **Serialization**: Use Pydantic's JSON serialization for API responses
- **Data transformation**: Use pandas for complex data processing tasks
- **File handling**: Use pathlib for cross-platform file operations

## Testing Strategy
- **Framework**: Use pytest as the primary testing framework
- **Structure**: Mirror source structure in tests directory
- **Test types**:
  - Unit tests for individual functions and classes
  - Integration tests for API endpoints and database operations
  - End-to-end tests for complete workflows
- **Fixtures**: Use pytest fixtures for test data and dependencies
- **Mocking**: Use pytest-mock for mocking external dependencies
- **Async testing**: Use pytest-asyncio for async code testing
- **Coverage**: Use pytest-cov to track test coverage (aim for 85%+)
- **AI/LLM testing**: Mock LLM responses for deterministic tests

## Error Handling & Logging
- **Logging**: Use Python's logging module with structured logging
- **Log levels**: Implement appropriate log levels (DEBUG, INFO, WARNING, ERROR)
- **Error tracking**: Integrate with Sentry for production error monitoring
- **Custom exceptions**: Create domain-specific exception classes
- **Context managers**: Use context managers for resource management
- **Graceful degradation**: Implement fallback strategies for external service failures

## Security Best Practices
- **Environment variables**: Use python-dotenv for development, never commit secrets
- **Input validation**: Validate all inputs with Pydantic schemas
- **SQL injection**: Use parameterized queries with SQLAlchemy
- **Authentication**: Implement proper JWT handling with python-jose
- **HTTPS**: Always use HTTPS in production
- **Dependencies**: Regularly audit dependencies with `uv audit`
- **Secrets management**: Use proper secrets management in production
- **Rate limiting**: Implement API rate limiting to prevent abuse

## Performance Optimization
- **Profiling**: Use cProfile and line_profiler for performance analysis
- **Async operations**: Use asyncio for I/O-bound operations
- **Caching**: Implement caching with Redis or in-memory solutions
- **Database optimization**: Use proper indexing and query optimization
- **Memory management**: Monitor memory usage, especially for large datasets
- **Lazy evaluation**: Use generators and iterators for large data processing

## Configuration Management
- **Environment-based**: Use Pydantic Settings for configuration
- **Validation**: Validate all configuration at startup
- **Secrets**: Separate secrets from regular configuration
- **Documentation**: Document all configuration options
- **Defaults**: Provide sensible defaults for development

## Documentation Standards
- **README**: Include setup, development, and deployment instructions
- **API documentation**: Use FastAPI's automatic OpenAPI generation
- **Code documentation**: Use comprehensive docstrings with examples
- **Type annotations**: Include complete type annotations for all functions
- **Architecture docs**: Document system architecture and design decisions

## Development Workflow
- **Git conventions**: Use conventional commits (feat:, fix:, docs:, etc.)
- **Branch naming**: Use feature/, fix/, hotfix/ prefixes
- **Pre-commit hooks**: Use pre-commit with ruff, mypy, and tests
- **Code reviews**: Require PR reviews for all changes to main branch
- **CI/CD**: Implement automated testing and deployment pipelines

## Deployment & Production
- **Containerization**: Use Docker with multi-stage builds
- **Process management**: Use Gunicorn or Uvicorn workers
- **Environment variables**: Use platform-specific environment management
- **Health checks**: Implement proper health check endpoints
- **Monitoring**: Use APM tools like New Relic or DataDog
- **Scaling**: Design for horizontal scaling with stateless services

## AI/LLM Specific Patterns
- **Prompt engineering**: Use systematic prompt templates and testing
- **Context management**: Implement proper context window management
- **Token optimization**: Monitor and optimize token usage
- **Model selection**: Use appropriate models for specific tasks
- **Embeddings**: Implement proper vector storage and retrieval
- **RAG patterns**: Use retrieval-augmented generation for knowledge tasks
- **Agent patterns**: Implement tool-using agents with proper error handling
- **Evaluation**: Implement LLM output evaluation and quality metrics

## Dependencies Management
- **Core dependencies**: Keep minimal core dependencies
- **Optional dependencies**: Use optional dependencies for non-essential features
- **Version pinning**: Pin major versions, allow minor updates
- **Security updates**: Regularly update dependencies for security patches
- **Dependency groups**: Use dependency groups for dev, test, and production
