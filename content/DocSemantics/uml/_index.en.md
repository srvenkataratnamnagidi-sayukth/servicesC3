---
title: "UML Diagrams"
tags : ["Composing"]
pre: "<b>4. </b>"
---
The Unified Modeling Language (UML) is a general-purpose, developmental, modeling language in the field of software engineering that is intended to provide a standard way to visualize the design of a system

An entity–relationship model (or ER model) describes interrelated things of interest in a specific domain of knowledge.
A basic ER model is composed of entity types (which classify the things of interest) and specifies relationships that can exist between entities (instances of those entity types).

Mermaid lets you represent diagrams using text and code. 
This simplifies maintianing complex diagrams. 
It is a Javascript based diagramming and charting tool that renders Markdown-inspired text definitions to create and modify diagrams dynamically. 
The main purpose of Mermaid is to help Documentation catch up with Development.

Diagramming and documentation costs precious developer time and gets outdated quickly. 
But not having diagrams or docs ruins productivity and hurts organizational learning.
Mermaid addresses this by cutting the time, effort and tooling that is required to create modifiable diagrams and charts, for smarter and more reusable content. 
Mermaid, as a text-based diagramming tool allows for quick and easy updates, it can also be made part of production scripts (and other pieces of code), to make documentation much easier. 
With Mermaid less time needs to be spent on making diagrams, as a separate documentation task.

## Mermaid Supported Diagrams
1. Flowchart
1. Sequence
1. Gantt
1. Class
1. Git Graph (Beta)
1. Entity Relationship
1. User Journey

Please go over the [Mermaid](https://mermaid-js.github.io/mermaid) Documentation to learn more about the Syntax and Semantics

## Specific Digraming Guidelines
Agreed buidelines for Digraming are as follows 
### Flowchart
1. Start and Stop State nodes should be represented as Circles 
{{<mermaid align="left">}}
graph LR 
    s1((Start)) --Done--> s2((Stop))
{{< /mermaid >}}

1. Permanent State of the node should be represented as "Rectangle"
{{<mermaid align="left">}}
graph LR 
	node1[This is the Permanent State of the Node]
{{< /mermaid >}}

1. Temporary State of the node should be represented as "Rectangle with Rounded Corners"
{{<mermaid align="left">}}
graph LR 
	node2(This is the Temporary State of the Node)
{{< /mermaid >}}

1. Action on the State of the node should be represented as Text on the link
{{<mermaid align="left">}}
graph LR 
    A -- This is the text! --- N2[Node2]
{{< /mermaid >}}

1. Data Persistence Node should be represented as Cyclinder
{{<mermaid align="left">}}
graph LR 
    DS1[(Data Store)]
{{< /mermaid >}}

1. All decision blocks should be represented as Diamond shapes 
{{<mermaid align="left">}}
graph LR 
    Paid{Invoice paid?}
{{< /mermaid >}}

1. Send Signal Node should be represented as   Pointed Rectangle 
{{<mermaid align="left">}}
graph LR 
    Paid{{Send email}}
{{< /mermaid >}}
     
1. Receive Signal Node should be represented as  Right point inside Rectangle 
{{<mermaid align="left">}}
graph LR 
    Paid>Received email]
{{< /mermaid >}}
     
### Sequence

#### Sequence Diagram Rules:
1. Numbering for the messages.
1. Notes for the explanation of the flow not for the success and failure of the message ie.. note is independent of message.
1. Messages optionally carry **S** for **success**, **F** for **failure**.
1. All the api call messages should have **GET/POST/PUT/DEL URLPath subject**.
1. The failure message should have **cross arrow head (- - x ->)**.
1. Group the messages for more clarity.
 
1. All types of the entities should be represented as Rectangles. Use Activation all the time with Sequence number if required.
{{<mermaid align="left">}}
sequenceDiagram
	autonumber
    Alice->>+John: Hello John, how are you?
    John-->>-Alice: Great!
{{< /mermaid >}}

### Class Diagrams
1. Only Inheritance and Association relations should be used.
{{<mermaid align="left">}}
classDiagram
	classA <|-- classB
	classE <-- classF
{{< /mermaid >}}
1. Cardinality / Multiplicity on relations is very important
{{<mermaid align="left">}}
classDiagram
    Customer "1" --> "*" Ticket
    Student "1" --> "1..*" Course
    Galaxy --> "many" Star : Contains
{{< /mermaid >}}

### ER Diagrams
Use Class diagrams instead of the ER Diagrams

### SVG files
Some times, we may have draw some complex diagrams. Especially the Architecture diagrams. In such case please draw diagrams using other tools and export the diagrams as SVG and embedded to the file using the following syntax

The recommended SVG Editor and format is [Plant-UML](https://plantuml.com/)
Create the PlantUML diagram using [Online Editor](http://www.plantuml.com/plantuml/uml/SyfFKj2rKt3CoKnELR1Io4ZDoSa70000) and export the same to SVG format.
Makesure the exported SVG file should have a copy of the Plain PlantUML at the end. This Plant UML code will be useful to keep the track of the changes to this file in the future. 
It will be wrapped in a MD% tag as follows

```
<!--MD5=[6f482033c72b4ade3dafe25052111253]
@startuml
  Plant UML code here ...
@enduml
-->
```   

The exported and validated file should be copied to the local/relative directory and use the following shortcode ("svg") to embedded the image. 

```
{{</* svg "sample_svg.svg" */>}}
```

##### Sample SVG file

{{< svg "sample_svg.svg" >}}


##### Deployment Diagrams help
- [Plant UML Deployment diagrams Syntax](https://plantuml.com/deployment-diagram)
- [Plant UML Component diagrams Syntax](https://plantuml.com/component-diagram)
- [Deployment Diagrams](https://www.lucidchart.com/pages/uml-deployment-diagram/#section_0)
- [Boundary-Control-Entity](http://www.cs.sjsu.edu/~pearce/modules/lectures/ooa/analysis/ecb.htm)

### Charts line, bar etc.
Use the chart tag to display the charts

```

{{</* chart 90 200 */>}}
{
    type: 'bar',
    data: {
        labels: ['Red', 'Blue', 'Yellow', 'Green', 'Purple', 'Orange'],
        datasets: [{
            label: 'Bar Chart',
            data: [12, 19, 18, 16, 13, 14],
            backgroundColor: [
                'rgba(255, 99, 132, 0.2)',
                'rgba(54, 162, 235, 0.2)',
                'rgba(255, 206, 86, 0.2)',
                'rgba(75, 192, 192, 0.2)',
                'rgba(153, 102, 255, 0.2)',
                'rgba(255, 159, 64, 0.2)'
            ],
            borderColor: [
                'rgba(255, 99, 132, 1)',
                'rgba(54, 162, 235, 1)',
                'rgba(255, 206, 86, 1)',
                'rgba(75, 192, 192, 1)',
                'rgba(153, 102, 255, 1)',
                'rgba(255, 159, 64, 1)'
            ],
            borderWidth: 1
        }]
    },
    options: {
        maintainAspectRatio: false,
        scales: {
            yAxes: [{
                ticks: {
                    beginAtZero: true
                }
            }]
        }
    }
}
{{</* /chart */>}}

```

##### Sample chart

{{< chart 90 200 >}}
{
    type: 'bar',
    data: {
        labels: ['Red', 'Blue', 'Yellow', 'Green', 'Purple', 'Orange'],
        datasets: [{
            label: 'Bar Chart',
            data: [12, 19, 18, 16, 13, 14],
            backgroundColor: [
                'rgba(255, 99, 132, 0.2)',
                'rgba(54, 162, 235, 0.2)',
                'rgba(255, 206, 86, 0.2)',
                'rgba(75, 192, 192, 0.2)',
                'rgba(153, 102, 255, 0.2)',
                'rgba(255, 159, 64, 0.2)'
            ],
            borderColor: [
                'rgba(255, 99, 132, 1)',
                'rgba(54, 162, 235, 1)',
                'rgba(255, 206, 86, 1)',
                'rgba(75, 192, 192, 1)',
                'rgba(153, 102, 255, 1)',
                'rgba(255, 159, 64, 1)'
            ],
            borderWidth: 1
        }]
    },
    options: {
        maintainAspectRatio: false,
        scales: {
            yAxes: [{
                ticks: {
                    beginAtZero: true
                }
            }]
        }
    }
}
{{< /chart >}}