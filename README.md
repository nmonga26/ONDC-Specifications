# ONDC Specifications Hub

This repository serves as the central hub for all ONDC (Open Network for Digital Commerce) specifications, organized using Git submodules for efficient management and version control.

## Overview

The ONDC Specifications Hub consolidates all domain-specific specifications into a single, well-organized structure. Each specification domain is maintained as a separate repository and linked here as a Git submodule, allowing for independent versioning while maintaining a unified view.

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

## Working with Submodules

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

## Specification Domains

### Core Specifications
- **ONDC-Protocol-Specs**: Core ONDC protocol definitions, APIs, and standards

### Domain-Specific Specifications
- **ONDC-RET-Specifications**: Retail and e-commerce domain specifications
- **ONDC-LOG-Specifications**: Logistics and delivery specifications
- **ONDC-SRV-Specifications**: Services domain specifications

# ONDC Specifications Guidelines

## Purpose
This document establishes comprehensive guidelines for adding new specifications or updating existing specifications in the ONDC-Specifications repository. All contributors must follow these guidelines to maintain consistency, quality, and interoperability across all ONDC domains.

## 1. Repository Structure Requirements

### 1.1 Domain Organization
- Each domain MUST have its own submodule following the naming pattern: `ONDC-{DOMAIN}-Specifications`
- Examples: `ONDC-RET-Specifications`, `ONDC-LOG-Specifications`, `ONDC-SRV-Specifications`

### 1.2 Standard Directory Structure
Every domain repository MUST follow this structure:
```
/ONDC-{DOMAIN}-Specifications
├── README.md
├── Usage.md
├── Contribution.md
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
├── ONDC-transaction-Specifications/ (submodule - REQUIRED)
└── ui/
```

### 1.3 Required Submodules
All domain specification repositories MUST include:
- **ONDC-transaction-specifications**: ONDC Transaction Specifications (MANDATORY)
 ```bash
# When creating or updating a domain specification repository:
git submodule add https://github.com/nmonga26/ONDC-transaction-Specifications.git ONDC-transaction-Specifications
```

## 2. Specification File Guidelines

### 2.1 File Naming Conventions
- Use lowercase with underscores for file names: `service_name_action.yaml`
- API examples: `{service_type}_{action}.json` or `{service_type}_{action}.yaml`
- Flow diagrams: `{service_type}_flow_{scenario}.png`
- Documentation: `{feature}_specification.md`

### 2.2 File Formats
- **API Specifications**: YAML format (primary), JSON for examples
- **Documentation**: Markdown (.md)
- **Diagrams**: PNG or SVG
- **Error Codes**: Excel (.xlsx) at root, YAML in components

### 2.3 Required Files for New Features
When adding a new service or feature, include:
1. API specification files in `/api/components/`
2. Examples in both JSON and YAML formats
3. Flow diagrams in `/api/brd_images/`
4. Attribute definitions in `/api/components/attributes/`
5. Enum definitions if applicable
6. Updated error codes
7. Documentation in `/api/docs/`

## 3. API Specification Standards

### 3.1 Example Structure
Each API endpoint MUST have:
- Request example: `{action}_request.json`
- Response example: `on_{action}_response.json`
- Error scenarios: `{action}_error_scenarios.yaml`

### 3.2 Required Sections
Every specification file MUST include:
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

### 3.3 Component Reusability
- Define reusable components in `/api/components/index.yaml`
- Reference common schemas using `$ref`
- Avoid duplication across specifications

## 4. Documentation Requirements

### 4.1 README.md Structure
Each domain repository MUST have a README with:
1. Domain overview and supported categories
2. Version information
3. Quick start guide
4. Links to detailed documentation
5. Contact information

### 4.2 API Documentation
For each API endpoint, document:
- Purpose and use cases
- Request/response formats
- Required vs optional fields
- Business rules and validations
- Error scenarios
- Example flows

### 4.3 Business Requirements
Include in `/api/docs/`:
- Business Requirements Document (BRD)
- Product Requirements Document (PRD)
- API mapping documentation
- Integration guidelines

## 5. Versioning Guidelines

### 5.1 Version Format
Follow semantic versioning: `draft-MAJOR.MINOR.PATCH`
- MAJOR: Breaking changes
- MINOR: New features (backward compatible)
- PATCH: Bug fixes

### 5.2 Version Alignment
- Align with Beckn protocol version
- Document version compatibility matrix
- Maintain backward compatibility for at least 2 minor versions

### 5.3 Change Documentation
For each version update:
- Update CHANGELOG.md with detailed changes
- Tag release in Git
- Update all affected documentation

## 6. Validation and Testing

### 6.1 Pre-commit Checks
Before committing:
- Validate YAML/JSON syntax
- Check for required fields
- Ensure examples match schemas
- Run build utilities to verify compilation

### 6.2 Example Validation
- All examples MUST be valid according to schemas
- Include both success and error scenarios
- Test edge cases

### 6.3 Build Process
- Run `build_util` to compile specifications
- Verify generated files in `/api/build/`
- Check for build errors or warnings

## 7. Contribution Process

### 7.1 Branch Strategy
- Create feature branches: `feature/{domain}-{feature-name}`
- Bug fixes: `fix/{domain}-{issue-number}`
- Documentation: `docs/{domain}-{topic}`

### 7.2 Pull Request Requirements
PRs MUST include:
1. Descriptive title with domain prefix
2. Summary of changes
3. Link to related issues
4. Test results
5. Documentation updates
6. Reviewer checklist

### 7.3 Review Criteria
Reviewers will check:
- Adherence to these guidelines
- Technical accuracy
- Backward compatibility
- Documentation completeness
- Example validity

## 8. Domain-Specific Requirements

### 8.1 Category Codes
Use standardized ONDC category codes:
- Format: `ONDC:{DOMAIN}{NUMBER}`
- Example: `ONDC:SRV10`, `ONDC:RET01`
- Document category mapping in README

### 8.2 Service Flows
Define flows for:
- Standard transaction flow
- Cancellation scenarios
- Update/modification flows
- Error handling flows
- Edge cases

### 8.3 Attributes and Enums
- Define domain-specific attributes
- Create comprehensive enum lists
- Document business rules
- Provide validation logic

## 9. Error Handling Standards

### 9.1 Error Code Format
```
{DOMAIN}-{CATEGORY}-{NUMBER}
Example: SRV-VALIDATION-001
```

### 9.2 Error Documentation
For each error code, provide:
- Error code
- HTTP status
- Error message
- Description
- Resolution steps

## 10. UI Integration

### 10.1 Documentation UI
- Ensure specifications render correctly in UI
- Test navigation and search functionality
- Verify example display
- Check responsive design

### 10.2 Interactive Features
Support for:
- API testing interface
- Example switching (JSON/YAML)
- Schema navigation
- Search functionality

## 11. Maintenance Guidelines

### 11.1 Regular Updates
- Review specifications quarterly
- Update deprecated features
- Incorporate feedback
- Align with ONDC policy changes

### 11.2 Issue Management
- Use GitHub issues for tracking
- Label issues by domain and type
- Prioritize security and breaking changes
- Maintain issue templates

## 12. Security Considerations

### 12.1 Sensitive Data
- Never include real credentials in examples
- Use placeholder values
- Document security requirements
- Include authentication/authorization specs

### 12.2 Data Privacy
- Follow ONDC privacy guidelines
- Mask personal information in examples
- Document data retention policies
- Include consent mechanisms

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

## Appendix A: Checklist for New Specifications

- [ ] Created directory structure
- [ ] Added API specification files
- [ ] Included request/response examples
- [ ] Defined attributes and enums
- [ ] Created flow diagrams
- [ ] Updated error codes
- [ ] Written documentation
- [ ] Validated all files
- [ ] Run build process
- [ ] Updated README
- [ ] Created PR with description
- [ ] Passed review process

## Appendix B: File Templates

### API Specification Template
```yaml
openapi: 3.0.0
info:
  title: ONDC {Service} API
  version: draft-2.0.0
  description: |
    API specification for {service description}

    Transaction Specifications: 
      This API follows ONDC Transaction Specifications for audit, logging, and error handling.
      Reference: ./ONDC-transaction-Specifications/

servers:
  - url: https://api.ondc.org/{domain}
    description: Production server

paths:
  /{endpoint}:
    post:
      summary: {Action description}
      operationId: {actionName}
      tags:
        - {Service Category}
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/{RequestSchema}'
            examples:
              example1:
                $ref: '#/components/examples/{ExampleName}'
      responses:
        '200':
          description: Successful response
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/{ResponseSchema}'
        '400':
          description: Bad request
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Error'

components:
  schemas:
    # Define schemas here
  examples:
    # Define examples here
```

### Flow Documentation Template
```markdown
# {Service} Flow Documentation

## Overview
Brief description of the service flow

## Participants
- Buyer App (BAP)
- Seller App (BPP)
- Gateway

## Flow Steps

### 1. Discovery
Description of discovery phase

### 2. Order Creation
Description of order creation

### 3. Fulfillment
Description of fulfillment process

### 4. Completion
Description of completion phase

## Error Scenarios
List of possible error scenarios

## Business Rules
Important business rules to consider
```

**Note**: This repository structure uses Git submodules. Make sure you understand [Git submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules) before making changes.
