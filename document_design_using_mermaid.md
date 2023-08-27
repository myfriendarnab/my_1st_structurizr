# Document your design using mermaid

- [Document your design using mermaid](#document-your-design-using-mermaid)
  - [Document your Domain](#document-your-domain)
  - [Visualize Application and User Flows](#visualize-application-and-user-flows)
  - [Model your architecture using C4 model](#model-your-architecture-using-c4-model)
  - [Design database schema using erDiagram](#design-database-schema-using-erdiagram)
  - [Visualize code flows using sequence diagrams](#visualize-code-flows-using-sequence-diagrams)
  - [Design and refactor your application using class diagram(code level)](#design-and-refactor-your-application-using-class-diagramcode-level)


```mermaid
stateDiagram-v2 
    direction LR
    Domain_Modeling --> App&User_Flows

    App&User_Flows --> c4
    c4 --> ER
    ER --> code_flows
    code_flows --> code
```

## Document your Domain

- use classDiagram
- decide relationships between entities (association, composition, aggregation) 

    |  Association | Composition  | Aggregation  |
    |---|---|---|
    | There’s no owner of the relationship though, and they can exist completely independently of one another  | There’s an owner of the relationship, but if the parent is deleted, the child can still remain  | Similarly to aggregations, there’s an owner of the relationship. However, if the parent is deleted, the child must be deleted, too  |
- Define Inheritance/ Interfaces

```mermaid
classDiagram
    note "From Duck till Zebra"
    Animal <|-- Duck
    note for Duck "can fly\ncan swim\ncan dive\ncan help in debugging"
    Animal <|-- Fish
    Animal <|-- Zebra
    Animal : +int age
    Animal : +String gender
    Animal : +isMammal()
    Animal : +mate()
    class Duck{
        +String beakColor
        +swim()
        +quack()
    }
    class Fish{
        -int sizeInFeet
        -canEat()
    }
    class Zebra{
        +bool is_wild
        +run()
    }
```


## Visualize Application and User Flows

```mermaid
sequenceDiagram;
actor Browser;
Note right of Browser: Sequence diagrams are high-level views of a process;
participant Sign Up Service;
participant User Service;
participant Kafka;
Browser->>Sign Up Service: GET /sign_up;
Sign Up Service-->>Browser: 200 OK (HTML page);
```

- create sequence diagrams to
  - define actor models
  - define interactions
  - alternate paths and branching logics
  - annotate diagrams with sequence numbers

## Model your architecture using C4 model

```mermaid
C4Context
      Enterprise_Boundary(b0, "BankBoundary0") {
        Person(customerA, "Banking Customer A", "A customer of the bank, with personal bank accounts.")
        Person(customerB, "Banking Customer B")
        Person_Ext(customerC, "Banking Customer C", "desc")

        Person(customerD, "Banking Customer D", "A customer of the bank, <br/> with personal bank accounts.")

        System(SystemAA, "Internet Banking System", "Allows customers to view information about their bank accounts, and make payments.")

        Enterprise_Boundary(b1, "BankBoundary") {

          SystemDb_Ext(SystemE, "Mainframe Banking System", "Stores all of the core banking information about customers, accounts, transactions, etc.")

          System_Boundary(b2, "BankBoundary2") {
            System(SystemA, "Banking System A")
            System(SystemB, "Banking System B", "A system of the bank, with personal bank accounts. next line.")
          }

          System_Ext(SystemC, "E-mail system", "The internal Microsoft Exchange e-mail system.")
          SystemDb(SystemD, "Banking System D Database", "A system of the bank, with personal bank accounts.")

          Boundary(b3, "BankBoundary3", "boundary") {
            SystemQueue(SystemF, "Banking System F Queue", "A system of the bank.")
            SystemQueue_Ext(SystemG, "Banking System G Queue", "A system of the bank, with personal bank accounts.")
          }
        }
      }

      BiRel(customerA, SystemAA, "Uses")
      BiRel(SystemAA, SystemE, "Uses")
      Rel(SystemAA, SystemC, "Sends e-mails", "SMTP")
      Rel(SystemC, customerA, "Sends e-mails to")

      UpdateElementStyle(customerA, $fontColor="red", $bgColor="grey", $borderColor="red")
      UpdateRelStyle(customerA, SystemAA, $textColor="blue", $lineColor="blue", $offsetX="5")
      UpdateRelStyle(SystemAA, SystemE, $textColor="blue", $lineColor="blue", $offsetY="-10")
      UpdateRelStyle(SystemAA, SystemC, $textColor="blue", $lineColor="blue", $offsetY="-40", $offsetX="-50")
      UpdateRelStyle(SystemC, customerA, $textColor="red", $lineColor="red", $offsetX="-50", $offsetY="20")

      UpdateLayoutConfig($c4ShapeInRow="3", $c4BoundaryInRow="1")
```

- create context diagram
- create container diagram with clear system boundaries (using sub graphs)
- strucuture component diagrams (optional, should be joint responsibility of dev lead)
- structure code diagrams (optional, should be primary responsibilities of lead/devs)

## Design database schema using erDiagram

```mermaid
erDiagram
    CUSTOMER ||--o{ ORDER : places
    CUSTOMER {
        string name
        string custNumber
        string sector
    }
    ORDER ||--|{ LINE-ITEM : contains
    ORDER {
        int orderNumber
        string deliveryAddress
    }
    LINE-ITEM {
        string productCode
        int quantity
        float pricePerUnit
    }
```

- When writing an architecture decision record (ADR) for a brand-new service, you may optionally include an ERD to show a snapshot of the database design at that point in time
- Add 
  - enrity relationships (like zero to many etc)
  - enrich schema with keys
  - comment your columns

## Visualize code flows using sequence diagrams

```mermaid
sequenceDiagram
    par Alice to Bob
        Alice->>Bob: Hello guys!
    and Alice to John
        Alice->>John: Hello guys!
    end
    Bob-->>Alice: Hi Alice!
    John-->>Alice: Hi Alice!
```

## Design and refactor your application using class diagram(code level)

- component/module level class diagram
- refactor using SOLID