# Architecture & Scaffold

High-level overview of the OEC DAO Hub architecture and data flow.

## System Diagram

```
┌──────────────────────────────────────────────────────┐
│                    React Frontend                     │
│  (Vite + TypeScript + Tailwind + Wagmi + Recharts)    │
│                                                       │
│  Dashboard │ Analytics │ Governance │ Portfolio │ ...  │
└──────────┬────────────────────────┬───────────────────┘
           │                        │
           │  Blockchain            │  API Calls
           │  (Wagmi/Viem)          │  (fetch)
           ▼                        ▼
┌──────────────────┐    ┌──────────────────────────────┐
│   Sepolia RPC    │    │   Netlify Serverless Funcs   │
│   (Alchemy)      │    │   (20 endpoints)             │
│                  │    │                              │
│  - Wallet reads  │    │  - Volume analytics          │
│                  │    │  - Portfolio tracking         │
└──────────────────┘    │  - Holder information        │
                        │  - Live Coin Watch sync      │
                        └──────────┬───────────────────┘
                                   │
                                   ▼
                        ┌──────────────────────┐
                        │  PostgreSQL (Neon)    │
                        │  Drizzle ORM          │
                        │                      │
                        │  - Token snapshots    │
                        │  - Tracked tokens     │
                        │  - Historical data    │
                        │  - User watchlists    │
                        └──────────────────────┘
```

## Frontend Structure

```
client/src/
├── pages/              # Route-level page components
│   ├── dashboard.tsx    # Token overview and analytics
│   ├── analytics.tsx    # TVL, volume, protocol metrics
│   ├── governance.tsx   # DAO proposals, voting, delegation
│   ├── portfolio.tsx    # User DeFi positions
│   ├── ecosystem.tsx    # Protocol links and metrics
├── components/          # Reusable UI components
│   ├── layout.tsx       # Collapsible sidebar layout
│   ├── wallet-connect.tsx
│   ├── price-chart.tsx
│   ├── ecosystem-sidebar.tsx
│   └── ...
├── hooks/               # Custom React hooks
├── services/            # Business logic and ABIs
├── lib/                 # Wagmi config, query client
│   └── wagmi.ts
└── App.tsx              # Router and providers
```

## Backend Structure

```
server/
├── index.ts             # Express server entry
├── routes.ts            # API route definitions
├── db.ts                # Drizzle ORM connection
├── storage.ts           # Database access layer
└── services/            # External API integrations
    ├── coingecko-api.ts
    ├── alchemy-api.ts
    ├── live-coin-watch-api.ts
    └── ...

netlify/functions/       # Serverless endpoints (production)
├── token-data.ts
├── token-historical-data.ts
├── volume-analytics.ts
├── holders.ts
└── ... (20 total)

shared/
└── schema.ts            # Drizzle schema + Zod validation
```

## Data Flow

1. **Token & Market Data**: Netlify functions query Neon PostgreSQL (cached from Live Coin Watch / CoinGecko syncs) and return JSON to the frontend
3. **Governance**: Currently uses mock data for UI development; will connect to on-chain governance contracts
4. **Analytics**: Aggregated from database snapshots with protocol-level filtering

## Key Design Decisions

- **Serverless-first**: All production API traffic goes through Netlify functions, not the Express server
- **Cached data**: Token prices and history are synced to PostgreSQL on a schedule, reducing external API calls
- **Wagmi 2 + Viem**: Modern wallet stack supporting 9 wallet providers out of the box
- **Wouter routing**: Lightweight alternative to React Router (< 2KB)
