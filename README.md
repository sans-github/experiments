# Onsemble<>DistributionCenter
## Bulk catalog ingestion
```mermaid 
---
title: Entire catalog ingestion - one time
---
    sequenceDiagram
      DistributionCenter->>+OnsembleCatalog: Onboard catalog data
       Note over DistributionCenter,OnsembleCatalog: Batch process, async process
```

## Add a new item
```mermaid 
---
title: As new item arrives
---
    sequenceDiagram
      DistributionCenter->>+OnsembleCatalog: Add a new item
       Note over DistributionCenter,OnsembleCatalog: API
```

## Update existing item
```mermaid 
---
title: Update an item or discontinue
---
    sequenceDiagram
      DistributionCenter->>+OnsembleCatalog: Update existing item
       Note over DistributionCenter,OnsembleCatalog: API call
```

## Track price and availability
```mermaid 
---
title: Price and availability updates
---
    sequenceDiagram
      DistributionCenter->>+OnsembleInvetory: Update price and availability
       Note over DistributionCenter,OnsembleInvetory: API call, For search and Browse
```
## Lock in price and availability
```mermaid 
---
title: Price and availability updates
---
    sequenceDiagram
      participant Contractor
      participant Onsemble
      participant DistributionCenter
      Contractor->>+ Onsemble: Place order
      Onsemble->>DistributionCenter: Get price and availability
      DistributionCenter-->>Onsemble: Price and availability
      Onsemble->>DistributionCenter: Deduct item in inventory
      Onsemble ->>Onsemble:Place order
      Onsemble ->>-Contractor: Confirm order
```


# Onsemble<>customer
## Order journey
```mermaid
---
title: Order journey
---
    flowchart TB
      Contractor(Contractor)
      subgraph Discovery
        Project(Project)
        OnsembleCatalog(Onsemble Catalog)
        OnsembleQuoteSystem(Onsemble Quote system)
      end
      subgraph Checkout
        OnsembleCart(Onsemble Cart)
        CheckoutNode(Onsemble Checkout)
        Store(Store)
      end
      Contractor -->|Review requirements| Project
      Contractor -->|Search and Browse| OnsembleCatalog
      Contractor -->|Prepare Quotes| OnsembleQuoteSystem
      OnsembleQuoteSystem -->|Customer reviews and approves quote| OnsembleCart
      OnsembleCart --> CheckoutNode
      Contractor -->|Pick up item| Store
```
