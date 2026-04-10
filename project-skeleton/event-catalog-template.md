# Event Catalog Template

## Event overview

| Event Name | Version | Producer | Consumer(s) | Trigger | Delivery | Idempotency Key | Schema |
|---|---|---|---|---|---|---|---|
| `order.created.v1` | `v1` | `ordering-service` | `inventory-service` | order persisted | at-least-once | `orderId` | `./schemas/order-created-v1.json` |

## Event detail template
- Event name
- Version
- Producer
- Business meaning
- Trigger
- Delivery assumptions
- Payload
- Field contract
- Security / privacy
- Change policy
