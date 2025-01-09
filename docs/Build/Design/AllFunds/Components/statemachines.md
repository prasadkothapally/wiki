# StateMachines

## lists
 - Transaction Type State Machine

## Transaction Type State Machine

State       | Description
------------|------------
Created     | The Transaction is created in the AllFunds system but has not yet been sent to a executor for processing
Sent        |  The transaction is sent to the executor for processing
Pending     | The transaction is accepted by the executor for further processing
Rejected    | The transaction has not been accepted by the executor for processing
Failed      | The transaction has been reporrted as failed by the executor.
Completed   | The transaction is completed.


### Visual
```kroki-plantuml
@startuml
[*] --> Created
[*] --> Sent
Created -> Sent
Sent -> Rejected
Sent -> Pending
Pending -> Failed
Pending -> Completed
Completed --> [*]
Failed --> [*]
Rejected --> [*]
@enduml
```