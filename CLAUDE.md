# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview
This repository is set up for an SAP BTP CAP (Cloud Application Programming Model) JavaScript project. The project structure is not yet initialized - use `cds init` to create the project scaffold.

## Technology Stack
- **Runtime**: Node.js (version 18+)
- **Framework**: SAP CAP (Cloud Application Programming Model)
- **Language**: JavaScript
- **Platform**: SAP Business Technology Platform (BTP)
- **Database**: SAP HANA Cloud (production) / SQLite (local development)

## Initial Setup

### Prerequisites
Install the SAP CDS CLI globally:
```bash
npm install -g @sap/cds-dk
```

### Initialize Project
```bash
# Create new CAP project structure
cds init

# Install dependencies
npm install
```

## Development Commands

### Running the Application
```bash
cds watch          # Development mode with hot reload (recommended)
cds serve          # Start server without watch
npm start          # Production mode
```

### Database Management
```bash
cds deploy --to sqlite      # Deploy schema to local SQLite
cds deploy --to hana        # Deploy to SAP HANA
```

### Building and Deployment
```bash
cds build          # Build project
mbt build          # Build MTA archive for BTP deployment
cf deploy mta_archives/*.mtar    # Deploy to Cloud Foundry
```

### Debugging
```bash
DEBUG=* cds serve           # Enable all debug output
DEBUG=serve,db cds serve    # Enable specific debug categories
```

## CAP Project Structure
Once initialized, the typical structure is:
- `db/` - Database artifacts (CDS models, data)
- `srv/` - Service implementations and business logic
- `app/` - UI applications (Fiori Elements, custom UIs)
- `package.json` - Project configuration
- `.cdsrc.json` - CAP configuration

## CAP Development Guidelines

### CDS Modeling
- Use PascalCase for entities, camelCase for properties
- Define associations and compositions for relationships
- Use aspects for reusable model fragments
- Leverage built-in aspects: `cuid`, `managed`, `temporal`

### Service Implementation
- Keep service logic in `srv/` directory
- Use event handlers: `srv.before()`, `srv.on()`, `srv.after()`
- Leverage generic providers for CRUD operations
- Implement custom actions/functions for complex operations
- Use `SELECT`, `INSERT`, `UPDATE`, `DELETE` from `cds.ql` for database operations

### Security
- Apply `@requires` and `@restrict` annotations for authorization
- Use `@PersonalData` annotations for GDPR compliance
- Validate all input data at service boundaries

### Performance
- Use projections to limit data transfer
- Implement pagination for large result sets
- Use `SELECT.columns()` to fetch only needed fields
- Consider database-specific optimizations for HANA

## Common CDS Commands
```bash
cds                 # Show help and available commands
cds version         # Show version info
cds compile <file>  # Compile CDS models to see output
cds env             # Show effective configuration
cds lint            # Lint CDS models
```

## Port Configuration
CAP default port is 4004. Configure via:
- Environment variable: `PORT=8080 cds serve`
- package.json: `"cds": { "server": { "port": 8080 } }`
