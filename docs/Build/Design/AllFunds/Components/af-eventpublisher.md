# Event Publisher

<span dir="">An af-event-publisher component will monitor the verification collection in the af-profile service. If there is any data inserted in that verification collection, AF-Event-Publisher will consume the data and publish the message to RabbitMQ based on the routing key by adding a resume token in the payload.
  </span>

# Interface

## Messaging
### Exchanges

#### Notification Exchanges

| Exchange | Routing Key | Headers |  |
|----------|-------------|---------|--|
| notification-exchange | rk.email.otp  | content_type=application/json |  
| notification-exchange | rk.mobile.otp | content_type=application/json |  

# Diagrams

Data flow diagram

## Example diagram

```mermaid
flowchart TD
   
```



### Dictionary

#### Tables

# Build

| Aspect | Value |
|--------|-------|
| Artifacts |  |
| Location |  |

# Deployment

# Security

# Scalability

# Resilience