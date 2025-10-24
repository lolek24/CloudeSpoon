# SAP BTP CAP JavaScript Project

## Project Overview
This is a Node.js project built using the SAP Cloud Application Programming (CAP) model for SAP Business Technology Platform (BTP). CAP provides a framework for building enterprise-grade applications with built-in support for multitenancy, authentication, and integration with SAP services.

## Technology Stack
- **Runtime**: Node.js
- **Framework**: SAP CAP (Cloud Application Programming Model)
- **Language**: JavaScript/TypeScript
- **Platform**: SAP Business Technology Platform (BTP)
- **Database**: SAP HANA Cloud / SQLite (for local development)

## Development Setup

### Prerequisites
- Node.js (version 18+ recommended)
- npm or yarn
- SAP CAP CLI: `npm install -g @sap/cds-dk`
- Cloud Foundry CLI (for BTP deployment)

### Local Development
```bash
# Install dependencies
npm install

# Start local development server
npm run start
# or
cds serve

# Watch mode for development
cds watch
```

### Database Management
```bash
# Deploy database schema locally
cds deploy --to sqlite

# For SAP HANA
cds deploy --to hana
```

## Project Structure
```
├── app/                    # UI applications (Fiori Elements, custom UIs)
├── db/                     # Database artifacts (CDS models, data)
├── srv/                    # Service implementations
├── package.json           # Project configuration
├── .cdsrc.json           # CAP configuration
└── mta.yaml              # Multi-target application descriptor
```

## CAP Best Practices

### Core Development Principles
- **Capture Intent**: Focus on "what" rather than "how" - model your domain intent clearly
- **Minimize Boilerplate**: Leverage CAP's built-in features to reduce technical debt
- **Grow as You Go**: Start simple and extend incrementally as requirements evolve
- **Domain-Driven Design**: Model your business domain first, then implement services

### CDS Modeling
- Use proper naming conventions (entities in PascalCase, properties in camelCase)
- Focus on capturing domain intent in your models
- Define associations and compositions correctly for data relationships
- Use aspects for reusable model fragments and cross-cutting concerns
- Implement proper data types, constraints, and validations
- Model with performance considerations from the start
- Use compositions for master-detail relationships
- Define calculated fields and virtual elements where appropriate

### Service Implementation
- Define clear service interfaces using CDS service definitions
- Keep service logic in separate files under `srv/`
- Use generic providers for standard CRUD operations
- Implement custom logic with event handlers (before/after/on)
- Add comprehensive input validation
- Support actions and functions for complex business operations
- Use CAP's built-in features (authentication, authorization, etc.)
- Implement proper error handling with meaningful messages
- Use transactions for data consistency
- Leverage CAP's automatic OData protocol support

### Security
- Implement CDS-based authorization using `@requires` and `@restrict` annotations
- Use platform security features (XSUAA, OAuth2)
- Annotate and protect personal data with `@PersonalData` annotations
- Enable automatic audit logging for compliance
- Validate input data at service boundaries
- Follow principle of least privilege
- Implement role-based access control
- Use secure coding practices for custom handlers

### Performance
- Use projections to limit data transfer and improve query performance
- Optimize database interactions with efficient CDS queries
- Implement proper caching strategies where appropriate
- Use streaming for large datasets
- Consider database-specific optimizations for SAP HANA
- Monitor and profile query performance
- Use lazy loading for associations when appropriate
- Implement pagination for large result sets

### Extensibility & Multitenancy
- Design services to support multitenancy from the start
- Use CAP's built-in tenant isolation features
- Implement extension points for customization
- Support cloud-native deployment strategies
- Enable horizontal scaling capabilities
- Design for intrinsic resilience and fault tolerance

## Git Workflow

### Branch Strategy
- `main` - production-ready code
- `develop` - integration branch
- `feature/*` - feature development
- `hotfix/*` - production fixes

### Commit Guidelines
```bash
# Format: type(scope): description
feat(service): add customer registration endpoint
fix(db): resolve duplicate key constraint issue
docs(readme): update setup instructions
```

### Before Committing
```bash
# Run linting
npm run lint

# Run tests
npm test

# Build the project
npm run build

# Check for security vulnerabilities
npm audit
```

## Testing

### Unit Tests
```bash
# Run all tests
npm test

# Run with coverage
npm run test:coverage

# Watch mode
npm run test:watch
```

### Integration Tests
```bash
# Test with local database
npm run test:integration

# Test against HANA
npm run test:hana
```

## Deployment

### Local Deployment
```bash
# Build for production
npm run build

# Start production server
npm start
```

### SAP BTP Deployment
```bash
# Build MTA archive
mbt build

# Deploy to Cloud Foundry
cf deploy mta_archives/*.mtar
```

## Environment Configuration

### Development (.env.local)
```
CDS_ENV=development
DEBUG=*
```

### Production (BTP)
- Configure service bindings
- Set up destination services
- Configure authentication (XSUAA)

## Common Commands
```bash
# CAP Commands
cds init                    # Initialize new CAP project
cds serve                   # Start development server
cds watch                   # Watch mode with auto-reload
cds deploy                  # Deploy database schema
cds build                   # Build for production
cds compile                 # Compile CDS models

# Development
npm run start              # Start application
npm run dev                # Development mode
npm run test               # Run tests
npm run lint               # Lint code
npm run build              # Build for production

# Database
cds deploy --to sqlite     # Local SQLite database
cds deploy --to hana       # SAP HANA deployment
```

## Troubleshooting

### Common Issues
1. **Port conflicts**: CAP default port is 4004
2. **Database connection**: Check service bindings and credentials
3. **Authentication**: Verify XSUAA configuration
4. **Deployment**: Check MTA descriptor and service dependencies

### Debug Mode
```bash
# Enable debug logging
DEBUG=* cds serve

# Specific debug categories
DEBUG=serve,db cds serve
```

## Resources
- [SAP CAP Documentation](https://cap.cloud.sap/)
- [CAP Samples](https://github.com/SAP-samples/cloud-cap-samples)
- [SAP BTP Documentation](https://help.sap.com/docs/btp)
- [Fiori Elements](https://ui5.sap.com/fiori-elements)

## Code Quality

### Linting
- Use ESLint with SAP-specific rules
- Configure Prettier for code formatting
- Set up pre-commit hooks

### Type Safety
- Consider migrating to TypeScript
- Use JSDoc for type annotations
- Implement proper input validation

## Performance Monitoring
- Use SAP Application Logging
- Implement health checks
- Monitor memory usage and response times
- Set up alerts for critical thresholds
