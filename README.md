# Banking Service - Provider API

A comprehensive Bruno collection for Sandbox testing and integrating with the Sage Banking Service Provider API. This collection contains all the necessary requests to test the complete banking service workflow, from onboarding to statement posting and offboarding.

## 📋 Table of Contents

- [Overview](#overview)
- [Collection Structure](#collection-structure)
- [Prerequisites](#prerequisites)
- [Environment Setup](#environment-setup)
- [Getting Started](#getting-started)
- [Workflow Flows](#workflow-flows)
- [API Endpoints](#api-endpoints)
- [Authentication](#authentication)
- [Testing](#testing)
- [Troubleshooting](#troubleshooting)

## 🎯 Overview

The Banking Service Provider API enables financial institutions and aggregators to integrate with Sage's banking platform. This collection provides a complete testing suite covering all major workflows including:

- **Bank Sync**: Provider-side bank management operations
- **Onboarding**: Complete customer and bank account setup process
- **Multi-Account Linking**: Linking multiple bank accounts to a single customer
- **Posting Statements**: Uploading and managing bank statements
- **Reauthorization**: Handling expired or revoked authorizations
- **Offboarding**: Proper cleanup and account removal

## 📁 Collection Structure

```
Banking Service - Provider API/
├── Bank Sync/
│   ├── POST /token
│   ├── POST/ banks toCreate
│   ├── POST/ banks toUpdate
│   └── POST/ remove bank
├── Onboarding/
│   ├── Banking Service Onboarding/
│   │   ├── 1: POST /organisations
│   │   ├── 2: GET /accessToken - Company
│   │   ├── 3: GET /bank
│   │   ├── 4: GET /indirectlinkaccount
│   │   ├── 5: POST /notification
│   │   ├── 6: GET /auth
│   │   ├── 7: POST /token
│   │   └── 8: PATCH /authorisations
│   ├── Banking Service Offboarding/
│   │   ├── 13: DELETE /bankaccount
│   │   ├── 14: POST /notification
│   │   └── 15: GET /bankaccountId
│   └── Post to Banking Service/
│       ├── 9: GET /indirectlinkaccount (RESULT)
│       ├── 10: POST /bankaccounts
│       ├── 11: POST /notification
│       ├── 12: GET /bankaccountId
│       ├── POST /accountqueries
│       └── POST /accountqueries_1
├── Multi-Account Linking/
│   └── Multiaccount linking/
│       ├── 13: GET /availableaccounts
│       ├── 14: GET /availableaccounts 2nd time
│       ├── 15: POST /linkavailablebankaccount
│       ├── 16: POST /linkavailablebankaccount02
│       └── 17: CheckAccountsStatus
├── Posting Statements/
│   ├── Banking Service Offboarding/
│   │   ├── 17: DELETE /bankaccount
│   │   ├── 18: POST /notification
│   │   └── 19: GET /bankaccountId
│   └── Posting Statements/
│       ├── 13: POST /token
│       ├── 14: POST /statements
│       ├── 15: GET /statements
│       └── 16: GET /transactions (startIndex, endIndex)
├── Reauthorization/
│   └── Reauth/
│       ├── 13: POST /token
│       ├── 14: POST /statements
│       ├── 15: GET /reauthaccount
│       ├── 16: POST /notification
│       ├── 17: GET /authrefresh
│       ├── 18: POST /token
│       ├── 19: PATCH /authorisations
│       └── 20: GET /bankaccountId
└── Banking Service Offboarding/
    ├── 20: DELETE /bankaccount
    ├── 21: POST /notification
    └── 22: GET /bankaccountId
```

## 🔧 Prerequisites

Before using this collection, ensure you have:

- **Bruno** installed and configured
- **Sage Banking Service** account and credentials
- **Cloud ID** authentication credentials
- **Provider API Key** for banking service operations
- **Consumer application** credentials and signing keys
- **Webhook endpoints** configured for notifications

## ⚙️ Environment Setup

### Required Environment Variables

#### Provider Environment
```bash
_preset_provider_baseUrl=https://api.bankingservice.sage.com
_preset_provider_apiKey=your_provider_api_key
_preset_cloudId_baseUrl=https://auth.sage.com
_preset_cloudId_clientId=your_client_id
_preset_cloudId_clientSecret=your_client_secret
_preset_cloudId_audience=your_audience
```

#### Consumer Environment
```bash
_preset_consumer_baseUrl=https://snd01us.sagebankdrive.com/api/v1
_preset_consumer_xApplication=sage.integrate.myproduct
_preset_consumer_application_signingKey=your_signing_key
_preset_consumer_bankId=your_bank_id
```

### Dynamic Variables

The collection automatically manages these variables during execution:
- `provider_auth_cloudId`: OAuth token for provider operations
- `consumer_organisationId`: Created organisation ID
- `consumer_companyId`: Created company ID
- `consumer_jwt`: JWT token for consumer operations
- `consumer_bankAccountId`: Created bank account ID
- `consumer_indirect_accountName`: Account name from indirect linking
- `consumer_indirect_accountKey`: Account key from indirect linking
- `consumer_indirect_accountIdentifier`: Account identifier from indirect linking
- `consumer_indirect_bankIdentifier`: Bank identifier from indirect linking
- `consumer_indirect_bankAccountExternalId`: External account ID
- `consumer_indirectPollRoute`: Polling route for indirect linking
- `bankAccountCandidateId01`: First available account candidate
- `bankAccountCandidateId02`: Second available account candidate
- `statementId`: Created statement ID
- `uniqueId_1`: Generated unique ID for transactions
- `uniqueId_2`: Generated unique ID for transactions

## 🚀 Getting Started

### 1. Import the Collection
- Open Bruno
- Import the `Banking Service - Provider API.json` file
- Set up your environment variables

### 2. Configure Authentication
- Update the environment variables with your actual credentials
- Ensure your Cloud ID credentials are valid
- Verify your provider API key has the necessary permissions

### 3. Set Up Webhook Endpoints
- Configure your notification endpoints for:
  - `/notification` - General notifications
  - `/auth` - Authentication callbacks
  - `/authrefresh` - Reauthorization callbacks

### 4. Test the Workflow
- Start with the **Bank Sync** folder to verify provider access
- Proceed through the **Onboarding** workflow
- Test **Multi-Account Linking** if needed
- Verify **Posting Statements** functionality
- Test **Reauthorization** scenarios
- Complete with **Offboarding** procedures

## 🔄 Workflow Flows

### Complete Onboarding Flow
1. **Create Organisation & Company** (1: POST /organisations)
2. **Get Access Token** (2: GET /accessToken - Company)
3. **Get Bank Information** (3: GET /bank)
4. **Initiate Indirect Linking** (4: GET /indirectlinkaccount)
5. **Handle Notifications** (5: POST /notification, 6: GET /auth)
6. **Provider Authentication** (7: POST /token)
7. **Update Authorizations** (8: PATCH /authorisations)
8. **Complete Account Setup** (9-12: Banking Service Integration)

### Multi-Account Linking Flow
1. **Check Available Accounts** (13: GET /availableaccounts)
2. **Re-check for Updates** (14: GET /availableaccounts 2nd time)
3. **Link First Account** (15: POST /linkavailablebankaccount)
4. **Link Second Account** (16: POST /linkavailablebankaccount02)
5. **Verify Account Status** (17: CheckAccountsStatus)

### Statement Posting Flow
1. **Authenticate Provider** (13: POST /token)
2. **Post Statement** (14: POST /statements)
3. **Retrieve Statement** (15: GET /statements)
4. **Get Transactions** (16: GET /transactions)

### Reauthorization Flow
1. **Authenticate Provider** (13: POST /token)
2. **Post Reauthorization Statement** (14: POST /statements)
3. **Initiate Reauthorization** (15: GET /reauthaccount)
4. **Handle Notifications** (16: POST /notification, 17: GET /authrefresh)
5. **Re-authenticate Provider** (18: POST /token)
6. **Update Authorization Status** (19: PATCH /authorisations)
7. **Verify Account Status** (20: GET /bankaccountId)

## 🔌 API Endpoints

### Provider Endpoints
- **Base URL**: `{{_preset_provider_baseUrl}}/v1`
- **Authentication**: OAuth 2.0 with Cloud ID
- **Headers**: `x-api-key`, `Authorization`

### Consumer Endpoints
- **Base URL**: `{{_preset_consumer_baseUrl}}`
- **Authentication**: JWT tokens with HMAC signing
- **Headers**: `x-application`, `Authorization`, `x-signature`, `x-nonce`

### Key Endpoints
- **Banks**: `/v1/banks` - Bank management operations
- **Authorizations**: `/v1/authorisations` - Authorization management
- **Statements**: `/v1/statements` - Statement posting and retrieval
- **Account Queries**: `/v1/accountqueries` - Account information queries

## 🔐 Authentication

### Provider Authentication
- **Method**: OAuth 2.0 Client Credentials
- **Endpoint**: `{{_preset_cloudId_baseUrl}}/oauth/token`
- **Grant Type**: `client_credentials`
- **Required Fields**: `client_id`, `client_secret`, `audience`

### Consumer Authentication
- **Method**: HMAC-SHA1 signing
- **Algorithm**: SHA1 with Base64 encoding
- **Required Headers**: `x-signature`, `x-nonce`
- **Signing Process**: Method + URL + Query + Body + Nonce

### HMAC Signing Process
1. Generate unique nonce (UUID v4)
2. Create signature base: `METHOD&URL&QUERY&NONCE`
3. Sign with HMAC-SHA1 using application signing key
4. Include signature and nonce in request headers

## 🧪 Testing

### Test Scripts
Each request includes comprehensive test scripts that:
- Verify response status codes
- Validate response data structure
- Set environment variables for subsequent requests
- Perform business logic validation

### Example Test
```javascript
// Assert response code 200
test("Response status code is 200", function () {
    expect(res.getStatus()).to.equal(200);
});

// Validate bank account status
test("Bank account is active", function () {
    var jsonData = res.getBody();
    expect(jsonData.status).to.eql("active");
});
```

### Environment Variable Management
The collection automatically manages environment variables:
- **Request Scripts**: Set variables before sending requests
- **Response Scripts**: Extract and store response data
- **Cross-Request Usage**: Variables persist across the entire workflow

## 🚨 Troubleshooting

### Common Issues

#### Authentication Errors
- Verify Cloud ID credentials are correct
- Check provider API key permissions
- Ensure consumer signing key is valid
- Verify audience configuration

#### Bank Account Issues
- Confirm bank ID exists and is enabled
- Check account linking status
- Verify indirect linking configuration
- Ensure proper notification endpoints

#### Statement Posting Errors
- Validate statement format and required fields
- Check account authorization status
- Verify transaction unique IDs
- Ensure proper currency codes

### Debug Steps
1. **Check Environment Variables**: Verify all required variables are set
2. **Review Request Logs**: Check Bruno's request/response logs
3. **Validate Credentials**: Test authentication endpoints independently
4. **Check Permissions**: Ensure API keys have necessary scopes
5. **Verify Endpoints**: Confirm webhook URLs are accessible

### Support
For additional assistance:
- Contact your Sage Banking Service Enablement Lead
- Review the API documentation for detailed endpoint information
- Check the collection documentation for specific request details

## 📚 Additional Resources

- **Sage Banking Service Documentation**: [Link to documentation]
- **API Reference**: [Link to API reference]
- **Integration Guide**: [Link to integration guide]
- **Support Portal**: [Link to support portal]

## 🔄 Version History

- **Version 1**: Initial collection with complete banking service workflows
- **Features**: Onboarding, multi-account linking, statement posting, reauthorization, offboarding

---

**Note**: This collection is designed for testing and development purposes. Ensure you have proper authorization and are using appropriate test environments before running these requests against production systems.
