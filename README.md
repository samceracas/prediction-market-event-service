# prediction-market-event-service

Owns the event and market data for Prediction Market. Handles creating and reading
`Event -> Market -> Asset` (for example: "Will France win the World Cup?" leads to
"France vs Brazil" leads to "France" / "Brazil"), and publishes changes to RabbitMQ so
trade-service can keep its own synced copy up to date.

Built with [Hono](https://hono.dev/) and [Prisma](https://www.prisma.io/) (Postgres).

## Endpoints

- `POST /event/create` - create an event with its markets and assets
- `GET /event/list` - paginated list of events
- `GET /event/details?id=` - one event with its markets/assets
- `GET /event/sync/full` - full, unpaginated dump used by trade-service to
  reconcile its shadow tables on (re)connect

## Running

```
npm install
npm run dev
```

Runs on `http://localhost:3001` by default (configurable via `PORT`). Requires
`DATABASE_URL` and `RABBITMQ_URL` in `.env`.
