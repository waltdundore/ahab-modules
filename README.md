# Ahab Modules

**Service modules for Ahab infrastructure automation**

This repository contains service module definitions for the Ahab project. Each module defines how to deploy a specific service (Apache, MySQL, Nginx, etc.) using Docker Compose.

---

## What Are Modules?

Modules are self-contained service definitions that include:
- Service configuration (ports, volumes, networks)
- Dependencies on other modules
- Docker Compose service definitions
- Multi-platform support (Fedora, Debian, Ubuntu)
- Version tracking

---

## Module Structure

Each module is defined in a `module.yml` file:

```yaml
name: apache
version: 1.0.0
description: Apache HTTP Server
platforms:
  - fedora
  - debian
  - ubuntu
docker:
  image: httpd:2.4
  ports:
    - "80:80"
  volumes:
    - ./html:/usr/local/apache2/htdocs
dependencies: []
```

---

## Available Modules

### Web Servers
- **apache** - Apache HTTP Server 2.4
- **nginx** - Nginx web server (coming soon)

### Databases
- **mysql** - MySQL database server (coming soon)
- **postgresql** - PostgreSQL database (coming soon)

### Languages
- **php** - PHP runtime environment (coming soon)

### Caching
- **redis** - Redis in-memory data store (coming soon)

---

## How Modules Work

1. **Module Definition**: Each service has a `module.yml` file
2. **Docker Compose Generation**: Ahab reads module.yml and generates docker-compose.yml
3. **Dependency Resolution**: Modules can depend on other modules
4. **Unified Deployment**: Multiple modules combine into single docker-compose.yml

---

## Module Development

### Creating a New Module

1. Create a directory for your module: `mkdir myservice/`
2. Create `myservice/module.yml` with service definition
3. Test the module: `make test-module MODULE=myservice`
4. Submit pull request

### Module.yml Schema

```yaml
name: string              # Module name (required)
version: string           # Semantic version (required)
description: string       # Brief description (required)
platforms: array          # Supported platforms (required)
  - fedora
  - debian
  - ubuntu
docker:                   # Docker configuration (required)
  image: string           # Docker image (required)
  ports: array            # Port mappings (optional)
    - "host:container"
  volumes: array          # Volume mounts (optional)
    - "host:container"
  environment: object     # Environment variables (optional)
    KEY: value
  networks: array         # Networks to join (optional)
    - network_name
dependencies: array       # Required modules (optional)
  - module_name
```

---

## Testing Modules

```bash
# Test single module
make test-module MODULE=apache

# Test module with dependencies
make test-module MODULE=php

# Validate module.yml syntax
make validate-module MODULE=apache
```

---

## Module Registry

The main Ahab repository maintains a registry of available modules in `MODULE_REGISTRY.yml`. When you create a new module, add it to the registry.

---

## Contributing

1. Fork this repository
2. Create a feature branch: `git checkout -b feature/new-module`
3. Add your module with complete module.yml
4. Test thoroughly on all supported platforms
5. Submit pull request with:
   - Module definition
   - Test results
   - Documentation updates

---

## Module Guidelines

### Best Practices

1. **Use official Docker images** when available
2. **Minimize dependencies** - only depend on truly required modules
3. **Document configuration** - explain all environment variables
4. **Test on all platforms** - Fedora, Debian, Ubuntu
5. **Version carefully** - follow semantic versioning
6. **Keep it simple** - one service per module

### Security

1. **No hardcoded secrets** - use environment variables
2. **No privileged containers** - unless absolutely necessary
3. **Minimal permissions** - least privilege principle
4. **Official images only** - from Docker Hub or verified sources
5. **Pin versions** - don't use `latest` tag

### Documentation

Each module should include:
- Clear description of what it does
- Configuration options explained
- Example usage
- Known limitations
- Platform-specific notes

---

## Architecture

```
ahab-modules/
├── README.md              ← You are here
├── apache/
│   └── module.yml         ← Apache module definition
├── mysql/
│   └── module.yml         ← MySQL module definition
├── nginx/
│   └── module.yml         ← Nginx module definition
└── php/
    └── module.yml         ← PHP module definition
```

---

## Integration with Ahab

Ahab uses this repository as a Git submodule:

```bash
# In ahab repository
git submodule add https://github.com/waltdundore/ahab-modules.git modules
git submodule update --init --recursive
```

When you run `make install apache mysql`, Ahab:
1. Reads `modules/apache/module.yml`
2. Reads `modules/mysql/module.yml`
3. Resolves dependencies
4. Generates unified `docker-compose.yml`
5. Runs `docker-compose up -d`

---

## Version History

- **v0.1.0** (2025-12-08) - Initial release with Apache module

---

## License

Same as Ahab: CC BY-NC-SA 4.0 for educational use

---

## Support

- **Issues**: https://github.com/waltdundore/ahab-modules/issues
- **Main Project**: https://github.com/waltdundore/ahab
- **Documentation**: https://waltdundore.github.io

---

**Part of the Ahab project - Infrastructure automation for K-12 schools and non-profits**
