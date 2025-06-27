# MCP Scientific Documentation Servers

A comprehensive repository for developing, testing, and deploying Model Context Protocol (MCP) servers that provide access to scientific computing and high-performance computing (HPC) library documentation.

## 🔬 Overview

This repository contains MCP servers designed to bridge the gap between AI models and scientific computing documentation. Each server provides structured access to documentation, API references, examples, and best practices for various scientific computing libraries and frameworks.

## 🏗️ Repository Structure

```
mcp/
├── servers/                    # Individual MCP servers
│   ├── numpy-docs/            # NumPy documentation server
│   ├── scipy-docs/            # SciPy documentation server
│   ├── mpi4py-docs/           # MPI4Py documentation server
│   ├── petsc-docs/            # PETSc documentation server
│   └── hpc-tools-docs/        # General HPC tools documentation
├── packages/                   # Shared packages and utilities
│   ├── mcp-base/              # Base MCP server framework
│   ├── doc-parser/            # Documentation parsing utilities
│   └── test-utils/            # Testing utilities
├── examples/                   # Example implementations and usage
├── docker/                     # Docker configurations
├── scripts/                    # Build and deployment scripts
├── docs/                       # Repository documentation
└── .github/                    # GitHub Actions workflows
```

## 🚀 Quick Start

### Prerequisites

- Node.js 18+ and npm
- Docker (optional, for containerized deployment)
- Python 3.8+ (for pip distribution)

### Installation

```bash
# Clone the repository
git clone https://github.com/your-username/mcp-scientific-docs.git
cd mcp-scientific-docs

# Install dependencies
npm install

# Build all packages
npm run build

# Run tests
npm test
```

### Running a Server

```bash
# Start the NumPy documentation server
npm run start:numpy-docs

# Or using Docker
docker run -p 3000:3000 ghcr.io/your-username/mcp-numpy-docs:latest
```

## 📦 Available MCP Servers

### NumPy Documentation Server (`numpy-docs`)
Provides access to NumPy documentation, including:
- API reference with function signatures
- Code examples and tutorials
- Performance optimization guides
- Broadcasting and indexing documentation

### SciPy Documentation Server (`scipy-docs`)
Covers SciPy ecosystem documentation:
- Module-specific documentation (scipy.linalg, scipy.optimize, etc.)
- Scientific computing algorithms
- Integration examples with NumPy

### MPI4Py Documentation Server (`mpi4py-docs`)
Parallel computing with Python:
- MPI concepts and patterns
- Collective operations documentation
- Performance considerations
- Example parallel algorithms

### PETSc Documentation Server (`petsc-docs`)
Portable, Extensible Toolkit for Scientific Computation:
- Solver documentation
- Matrix and vector operations
- Parallel computing patterns
- Performance tuning guides

### HPC Tools Documentation Server (`hpc-tools-docs`)
General HPC tools and practices:
- Job schedulers (SLURM, PBS, etc.)
- Profiling tools (Intel VTune, TAU, etc.)
- Optimization techniques
- Best practices for scientific computing

## 🛠️ Development

### Creating a New MCP Server

```bash
# Generate a new server from template
npm run create-server my-new-docs

# This creates:
# servers/my-new-docs/
# ├── src/
# │   ├── index.ts
# │   ├── handlers/
# │   └── parsers/
# ├── tests/
# ├── package.json
# └── README.md
```

### Development Workflow

```bash
# Install dependencies for all packages
npm run bootstrap

# Start development server with hot reload
npm run dev:numpy-docs

# Run tests in watch mode
npm run test:watch

# Lint and format code
npm run lint
npm run format

# Build for production
npm run build:all
```

### Project Structure for New Servers

Each MCP server follows this structure:

```typescript
// src/index.ts
import { MCPServer } from '@mcp-scientific/mcp-base';
import { DocumentationHandler } from './handlers/documentation';

const server = new MCPServer({
  name: 'my-docs-server',
  version: '1.0.0',
});

server.addHandler(new DocumentationHandler());
server.start();
```

## 🧪 Testing

We use a comprehensive testing strategy:

- **Unit Tests**: Jest for individual function testing
- **Integration Tests**: Testing MCP protocol compliance
- **End-to-End Tests**: Testing with actual MCP clients
- **Documentation Tests**: Ensuring documentation parsing accuracy

```bash
# Run all tests
npm test

# Run tests for specific server
npm run test:numpy-docs

# Run integration tests
npm run test:integration

# Generate coverage report
npm run test:coverage
```

## 📊 Quality Assurance

- **TypeScript**: Full type safety with strict mode
- **ESLint**: Code quality and consistency
- **Prettier**: Code formatting
- **Husky**: Pre-commit hooks
- **Semantic Release**: Automated versioning and releases

## 🐳 Docker Deployment

Each MCP server can be deployed as a Docker container:

```bash
# Build Docker image
docker build -f docker/numpy-docs.Dockerfile -t mcp-numpy-docs .

# Run container
docker run -p 3000:3000 mcp-numpy-docs

# Multi-architecture build
docker buildx build --platform linux/amd64,linux/arm64 -t ghcr.io/your-username/mcp-numpy-docs:latest .
```

### Docker Compose for Development

```yaml
# docker-compose.yml
version: '3.8'
services:
  numpy-docs:
    build: 
      context: .
      dockerfile: docker/numpy-docs.Dockerfile
    ports:
      - "3001:3000"
  
  scipy-docs:
    build:
      context: .
      dockerfile: docker/scipy-docs.Dockerfile
    ports:
      - "3002:3000"
```

## 📦 Package Distribution

### NPM Packages

Each server is published as an individual npm package:

```bash
# Install a specific server
npm install @mcp-scientific/numpy-docs

# Use in your project
import { NumpyDocsServer } from '@mcp-scientific/numpy-docs';
```

### Python Packages (PyPI)

For Python ecosystem integration:

```bash
# Install via pip
pip install mcp-numpy-docs

# Use in Python
from mcp_numpy_docs import NumpyDocsServer
```

## 🚢 Deployment Options

### GitHub Container Registry (GHCR)

```bash
# Pull and run
docker pull ghcr.io/your-username/mcp-numpy-docs:latest
docker run -p 3000:3000 ghcr.io/your-username/mcp-numpy-docs:latest
```

### NPM Registry

```bash
npx @mcp-scientific/numpy-docs
```

### Direct Binary (via pkg)

```bash
# Download pre-built binary
curl -L -o mcp-numpy-docs https://github.com/your-username/mcp-scientific-docs/releases/latest/download/mcp-numpy-docs-linux
chmod +x mcp-numpy-docs
./mcp-numpy-docs
```

## 🤝 Contributing

We welcome contributions! Please see our [Contributing Guide](CONTRIBUTING.md) for details.

### Development Setup

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/amazing-feature`
3. Install dependencies: `npm install`
4. Make your changes
5. Run tests: `npm test`
6. Commit changes: `git commit -m 'Add amazing feature'`
7. Push to branch: `git push origin feature/amazing-feature`
8. Open a Pull Request

### Code Style

- Use TypeScript with strict mode
- Follow existing code patterns
- Add tests for new functionality
- Update documentation as needed

## 📖 Examples

### Basic Usage with MCP Client

```typescript
import { MCPClient } from '@modelcontextprotocol/client';

const client = new MCPClient();
await client.connect('http://localhost:3000');

// Search NumPy documentation
const result = await client.request('search', {
  query: 'array broadcasting',
  library: 'numpy'
});

// Get function documentation
const docs = await client.request('get_function_docs', {
  function: 'numpy.array',
  include_examples: true
});
```

### Custom Documentation Parser

```typescript
import { DocumentationParser } from '@mcp-scientific/doc-parser';

class MyLibraryParser extends DocumentationParser {
  async parseDocumentation(source: string): Promise<Documentation> {
    // Custom parsing logic
    return {
      functions: this.parseFunctions(source),
      classes: this.parseClasses(source),
      examples: this.parseExamples(source)
    };
  }
}
```

## 🔧 Configuration

Each server can be configured via environment variables or config files:

```bash
# Environment variables
export MCP_PORT=3000
export MCP_DOC_SOURCE_URL=https://numpy.org/doc/stable/
export MCP_CACHE_TTL=3600
export MCP_LOG_LEVEL=info

# Or via config file
{
  "port": 3000,
  "docSourceUrl": "https://numpy.org/doc/stable/",
  "cacheTtl": 3600,
  "logLevel": "info"
}
```

## 📊 Monitoring and Observability

- Health check endpoints for all servers
- Prometheus metrics integration
- Structured logging with Winston
- Request tracing for debugging

## 🔒 Security

- Input validation and sanitization
- Rate limiting protection
- CORS configuration
- Security headers (helmet.js)

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- [Model Context Protocol](https://github.com/modelcontextprotocol/specification) team
- Scientific computing community
- Contributors and maintainers

## 📞 Support

- 📖 [Documentation](https://your-username.github.io/mcp-scientific-docs)
- 🐛 [Issue Tracker](https://github.com/your-username/mcp-scientific-docs/issues)
- 💬 [Discussions](https://github.com/your-username/mcp-scientific-docs/discussions)
- 📧 Email: your-email@domain.com

---

**Made with ❤️ for the scientific computing community**