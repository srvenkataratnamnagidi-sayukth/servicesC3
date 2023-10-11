---
title: DevOps
weight: 5
---

## Vision
DevOps is a set of practices that works to automate and integrate the processes between software development and IT teams, so they can build, test, and release software faster and more reliably.

The term DevOps was formed by combining the words “development” and “operations” and signifies a cultural shift that bridges the gap between development and operation teams, which historically functioned in siloes. 

Because of the continuous nature of DevOps, practitioners use the infinity loop to show how the phases of the DevOps lifecycle relate to each other. Despite appearing to flow sequentially, the loop symbolizes the need for constant collaboration and iterative improvement throughout the entire lifecycle.

{{% notice info %}}
At its core, DevOps is a culture, a movement, a philosophy.
{{% /notice %}}


## Tools and Technologies
### Programming Languages
#### Python
Python will be used to write Integration scripts and "Scraplets for Promethues"

#### Java
For all the Java based application, we write "Scraplets for Promethues"

#### Go
For all the Cross platform(Windows & Linux) application, we write "Scraplets for Promethues"

### Tools
### Git(Github)
All the source code and configurations will be maintained by Git

### Maven
Maven will be used as compiler & package manager for all applications

### Sonarcube
It is a Static code analyzer for all types of vulnerabilities in our source code

### Snyk
it is vulnerability assessment tool for 3rd party libraries we are using

### TestNG
it is used as a Unit Testing Framework

### Jenkins
it is the main the CI/CD manager. it uses Git, Maven to generate the artifacts using a Pipeline

### Roboletric
Used for mobile Unit testing

### Gradle
used for Android Compile and Packaging


## DevOps Pipeline

### Artifact Pipeline

{{< svg "ShadkonaDevOpsPipeline.svg" >}} 

### Metric Monitor Pipeline

{{< svg "PipelineMonitor.svg" >}} 

### Pipeline Monitor Architecture

{{< svg "PipelineMonitorArch.svg" >}}

### Scraplet Architecture

{{< svg "ScrapletArch.svg" >}}

### Deployment Architecture

{{< svg "GramSevakDeploymentArchitecure.svg" >}}

{{% children  %}}
