# Playground to try out various diagrams

## State Machine

```kroki-plantuml
@startuml
[*] --> Creating
Creating -> Created
Created -> Started
Started -> Stopped
Created --> [*]
Started --> [*]
Stopped --> [*]
@enduml
```
```xkroki-plantuml
@startuml
[*] --> Creating
Creating -> Created
Created -> Started
Started -> Stopped
Created --> [*]
Started --> [*]
Stopped --> [*]
@enduml
```



## Pie Chart
```mermaid
pie title Pets adopted by volunteers
    "Dogs" : 386
    "Cats" : 85
    "Rats" : 15
```
```xmermaid
pie title Pets adopted by volunteers
    "Dogs" : 386
    "Cats" : 85
    "Rats" : 15
```

## Mindmap
```mermaid
mindmap
  root((mindmap))
    Origins
      Long history
      ::icon(fa fa-book)
      Popularisation
        British popular psychology author Tony Buzan
    Research
      On effectiveness<br/>and features
      On Automatic creation
        Uses
            Creative techniques
            Strategic planning
            Argument mapping
    Tools
      Pen and paper
      Mermaid
```
```xmermaid
mindmap
  root((mindmap))
    Origins
      Long history
      ::icon(fa fa-book)
      Popularisation
        British popular psychology author Tony Buzan
    Research
      On effectiveness<br/>and features
      On Automatic creation
        Uses
            Creative techniques
            Strategic planning
            Argument mapping
    Tools
      Pen and paper
      Mermaid
```

# Sequence Diagram

```puml

@startuml
autonumber
skin rose
skinparam svgDimensionStyle false

title "Portfolio - Payment Flow"

/'
This highlights the flow of a payment flow.
'/

actor User as user
boundary App as app
boundary WebView as webview
control "Portfolio Service" as pfo
boundary "MFU Service" as mfu
control "PaymentStatusCallback" as psb
control "Android DeepLinker" as deeplink

== purchase initialization ==

user -> app : Click on purchase
app -> pfo : Purchase request sent
pfo -> mfu : Purchase request forwarded
mfu -> pfo : purchase response with payment link returned
pfo -> app : return payment link

== User proceeds with payment ==

app -> webview : Launch and navigate to Payment Link
webview -> webview : user finishes payment steps using rendered payment pages
webview -> mfu : submits payment
mfu -> webview : responds with 302 Redirect to preconfigured Payment Callback URL ( https://fintrust-dev.techwave.net/api/execution/mfu/payment-callback )

== App handled payment status ==

webview -> psb : redirect
psb -> webview : responds with 302 Redirect to preconfigured App Supported Callback URL (app://allfunds?...)
webview -> deeplink : Handle redirect
deeplink -> app : Transfers control to app with context
app -> user : displays payment status and next steps.
 
@enduml

```

# Block Diagram
```kroki-blockdiag no-transparency=false
blockdiag {
  blockdiag -> generates -> "block-diagrams";
  blockdiag -> is -> "very easy!";
  blockdiag -> is -> "also fun too!";

  blockdiag [color = "greenyellow"];
  "block-diagrams" [color = "pink"];
  "very easy!" [color = "orange"];
}
```

```
xkroki-blockdiag no-transparency=false
blockdiag {
  blockdiag -> generates -> "block-diagrams";
  blockdiag -> is -> "very easy!";
  blockdiag -> is -> "also fun too!";

  blockdiag [color = "greenyellow"];
  "block-diagrams" [color = "pink"];
  "very easy!" [color = "orange"];
}
```