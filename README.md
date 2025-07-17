# ONDC Specifications Hub

This repository serves as the central hub for all ONDC (Open Network for Digital Commerce) specifications, organized using Git submodules for efficient management and version control.

## Overview

The ONDC Specifications Hub consolidates all domain-specific specifications into a single, well-organized structure. Each specification domain is maintained as a separate repository and linked here as a Git submodule, allowing for independent versioning while maintaining a unified view.

## Repository Structure

```
ONDC-Specifications/
├── SPECIFICATIONS/
│   ├── ONDC-Protocol-Specs/          # Core protocol specifications
│   ├── ONDC-RET-Specifications/      # Retail domain specifications
└── README.md                          # This file
```

## Getting Started

### Clone Repository with All Submodules

To clone this repository along with all specification submodules:

```bash
git clone --recursive https://github.com/nmonga26/ONDC-Specifications.git
```

### If Already Cloned Without Submodules

If you've already cloned the repository without the `--recursive` flag:

```bash
git submodule init
git submodule update
```

Or in a single command:

```bash
git submodule update --init --recursive
```

## 🔧 Working with Submodules

### Update a Specific Submodule

To update a specific specification submodule to its latest version:

```bash
# Navigate to the specific submodule
cd SPECIFICATIONS/ONDC-Protocol-Specs

# Pull the latest changes
git pull origin main

# Go back to the main repository
cd ../..

# Stage the submodule update
git add SPECIFICATIONS/ONDC-Protocol-Specs

# Commit the change
git commit -m "Update ONDC-Protocol-Specs to latest version"

# Push to remote
git push
```

### Update All Submodules

To update all submodules to their latest versions:

```bash
# Update all submodules to their latest remote versions
git submodule update --remote --merge

# Stage all changes
git add .

# Commit the updates
git commit -m "Update all specification submodules to latest versions"

# Push to remote
git push
```

### Check Submodule Status

To see the current status of all submodules:

```bash
git submodule status
```

### Fetch Changes Without Updating

To fetch the latest changes for all submodules without updating them:

```bash
git submodule foreach git fetch
```

## 📚 Specification Domains

### Core Specifications
- **ONDC-Protocol-Specs**: Core ONDC protocol definitions, APIs, and standards

### Domain-Specific Specifications
- **ONDC-RET-Specifications**: Retail and e-commerce domain specifications
- **ONDC-Protocol-Specs**: Open Network for Digital Commerce (ONDC) Protocol Open API Specifications

## Workflow Guidelines

### For Specification Maintainers

1. Make changes in the individual specification repository
2. Follow the versioning and release process for that repository
3. Notify the hub maintainers when significant updates are released

### For Hub Maintainers

1. Regularly update submodules to include latest stable versions
2. Ensure all submodules are pointing to stable releases
3. Document any breaking changes in the main repository

### For Contributors

1. Always work on the individual specification repositories
2. Follow the contribution guidelines of each specification repository
3. Do not make direct changes to submodules from this hub repository

## Versioning

- Each specification domain maintains its own semantic versioning
- This hub repository tags major milestones when multiple specifications are updated
- Version compatibility matrix is maintained in the docs folder

## Best Practices

1. **Always use recursive clone** when setting up the repository
2. **Check submodule status** before making updates
3. **Update submodules individually** when working on specific domains
4. **Test compatibility** when updating multiple submodules
5. **Document breaking changes** in commit messages
6. **Use meaningful commit messages** when updating submodules

## Contributing

To contribute to specific specifications:
1. Navigate to the individual specification repository
2. Follow the contribution guidelines for that repository
3. Submit pull requests to the specific repository, not this hub

## Troubleshooting

### Submodule Not Initialized
```bash
git submodule update --init --recursive
```

### Submodule Stuck on Old Commit
```bash
cd SPECIFICATIONS/[submodule-name]
git checkout main
git pull origin main
```

### Merge Conflicts in Submodules
```bash
cd SPECIFICATIONS/[submodule-name]
git status  # Check the conflict
git checkout --theirs .  # or --ours depending on your needs
```

**Note**: This repository structure uses Git submodules. Make sure you understand [Git submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules) before making changes.