# Carbon Offset Registry & Trading Platform

A decentralized marketplace for environmental offset project registration, independent verification, credit tokenization, transparent trading, and immutable retirement tracking with verifiable environmental impact proof.

## Overview

This smart contract implements a comprehensive carbon offset trading platform on the Stacks blockchain that enables:

- Environmental project registration and management
- Independent third-party verification processes
- Carbon credit tokenization and batch creation
- Peer-to-peer credit trading marketplace
- Permanent credit retirement with certificate issuance
- Transparent audit trails and verification history

## Features

### Project Management
- **Project Registration**: Developers can register environmental offset projects with comprehensive details
- **Verification Process**: Independent organizations conduct project verification and validate carbon credits
- **Status Tracking**: Real-time monitoring of project status from registration to operational

### Credit Trading System
- **Batch Creation**: Verified projects can create trading batches with specific vintage years and pricing
- **Marketplace Trading**: Users can purchase carbon credits directly from project developers
- **Peer-to-Peer Transfers**: Credit holders can transfer credits to other addresses

### Retirement & Certificates
- **Permanent Retirement**: Credits can be permanently retired for environmental claims
- **Digital Certificates**: Platform administrators can issue verifiable retirement certificates
- **Beneficiary Assignment**: Retirements can be made on behalf of third parties

### Verification Network
- **Authorized Verifiers**: Platform maintains registry of certified verification organizations
- **Audit Trails**: Complete verification history with methodology documentation
- **Multi-Round Verification**: Projects support multiple verification rounds over time

## Supported Environmental Categories

The platform supports the following project categories:

- Renewable Energy Generation
- Forest Restoration & Conservation
- Methane Capture & Utilization
- Energy Efficiency Optimization
- Carbon Capture & Sequestration
- Regenerative Agriculture Practices
- Waste Reduction & Recycling
- Clean Transportation Infrastructure

## Contract Architecture

### Core Data Structures

**Environmental Offset Project Registry**
- Project metadata and documentation
- Developer information and location details
- Verification status and credit statistics
- Activity status tracking

**Independent Verification Audit Trail**
- Verifier organization details
- Validation quantities and methodologies
- Monitoring periods and report locations
- Verification timestamps

**Carbon Credit Trading Batches**
- Project origin and vintage year
- Quantity and pricing information
- Trading status and availability

**Individual Credit Holdings Registry**
- User balance tracking by project and vintage
- Support for multiple project holdings

**Permanent Retirement Transaction Log**
- Retirement details and purposes
- Beneficiary information
- Certificate locations and timestamps

## Key Functions

### Project Operations

#### `register-environmental-offset-project`
Register a new environmental offset project with validation of required fields and supported categories.

**Parameters:**
- `project-title`: Project name (max 128 chars)
- `comprehensive-description`: Detailed description (max 1024 chars)
- `project-location`: Geographic location
- `environmental-impact-category`: Must match supported categories
- `project-start-date`: Project start timestamp
- `projected-completion-date`: Expected completion timestamp
- `supporting-documentation-uri`: Link to project documentation

#### `conduct-independent-project-verification`
Conduct verification of a registered project by authorized verification organizations.

**Parameters:**
- `project-id`: Target project identifier
- `credits-validated-quantity`: Number of credits validated
- `verification-report-location`: Link to verification report
- `methodology-standard-applied`: Verification methodology used
- `monitoring-period-beginning`: Start of monitoring period
- `monitoring-period-ending`: End of monitoring period
- `verification-documentation`: Additional verification data

### Trading Operations

#### `create-carbon-credit-trading-batch`
Create a trading batch from verified project credits.

**Parameters:**
- `originating-project-id`: Source project identifier
- `credit-issuance-vintage`: Vintage year for credits
- `batch-total-quantity`: Number of credits in batch
- `per-credit-price-ustx`: Price per credit in microSTX

#### `execute-carbon-credit-purchase`
Purchase carbon credits from available trading batches.

**Parameters:**
- `batch-id`: Target batch identifier
- `desired-credit-quantity`: Number of credits to purchase

### Retirement Operations

#### `execute-permanent-carbon-credit-retirement`
Permanently retire carbon credits with optional beneficiary assignment.

**Parameters:**
- `originating-project-id`: Source project identifier
- `vintage-year`: Credit vintage year
- `retirement-quantity`: Number of credits to retire
- `retirement-purpose-description`: Reason for retirement
- `retirement-beneficiary-address`: Optional beneficiary address

### Administrative Functions

#### `authorize-verification-organization`
Platform administrators can authorize verification organizations.

**Parameters:**
- `verifier-organization-address`: Organization address
- `organization-official-name`: Official organization name
- `certification-credentials`: Verification credentials

#### `issue-digital-retirement-certificate`
Issue digital certificates for completed retirements.

**Parameters:**
- `retirement-record-id`: Target retirement record
- `retirement-certificate-location`: Certificate document link

## Read-Only Functions

### Query Functions

- `get-environmental-project-information(project-id)`: Retrieve project details
- `get-carbon-credit-batch-information(batch-id)`: Get batch information
- `get-individual-credit-holdings-balance(address, project-id, vintage-year)`: Check user balances
- `get-retirement-transaction-information(retirement-id)`: View retirement details
- `get-verification-organization-status(verifier-address)`: Check verifier status
- `get-project-verification-history(project-id, round)`: View verification history
- `get-supported-environmental-categories()`: List supported project categories
- `get-platform-operational-statistics()`: Platform statistics and counters

## Error Codes

The contract uses standardized error codes for validation and operation failures:

- `404`: Resource not found
- `403`: Unauthorized access
- `400`: Invalid parameters
- `402`: Insufficient balance
- `410`: Unsupported project category
- `411`: Invalid date range
- `412`: Required field empty
- `413`: Project not verified
- `414`: Project status inactive
- `415`: Insufficient credit supply
- `416`: Credit batch unavailable
- `417`: Payment transaction failed
- `418`: Certificate already exists
- `419`: Self-authorization forbidden
- `420`: Vintage year out of range

## Configuration

### Platform Constants

- **Minimum Vintage Year**: 2010
- **Maximum Project Categories**: 10
- **Platform Administrator**: Contract deployer address

## Usage Examples

### Register a Project

```clarity
(contract-call? .carbon-offset-platform register-environmental-offset-project
  u"Solar Farm Project"
  u"Large-scale solar installation generating renewable energy"
  u"California, USA"
  "renewable-energy-generation"
  u1640995200  ; 2022-01-01
  u1672531200  ; 2023-01-01
  u"https://project-docs.example.com/solar-farm"
)
```

### Purchase Credits

```clarity
(contract-call? .carbon-offset-platform execute-carbon-credit-purchase
  u1    ; batch-id
  u100  ; quantity
)
```

### Retire Credits

```clarity
(contract-call? .carbon-offset-platform execute-permanent-carbon-credit-retirement
  u1      ; project-id
  u2022   ; vintage-year
  u50     ; quantity
  u"Corporate carbon neutrality initiative"
  none    ; no beneficiary
)
```

## Security Considerations

- All project modifications require appropriate authorization
- Verification organizations must be pre-approved by platform administrators
- Credit transfers validate sufficient balances before execution
- Self-transactions and self-authorizations are prevented
- All monetary transactions use secure STX transfer functions