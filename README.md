# GX Exchange TypeScript Examples

Sample scripts demonstrating how to interact with the GX Exchange API using TypeScript. Covers order placement, EIP-712 signing, and frontend value computations.

## What It Does

These examples serve as reference implementations for building TypeScript-based trading tools, bots, and frontends on GX Chain. They use `viem` for wallet signing and `axios` for API communication.

## Quick Start

```bash
git clone https://github.com/GX-EXCHANGE/gx-ts-examples.git
cd gx-ts-examples
npm install
```

## Examples

| File | Description |
|---|---|
| `OrderExample.tsx` | Place limit and trigger orders with EIP-712 signing |
| `Signing.tsx` | EIP-712 structured data signing for GX Chain L1 actions |
| `LiquidationPx.tsx` | Compute liquidation prices for open positions |

### Place a Limit Order

```typescript
import { signStandardL1Action } from "./Signing";
import { privateKeyToAccount } from "viem/accounts";

const wallet = privateKeyToAccount("0x...");
const order = { a: assetId, b: true, p: "1100", s: "0.2", r: false, t: { limit: { tif: "Gtc" } } };
const signature = await signStandardL1Action(wallet, order, chainId);
await axios.post(baseUrl + "/exchange", { action: { type: "order", orders: [order] }, signature });
```

### Query Mid Prices

```typescript
const response = await axios.post(baseUrl + "/info", { type: "allMids" });
console.log(response.data); // { "ETH": "1850.5", "BTC": "43200.0", ... }
```

## Configuration

Set the API base URL in your scripts:

- **Mainnet:** `https://api.gx.exchange`
- **Testnet:** `https://api.gx-exchange-testnet.xyz`

## Requirements

- Node.js 18+

## Documentation

- [TypeScript SDK Reference](https://docs.gx.exchange/for-developers/api/typescript-sdk)
- [API Reference](https://docs.gx.exchange/for-developers)
- [Trading Guide](https://docs.gx.exchange/trading)

## Links

- [GX Exchange GitHub](https://github.com/GX-EXCHANGE)
- [GX Exchange](https://gx.exchange)

## License

MIT
