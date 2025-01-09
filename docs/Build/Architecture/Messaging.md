# Messaging

This page describes various aspects of the messaging architecture for Fintrust apps.

## Retries and Dead letter processing

```kroki-plantuml
@startuml
  
  component Publisher1 {
  }
  
  component Publisher2 {
  }

  component Subscriber1 {
  }
  
  component Subscriber2 {
  }
  
  component DLQProcessor {
  }

  queue Exchange1 {
  }

  queue Queue1 {
  }
  
  queue Exchange2 {
  }

  queue Queue2 {
  }
  
  
  queue RetryQueue {
  }
  
  queue DLQ {
  }

  Publisher1 --> Exchange1
  Exchange1 --> Queue1
  Queue1 --> Subscriber1
  Queue1 -> RetryQueue
  
  Publisher2 --> Exchange2
  Exchange2 --> Queue2
  Queue2 --> Subscriber2
  RetryQueue <- Queue2
  
  Queue1 <- DLQProcessor
  Queue2 <- DLQProcessor
  
  DLQProcessor --> DLQ

  RetryQueue --> DLQProcessor

  
@enduml
```

 - Publisher puts a message on an Exchange
 - Exchange routes the message to a destination queue based on bindings and routing keys
 - Subscriber listens on the queue and picks up the message for processing
 - When subcriber finishes processing the message successfully, manually ACK's so that the message is removed from the queue
 - When subscriber fails processing the message, message is not ACK'ed and after a fixed number of retries, message is moved to the retry-queue.
 - The DLQ processor listens on the RetryQueue and moves the message back to the source Queue for a Retry.
 - If the message cannot be retried after a configured number of retries, the message is moved to the DeadLetterQueue. No processing is attempted after this.

This flow presented above is simplified for a high level understanding. For a deeper understanding on this topic, please see the DLQProcessor component.
