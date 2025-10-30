# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a TypeScript SDK for Tochka Bank APIs, providing a unified interface to access various banking services including acquiring, invoicing, open banking, payments, SBP (Fast Payment System), and webhooks.

## Build and Development Commands

- `yarn build` - Compile TypeScript to JavaScript in the `dist/` directory
- `tsc` - Direct TypeScript compilation (equivalent to build)

## Architecture

### Core Structure

The SDK follows a domain-driven architecture with:

1. **Main SDK Class** (`src/index.ts`): `TochkaBankSDK` - Central aggregator class that provides access to all domain modules
2. **Domain Classes** (`src/domain/`): Separate classes for each API domain, all extending `TochkaBankDomainBase`
3. **Generated API Client** (`src/tochka-api/`): Auto-generated from OpenAPI spec (`spec/tochka-api-spec.json`)

### Domain Modules

Each domain class in `src/domain/` wraps specific Tochka Bank API functionality:

- **TochkaBankAcquiring**: Payment operations, subscriptions, receipts, two-phase payments
- **TochkaBankInvoice**: Billing and invoice management
- **TochkaBankOpenBanking**: Account and statement queries
- **TochkaBankPayment**: Payment requests and status tracking
- **TochkaBankSBP**: Fast payment system QR codes and operations
- **TochkaBankWebhook**: Event notifications and webhook management

### Base Class Pattern

All domain classes extend `TochkaBankDomainBase` which provides:
- Shared API client instance
- API version management
- Client ID access
- Common configuration

### Environment Configuration

The SDK supports both production and sandbox environments:
- Production: `https://enter.tochka.com/uapi`
- Sandbox: `https://enter.tochka.com/sandbox/v2`

### Authentication

Uses JWT Bearer token authentication passed through the main SDK constructor and automatically applied to all API requests.

## Key Files

- `src/index.ts` - Main SDK entry point and aggregator class
- `src/domain/tochka-base.ts` - Base class for all domain modules
- `src/tochka-api/tochka-api.ts` - Generated API client from OpenAPI spec
- `spec/tochka-api-spec.json` - OpenAPI specification used to generate the client
- `tsconfig.json` - TypeScript configuration targeting ES2016/CommonJS

## Generated Code

The `src/tochka-api/` directory contains auto-generated TypeScript code from the OpenAPI specification. Do not manually edit these files as they will be overwritten when the API client is regenerated.