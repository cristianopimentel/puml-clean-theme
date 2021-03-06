# PlantUML - Clean Theme
> This is my attempt to come up with a clean PlantUML theme that I can use to design and estimate projects faster.
>
> This is based on my own notation but using draw.io.
> 
> Nice pet-project for the 1st weekend of a new year.

Visit [https://plantuml.com/](https://plantuml.com/) for more information about PlantUML.

## How To Use
To use the theme you can `!include` the file from GitHub or from the disc, here is an example of how to include the Deployment Diagram theme:
```
!include https://raw.githubusercontent.com/cristianopimentel/puml-clean-theme/main/deployment-diagram.puml

' OR

!include deployment-diagram.puml 
```

If you are going to include from GitHub, always use the `RAW` version of the file.

## Deployment Diagram

Reference [Deployment Diagram](https://plantuml.com/deployment-diagram) - `deployment-diagram.puml`

### Stereotypes
Here is the list of available stereotypes and where you can use them:
| Stereotype   | Elements                                                                                    |
|--------------|---------------------------------------------------------------------------------------------|
| `new`        | all                                                                                         |
| `update`     | all                                                                                         |
| `remove`     | all                                                                                         |
| `internal`   | `card`, `circle`, `cloud`, `collections`, `folder`, `frame`, `node`, `rectangle`, `storage` |
| `external`   | `card`, `circle`, `cloud`, `collections`, `folder`, `frame`, `node`, `rectangle`, `storage` |
| `firewalled` | `card`, `circle`, `cloud`, `collections`, `folder`, `frame`, `node`, `rectangle`, `storage` |


### Procedures/Functions
Here is the list of the `!procedure`/`!function` available:
| Name | Type | Parameters |
|-|-|-|
| `$Legend($hasEnvironment)` | Procedure | `$hasEnvironment = 0`: If some value is specified it will accept as TRUE and add to the legend lines to explain what `internal`, `external` and `firewalled` means |

### Screenshots

**All Shapes**

![All shapes](/img/all-shapes.png)

**All Stereotypes**

![All stereotypes](/img/all-stereotypes.png)

**Legend with hasEnvironment ommited**

![Legend](/img/legend-hasenvironment-false.png)

**Legend with hasEnvironment = TRUE**

![Legend](/img/legend-hasenvironment-true.png)

**Complex Example** - based on https://www.pinterest.com/pin/48202658490696590/ (I tried my best!)

![Complex Example](/img/example.png)

### Code Example
**Complex Example**
```
@startuml
!include https://raw.githubusercontent.com/cristianopimentel/puml-clean-theme/main/deployment-diagram.puml

' "Based on https://www.pinterest.com/pin/48202658490696590/"

rectangle company <<internal>><<firewalled>> {
    rectangle "Datacenter N" as datacenterN {
        collections "Cluster Manager" as clusterManagerB #pink

        rectangle "Frontend Layer" as frontEndLayerB {
            collections "Frontend Node\nRouter Library" as frontEndNodeB #green
        }
        rectangle "Data Layer" as dataLayerB {
            collections "Data Node" as dataNodeB #blue
            database "Disk A" as diskB1
            database "Disk N" as diskBN

            dataNodeB --> diskB1
            dataNodeB --> diskBN
        }

        card Client as clientB #Yellow

        clientB --> frontEndLayerB : HTTP
        frontEndLayerB --> dataLayerB
        clusterManagerB -> frontEndLayerB
        clusterManagerB -> dataLayerB
    }

    rectangle "Datacenter A" as datacenterA {
        collections "Cluster Manager" as clusterManagerA #pink

        rectangle "Frontend Layer" as frontEndLayerA {
            collections "Frontend Node\nRouter Library" as frontEndNodeA #green
        }
        rectangle "Data Layer" as dataLayerA {
            collections "Data Node" as dataNodeA #blue
            database "Disk A" as diskA1
            database "Disk N" as diskAN

            dataNodeA --> diskA1
            dataNodeA --> diskAN
        }

        card Client as clientA #Yellow

        clientA --> frontEndLayerA : HTTP
        frontEndLayerA --> dataLayerA
        clusterManagerA -> frontEndLayerA
        clusterManagerA -> dataLayerA
    }

    datacenterA <.> datacenterN
}

card "CDN" as cdnA <<new>>
cdnA ---> frontEndLayerA

card "CDN" as cdnB <<update>>
cdnB ---> frontEndLayerB

actor user
user --> cdnA : HTTPS
user --> cdnB : HTTPS
@enduml
```

## Contact
Created by [@cristianopimentel](https://cris.live) - feel free to contact me!