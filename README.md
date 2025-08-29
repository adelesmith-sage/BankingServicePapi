# Banking Service - Provider API

A Bruno collection for testing and integrating with the Sage Banking Service Provider API. This collection covers the complete banking service workflow from onboarding to offboarding.

## 🚀 Quick Start

### 1. Install Bruno
- **Download from**: [https://www.usebruno.com/downloads](https://www.usebruno.com/downloads)
- **Supported platforms**: Windows, macOS, Linux
- **Alternative**: Install via package managers:
  ```bash
  # macOS
  brew install bruno
  
  # Windows
  winget install Bruno.Bruno
  
  # Linux
  snap install bruno
  ```

### 2. Import the Collection
1. Open Bruno
2. Click **Import Collection** or use `Ctrl/Cmd + I`
3. Select the `Banking Service - Provider API.json` file
4. The collection will appear in your workspace

### 3. Set Up Environment
- Your enablement engineer will provide an environment file
- Import the environment file in Bruno
- All required variables will be pre-configured

## 📁 Collection Overview

The collection is organized into logical workflows:

- **Bank Sync** - Provider-side bank management
- **Onboarding** - Customer and account setup
- **Multi-Account Linking** - Link multiple accounts
- **Posting Statements** - Upload bank statements
- **Reauthorization** - Handle expired authorizations
- **Offboarding** - Account cleanup

## 🔧 Environment Variables

Your enablement engineer will provide these pre-configured variables:

### Provider Environment
- `_preset_provider_baseUrl` - Banking service API base URL
- `_preset_provider_apiKey` - Provider API key
- `_preset_cloudId_*` - Cloud ID authentication credentials

### Consumer Environment
- `_preset_consumer_baseUrl` - Consumer API base URL
- `_preset_consumer_xApplication` - Application identifier
- `_preset_consumer_application_signingKey` - HMAC signing key
- `_preset_consumer_bankId` - Bank identifier

## 🔄 Workflow Execution

### Onboarding Flow
1. Create organisation and company
2. Get access tokens
3. Set up bank account linking
4. Complete authorization

### Statement Posting
1. Authenticate provider
2. Post statement data
3. Verify transactions

### Multi-Account Linking
1. Check available accounts
2. Link selected accounts
3. Verify connection status

## 🧪 Testing

Each request includes test scripts that:
- Validate response codes
- Set environment variables
- Perform business logic checks

## 🚨 Troubleshooting

### Common Issues
- **Authentication errors**: Verify environment variables are loaded
- **Bank account issues**: Check bank ID and linking status
- **Statement errors**: Validate data format and required fields

### Support
Contact your Sage Banking Service Enablement Lead for assistance.

## 📚 Resources

- [Bruno Documentation](https://www.usebruno.com/docs)
- [Sage Banking Service Documentation](https://developer.sage.com/banking-service/)

---

**Note**: This collection is for testing and development. Use appropriate test environments before production.
