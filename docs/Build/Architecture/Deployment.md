# Deployment

This page describes various aspects of the deployment architecture for Fintrust apps.

## Namespaces

The following namespaces are used in Kubernetes.

```kroki-plantuml
@startuml
package AllFunds { 
  [AllFunds Component .. 1]
  [AllFunds Component .. 2]
  [AllFunds Component .. N]
}

package Accounting { 
  [Accounting Component .. 1]
  [Accounting Component .. 2]
  [Accounting Component .. N]
}

package Kestra { 
  [Kestra Scheduler]
}
@enduml
```

namespace     |purpose
--------------|--------
AllFunds      |Used for deployment of all application components related to AllFunds
Accounting    |Used for deployment of all application components related to Accounting
Kestra        |Used for deployment of the Kestra scheduler components
Fintrust-Data |Only used on lower environments (such as local, auto, stage etc. ) Supports deployment of stateful components such as Postgres, Mongo and RabbitMQ

## Components

The application comprises of the following components

```kroki-plantuml
@startuml

frame AllFunds { 
  component af-profile{
  }
  component af-funds{
  }
  component af-portfolio{
  }
  component af-notifications{
  }
  component af-eventpublisher{
  }
  component af-dlqprocessor{
  }
}

frame Accounting {
  component acc-api{
  }
  component acc-bo{
  }
  component acc-analytics{
  }
}

frame Kestra {
 component KestraScheduler{
 }
}

@enduml
```

## Interactions

```kroki-plantuml
@startuml

frame Kubernetes {

package AllFunds { 
  HTTP1 - [Any AllFunds Component]
  MQ1 - [Any AllFunds Component]
  OUT1 -- [Any AllFunds Component]
}

package Accounting {
  HTTP2 - [Any Accounting Component]
  MQ2 - [Any Accounting Component]
  OUT2 -- [Any Accounting Component]
}

package Kestra {
 component KestraScheduler {
   [Any Job]
 }
}

component FluentD {
}

}

database Postgres {
  [accounting schema]
  [common schema]
}

database MongoDB {
  [any collection]
}

queue RabbitMQ {
  [any queue]
}

component OpenObserve {
}

  [Any Accounting Component] --> [accounting schema]
  [Any Accounting Component] --> [common schema]
  [Any AllFunds Component] --> [common schema]
  [Any AllFunds Component] --> [any collection]
  MQ1 --> [any queue]
  MQ2 -> [any queue]
  OUT1 -> FluentD 
  OUT2 -> FluentD 
  FluentD --> OpenObserve
  [Any Job] --> HTTP1
  [Any Job] --> HTTP2

@enduml
```



