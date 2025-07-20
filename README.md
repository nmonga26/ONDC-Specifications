# ONDC Specifications Hub

This repository serves as the central hub for all ONDC (Open Network for Digital Commerce) specifications, organized using Git submodules for efficient management and version control. It consolidates all domain-specific specifications while maintaining consistent standards and guidelines across the ecosystem.

## Table of Contents
- [Overview](#overview)
- [Repository Structure](#repository-structure)
- [Getting Started](#getting-started)
- [Specification Guidelines](#specification-guidelines)
- [Working with Submodules](#working-with-submodules)
- [Contributing](#contributing)
- [Versioning](#versioning)
- [Troubleshooting](#troubleshooting)

## Overview

The ONDC Specifications Hub provides:
- Centralized access to all ONDC domain specifications
- Consistent structure and standards across domains
- Independent versioning for each domain
- Unified documentation and contribution guidelines

## Repository Structure

```
ONDC-Specifications/
  │── ONDC-Protocol-Specs/          # Core protocol specifications
  │── ONDC-RET-Specifications/      # Retail domain specifications
  │── ONDC-LOG-Specifications/      # Logistics domain specifications
  │── ONDC-SRV-Specifications/      # Services domain specifications
  │── ONDC-{DOMAIN}-Specifications/ # Other domain specifications
  └── README.md                          # This file
```

### Domain Repository Structure
Each domain MUST follow this standard structure:
```
/ONDC-{DOMAIN}-Specifications
├── README.md
├── Usage.md
├── Contribution.md
├── CHANGELOG.md
├── Error-codes.xlsx
├── index.html
├── build_util
├── api/
│   ├── brd_images/
│   ├── build/
│   ├── components/
│   │   ├── Examples/
│   │   ├── attributes/
│   │   ├── enums/
│   │   ├── error_codes/
│   │   ├── flows/
│   │   ├── tags/
│   │   └── utils/
│   └── docs/
├── beckn-core/ (submodule)
└── ui/
```

## Getting Started

### Quick Setup

Clone the repository with all specification submodules:
```bash
git clone --recursive https://github.com/nmonga26/ONDC-Specifications.git
cd ONDC-Specifications
```

If already cloned without submodules:
```bash
git submodule update --init --recursive
```

## Specification Guidelines

### Adding New Specifications

When adding new specifications or updating existing ones, follow these requirements:

#### 1. File Naming Conventions
- API specs: `service_name_action.yaml`
- Examples: `{service_type}_{action}.json`
- Flow diagrams: `{service_type}_flow_{scenario}.png`
- Documentation: `{feature}_specification.md`

#### 2. Required Files for New Features
- [ ] API specification in `/api/components/`
- [ ] Examples in JSON and YAML formats
- [ ] Flow diagrams in `/api/brd_images/`
- [ ] Attribute definitions in `/api/components/attributes/`
- [ ] Enum definitions (if applicable)
- [ ] Updated error codes
- [ ] Documentation in `/api/docs/`

#### 3. API Specification Format
```yaml
openapi: 3.0.0
info:
  title: ONDC {Domain} API
  version: "draft-2.x.x"
  description: |
    Detailed description of the API purpose
    
paths:
  /{endpoint}:
    post:
      summary: Brief description
      description: Detailed description
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/{Schema}'
      responses:
        '200':
          description: Success response
        '400':
          description: Error scenarios
```

#### 4. Documentation Requirements
Each specification MUST include:
- Purpose and use cases
- Request/response formats
- Required vs optional fields
- Business rules and validations
- Error scenarios
- Example flows

## Working with Submodules

### Common Operations

#### Update a Specific Domain
```bash
# Navigate to the submodule
cd SPECIFICATIONS/ONDC-RET-Specifications

# Pull latest changes
git pull origin main

# Return to main repo and commit
cd ../..
git add SPECIFICATIONS/ONDC-RET-Specifications
git commit -m "Update ONDC-RET-Specifications to latest version"
git push
```

#### Update All Domains
```bash
# Update all submodules
git submodule update --remote --merge

# Commit all updates
git add .
git commit -m "Update all specification submodules to latest versions"
git push
```

#### Check Status
```bash
# View current status of all submodules
git submodule status

# Check for available updates
git submodule foreach git fetch
git submodule summary
```

### Workflow Guidelines

#### For Domain Maintainers
1. Work in individual specification repositories
2. Follow semantic versioning for releases
3. Update CHANGELOG.md with all changes
4. Notify hub maintainers of major updates

#### For Hub Maintainers
1. Review and update submodules weekly
2. Ensure all point to stable releases
3. Update VERSION_COMPATIBILITY.md
4. Tag hub repository for major milestones

#### For Contributors
1. Fork the specific domain repository
2. Create feature branch: `feature/{domain}-{feature-name}`
3. Follow domain-specific contribution guidelines
4. Submit PR to domain repository (not hub)

## Contributing

### Contribution Process

1. **Identify Target Domain**
   - Determine which specification domain your contribution affects
   - Navigate to that specific repository

2. **Follow Domain Guidelines**
   - Read the domain's Contribution.md
   - Ensure compliance with specification standards
   - Validate examples and schemas

3. **Submit Changes**
   - Create PR in domain repository
   - Reference any related issues
   - Include test results and documentation

### PR Checklist
- [ ] Follows file naming conventions
- [ ] Includes all required files
- [ ] Examples validated against schemas
- [ ] Documentation updated
- [ ] Build process successful
- [ ] No breaking changes (or clearly documented)

## Versioning

### Version Management

- **Domain Versions**: Each domain maintains independent semantic versioning
- **Hub Versions**: Tagged when multiple domains reach major milestones
- **Compatibility**: See `docs/VERSION_COMPATIBILITY.md` for cross-domain compatibility

### Version Format
```
draft-MAJOR.MINOR.PATCH
```
- **MAJOR**: Breaking changes
- **MINOR**: New features (backward compatible)
- **PATCH**: Bug fixes

## Troubleshooting

### Common Issues

#### Submodule Not Initialized
```bash
git submodule update --init --recursive
```

#### Submodule on Wrong Branch
```bash
cd SPECIFICATIONS/[domain-name]
git checkout main
git pull origin main
```

#### Merge Conflicts in Submodules
```bash
cd SPECIFICATIONS/[domain-name]
git status
# Resolve conflicts manually or:
git checkout --theirs .  # Accept remote changes
# or
git checkout --ours .    # Keep local changes
```

#### Submodule Showing Modified Status
```bash
# Check what changed
git diff SPECIFICATIONS/[domain-name]

# Reset if unintended
git submodule update --init
```
---

**Note**: This repository uses Git submodules. Familiarize yourself with [Git submodules documentation](https://git-scm.com/book/en/v2/Git-Tools-Submodules) before making changes.
