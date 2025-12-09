# Initialize ahab-modules Repository

**Instructions for initializing the ahab-modules repository**

Date: December 8, 2025

---

## Files to Commit

This directory contains the initial structure for the ahab-modules repository:

```
ahab-modules-init/
├── README.md           ← Main documentation
├── LICENSE             ← CC BY-NC-SA 4.0 license
├── .gitignore          ← Git ignore rules
├── apache/
│   └── module.yml      ← Apache module definition
└── INITIALIZE.md       ← This file
```

---

## Initialization Steps

### 1. Clone the empty repository

```bash
git clone https://github.com/waltdundore/ahab-modules.git
cd ahab-modules
```

### 2. Copy initialization files

```bash
# From the ahab-modules-init directory
cp -r ../ahab-modules-init/* .
cp ../ahab-modules-init/.gitignore .
```

### 3. Initialize git and commit

```bash
git add .
git commit -m "Initial commit: ahab-modules repository

- Add README.md with module documentation
- Add LICENSE (CC BY-NC-SA 4.0)
- Add .gitignore for generated files
- Add apache module as first example
- Module structure and guidelines documented

This repository contains service module definitions for Ahab.
Each module defines how to deploy a service using Docker Compose."

git push origin main
```

### 4. Verify initialization

```bash
# Check that files are committed
git log --oneline

# Check remote
git remote -v

# Verify on GitHub
# Visit: https://github.com/waltdundore/ahab-modules
```

---

## Next Steps

After initialization:

1. **Add ahab-modules as submodule to ahab**:
   ```bash
   cd /path/to/ahab
   git submodule add https://github.com/waltdundore/ahab-modules.git modules
   git submodule update --init --recursive
   ```

2. **Create additional modules**:
   - mysql/module.yml
   - nginx/module.yml
   - php/module.yml
   - postgresql/module.yml
   - redis/module.yml

3. **Update MODULE_REGISTRY.yml** in main ahab repository

4. **Test module loading**:
   ```bash
   make test-module MODULE=apache
   ```

---

## Module Template

When creating new modules, use this template:

```yaml
name: service_name
version: 1.0.0
description: Brief description of the service
platforms:
  - fedora
  - debian
  - ubuntu
docker:
  image: official/image:tag
  container_name: ahab_service_name
  ports:
    - "host:container"
  volumes:
    - ./data:/container/path
  environment:
    KEY: value
  restart: unless-stopped
  networks:
    - ahab_network
dependencies: []
notes: |
  Configuration and usage notes here
```

---

## Troubleshooting

### Repository already has commits

If the repository already has commits, you'll need to force push:

```bash
git push -f origin main
```

**Warning**: This will overwrite any existing commits!

### Permission denied

Make sure you have write access to the repository:

```bash
git remote -v
# Should show: https://github.com/waltdundore/ahab-modules.git
```

If using SSH, ensure your SSH key is configured:

```bash
ssh -T git@github.com
```

---

## Verification Checklist

- [ ] Repository cloned successfully
- [ ] All files copied to repository
- [ ] .gitignore is present (hidden file!)
- [ ] Initial commit created
- [ ] Pushed to GitHub
- [ ] Files visible on GitHub web interface
- [ ] README.md renders correctly on GitHub
- [ ] apache/module.yml is present

---

**Once initialized, this repository will be ready to use as a submodule in the main ahab project.**
