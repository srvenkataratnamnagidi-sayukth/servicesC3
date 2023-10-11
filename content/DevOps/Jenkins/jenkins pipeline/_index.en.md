---
title: Jenkins Pipeline
tags : ["Pipeline Scripting"]
---

## Jenkins Pipeline to automate the builds

![This is an image](https://www.lambdatest.com/blog/wp-content/uploads/2020/09/Jenkins-Pipeline.png)

### Jenkins Pipeline:

Jenkins Pipeline is a collection of jobs or events that brings the software from version control into the hands of the end users by using automation tools. It is used to incorporate continuous delivery in our software development workflow.

### Jenkins Pipeline Types:

Jenkins Pipeline basically two types

#### 1.Declarative

#### 2.Scripted

### JenkinsFile:

 
### Pipeline

It is a user-defined framework that includes all the processes like create, check, deploy, etc. In a Jenkinsfile, it’s a list of all the levels. All of the stages and steps within this block are described. 


### Why Pipeline?

Jenkins is, fundamentally, an automation engine which supports a number of automation patterns. Pipeline adds a powerful set of automation tools onto Jenkins, supporting use cases that span from simple continuous integration to comprehensive CD pipelines. By modeling a series of related tasks, users can take advantage of the many features of Pipeline

### Pipeline concepts

The following concepts are key aspects of Jenkins Pipeline, which tie in closely to Pipeline syntax

#### 1.Pipeline

A Pipeline is a user-defined model of a CD pipeline. A Pipeline’s code defines your entire build process, which typically includes stages for building an application, testing it and then delivering it.Also, a pipeline block is a key part of Declarative Pipeline syntax.

#### 2.Node

A node is a machine which is part of the Jenkins environment and is capable of executing a Pipeline.
Also, a node block is a key part of Scripted Pipeline syntax.

#### 3.Stage

A stage block defines a conceptually distinct subset of tasks performed through the entire Pipeline 

#### 4.Step

A single task. Fundamentally, a step tells Jenkins what to do at a particular point in time 

### Declarative Pipeline fundamentals

Declarative pipeline is a relatively new feature that supports the pipeline as code concept.In Declarative Pipeline syntax, the pipeline block defines all the work done throughout your entire Pipeline.

````
pipeline {
    agent any 
    stages {
        stage('Build') { 
            steps {
                
            }
        }
        stage('Test') { 
            steps {
                
            }
        }
        stage('Deploy') { 
            steps {
                
            }
        }
    }
}
````
1.Execute this Pipeline or any of its stages, on any available agent.

2.Defines the "Build" stage.

3.Perform some steps related to the "Build" stage.

4.Defines the "Test" stage.

5.Perform some steps related to the "Test" stage.

6.Defines the "Deploy" stage.

7.Perform some steps related to the"Deploy" stage.

### Declarative Pipeline Example

Here is an example of a Jenkinsfile using Declarative Pipeline syntax
````
pipeline { 
    agent any 
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Build') { 
            steps { 
                sh 'make' 
            }
        }
        stage('Test'){
            steps {
                sh 'make check'
            }
        }
        stage('Deploy') {
            steps {
                sh 'make publish'
            }
        }
    }
}
````
1.pipeline is Declarative Pipeline-specific syntax that defines a "block" containing all content and instructions for executing the entire Pipeline.

2.agent is Declarative Pipeline-specific syntax that instructs Jenkins to allocate an executor  and workspace for the entire Pipeline.

3.stage is a syntax block that describes a stage of this Pipeline. Read more about stage blocks in Declarative Pipeline syntax on the Pipeline syntax page.

4.steps is Declarative Pipeline-specific syntax that describes the steps to be run in this stage.

5.sh is a Pipeline step  that executes the given shell command.

6.node is Scripted Pipeline-specific syntax that instructs Jenkins to execute this Pipeline
