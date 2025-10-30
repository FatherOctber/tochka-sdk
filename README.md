# Tochka Bank TypeScript SDK

A comprehensive TypeScript SDK for Tochka Bank API, providing easy access to all banking services including acquiring, invoicing, open banking, payments, SBP (Fast Payment System), and webhooks.

## Installation

```bash
npm install tochka-sdk
```

## Quick Start

```typescript
import { TochkaBankSDK } from 'tochka-sdk';

const sdk = new TochkaBankSDK({
  jwtToken: process.env.TOCHKA_JWT_TOKEN,
  clientId: process.env.TOCHKA_CLIENT_ID,
  isDevelopment: true, // Use sandbox environment
});

// Create an invoice
const invoice = await sdk.Invoice.createInvoice("v1.0", {
  customerCode: "300000092",
  amount: 100000,
  description: "Test invoice"
});

// Get payment status
const status = await sdk.Invoice.getInvoicePaymentStatus("v1.0", "300000092", "invoice-123");
```

## Configuration

### SDK Options

```typescript
interface TochkaBankSDKOptions {
  jwtToken: string;        // JWT Bearer token for authentication
  clientId: string;        // Client ID
  apiVersion?: string;     // API version (default: "v1.0")
  isDevelopment?: boolean; // Use sandbox environment (default: false)
  timeout?: number;        // Request timeout in milliseconds (default: 30000)
}
```

### Environment Variables

```bash
TOCHKA_JWT_TOKEN=your_jwt_token_here
TOCHKA_CLIENT_ID=your_client_id_here
```

## API Domains

The SDK is organized into domain-specific modules:

### Acquiring
Payment operations, subscriptions, and receipts
```typescript
// Create payment operation
const payment = await sdk.Acquiring.createPaymentOperation("v1.0", {
  amount: 100000,
  description: "Payment for order #123",
  // ... other parameters
});

// Get payment status
const paymentInfo = await sdk.Acquiring.getPaymentOperationInfo("v1.0", "payment-id");

// Create subscription
const subscription = await sdk.Acquiring.createSubscription("v1.0", {
  // subscription parameters
});
```

### Invoice
Billing and invoice management
```typescript
// Create invoice
const invoice = await sdk.Invoice.createInvoice("v1.0", {
  customerCode: "300000092",
  amount: 100000,
  description: "Invoice for services"
});

// Get invoice status
const status = await sdk.Invoice.getInvoicePaymentStatus("v1.0", "customer-code", "invoice-id");
```

### Open Banking
Account and statement queries
```typescript
// Get accounts
const accounts = await sdk.OpenBanking.getAccounts("v1.0");

// Get account statements
const statements = await sdk.OpenBanking.getAccountStatements("v1.0", {
  accountId: "account-id",
  dateFrom: "2024-01-01",
  dateTo: "2024-01-31"
});
```

### Payment
Payment requests and status tracking
```typescript
// Create payment request
const payment = await sdk.Payment.createPaymentRequest("v1.0", {
  // payment parameters
});

// Get payment status
const status = await sdk.Payment.getPaymentStatus("v1.0", "payment-id");
```

### SBP (Fast Payment System)
QR codes and fast payments
```typescript
// Create QR code
const qrCode = await sdk.SBP.createQRCode("v1.0", {
  amount: 100000,
  description: "Payment via SBP"
});

// Get payment status
const status = await sdk.SBP.getPaymentStatus("v1.0", "payment-id");
```

### Webhook
Event notifications and webhook management
```typescript
// Register webhook
const webhook = await sdk.Webhook.registerWebhook("v1.0", {
  url: "https://your-domain.com/webhook",
  events: ["payment.completed", "payment.failed"]
});

// Get webhook list
const webhooks = await sdk.Webhook.getWebhooks("v1.0");
```

## Environment Support

The SDK supports both production and sandbox environments:

- **Production**: `https://enter.tochka.com/uapi`
- **Sandbox**: `https://enter.tochka.com/sandbox/v2`

Set `isDevelopment: true` in the SDK options to use the sandbox environment.

## Error Handling

All API methods return promises and can throw errors. Always wrap calls in try-catch blocks:

```typescript
try {
  const invoice = await sdk.Invoice.createInvoice("v1.0", invoiceData);
  console.log('Invoice created:', invoice);
} catch (error) {
  console.error('Failed to create invoice:', error);
}
```

## TypeScript Support

The SDK is written in TypeScript and includes full type definitions. All API methods, parameters, and responses are fully typed for the best development experience.

## API Reference

For detailed API documentation, refer to the [Tochka Bank API documentation](https://enter.tochka.com/doc/).

## Development

### Building from Source

```bash
# Install dependencies
npm install

# Build the project
npm run build

# Generate API client from OpenAPI spec
npm run generateTochkaApi
```

### Project Structure

```
src/
├── domain/           # Domain-specific classes
│   ├── tochka-acquiring.ts
│   ├── tochka-invoice.ts
│   ├── tochka-openbanking.ts
│   ├── tochka-payment.ts
│   ├── tochka-sbp.ts
│   ├── tochka-webhook.ts
│   └── tochka-base.ts
├── tochka-api/       # Auto-generated API client
│   └── tochka-api.ts
└── index.ts          # Main SDK entry point
```

## License

MIT

## Contributing

Contributions are welcome! Please read the contribution guidelines before submitting pull requests.

## Support

For SDK-related issues, please open an issue on GitHub.
For API-related questions, refer to the official Tochka Bank documentation.