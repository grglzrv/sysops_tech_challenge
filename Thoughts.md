Docker is a popular new technology that lets development teams bundle applications in virtual containers to easily build and deploy them. We’ve previously seen how Docker reduces the complexity of DevOps workflows and encourages the practice of immutable infrastructure, where the entire application, along with its underlying operating system, is recreated and redeployed as a lightweight container for each change to an application, rather than relying on incremental updates.

Given Docker’s remarkable success story over the last three years and the availability of its remote API, it was inevitable that Docker would become a popular platform as well, on which developers have built all kinds of software.

In keeping with Docker’s own philosophy, third party developers in this new ecosystem have contributed many open source projects. In this article we review these projects to see how they are using the Docker API.

#### **Dogfooding**
The foremost user of the Docker API is Docker itself — they host a series of tools to combine and orchestrate Docker containers in useful configurations. Docker Compose facilitates the deployment of multi-container applications, while Docker Swarm allows the creation of clusters of Docker containers.

While Docker itself is active in this area, they welcome the contribution of other actors in orchestrating Docker containers. Orchestration is a broad term, but we can break it down into scheduling, clustering, service discovery, and other tasks.

It is usually undesirable to have several processes running inside the same Docker container, for reasons of efficiency, transparency, and to avoid tight coupling of dependencies. It’s much more practical for each container to remain limited to a single responsibility and to offer a clearly defined service to the rest of the infrastructure. A complete application therefore usually involves a collection of Docker containers. This introduces complexity for which new solutions abound.

#### **Scheduling**
Scheduling of Docker containers is also an important aspect of container orchestration. In this context scheduling refers to the rules by which containers are run on a given host. For example, a scheduling policy might involve two containers having to run on the same host when their functionalities are synergistic. Thanks to this policy, the two containers can be abstracted away as a single application when defining cluster behavior.

In addition to the scheduling features of Docker Swarm, Fleet by CoreOS and Marathon are examples of open source Docker schedulers.

Also read API-Driven DevOps: Spotlight on Docker for a more in-depth analysis of container architecture
Cluster Management
Clustering involves managing collections of Docker hosts into a cohesive whole so that they might operate together as a single system.

There are open source alternatives for Docker Swarm, like Google’s Kubernetes which lets teams define ‘pods’ of Docker containers. Others include Shipyard, Fleet by CoreOs and Marathon.

Companies such as Spotify have developed and open sourced their own Docker container management system, such is the need for a well-adapted Docker-based system for each use case.

#### **Service Discovery**
Service discovery refers to the discovery of the IP addresses related to a service on a network, which can be a complicated process in a multi-host, clustered environment.

Several companies like GliderLabs have leveraged Docker’s Remote API to listen to events and create utilities around container-based software. Registrator, an open source project supported by Weave, helps improve service discovery by inspecting newly created Docker containers and registering the new services in a directory like Consul.

#### **Networking**
To connect the Docker containers that form an application, Docker has some networking features. A default virtual bridge network is enabled by default, but there is a choice of configurations. Vendors have offered alternative network configurations for different use cases.

Weave creates a virtual network of micro-routers to connect containers across multiple hosts. This leads to simpler network configuration, dynamic addition of nodes to the network, and encrypted communications. Weave offers additional services such as the network monitoring product Weave Scope.

Flannel, an open source virtual networking solution by CoreOS, creates an overlay network using an Etcd cluster to store network configuration.

Project Calico is another open source networking solution for Docker containers, based on a pure ‘Layer 3’ approach, meaning that it is not an overlay network — no packet encapsulation happens above the third layer of the OSI model. This has the benefit of increasing performance when compared to the other solutions.

#### **Storage**
One problem that aficionados of immutable infrastructure have, which Docker mediates, is databases. Data in databases is mutable by definition, so a container featuring a database cannot simply be recreated from scratch and redeployed without compromising the database’s integrity.

There are also native Docker solutions to this problem in the form of data volumes and data volume containers. Data volumes are persistent and survive the deletion of the containers they are connected to, and the data they contain remain inviolate throughout the Docker life cycle. A data volume container can be used when sharing data across multiple containers.

Data volumes can be backed up and restored; products like Flocker by ClusterHQ, an open source data volume manager, manages data volumes and containers, and performs data migration in order to support container-based production databases.

#### **Continuous Integration**
Many tools exist in the area of continuous integration (CI) to better handle Docker containers in the build, test, and deployment cycle. For example, CodeFresh can be used to trigger the creation and deployment of Docker containers by detecting changes to a Git repository or a new build from the continuous integration server.

CodeShip’s Jet is a new CI platform for Docker. It can pull images from any Docker registry and integrate with Docker Compose to easily perform concurrent building and deploying of container-based applications.

Drone is another continuous delivery platform built on top of Docker, that uses an ephemeral container during the build process.

#### **Hosted Docker Registries**
In addition to the DockerHub itself, several companies offer hosted Docker Registries, like Quay.io, Artifactory and Google’s Container Registry. These services serve as private repositories for containers and offer advanced repository features, third party integrations, and a clean user experience for DevOps engineers.

#### **Log Aggregation**
Logspout is another open source project by GliderLabs. When several Docker containers share a single host server, Logspout performs log routing and aggregation into a log management system like PaperTrail. Also, Filebeat tallies a container’s logs and sends them to Logstash.

#### **Monitoring**
A slew of third party monitoring solutions for Docker-based apps are available, built by some of the biggest names in the cloud monitoring space. Leveraging Docker’s stats API, they display the resulting data in elaborate dashboards.

Examples of these monitoring solutions include:

A Docker extension by AppDynamics,
a Docker-enabled DataDog agent,
first-class citizen treatment of Docker containers in New Relic,
and Scout’s Docker agent, itself distributed as a Docker image.
Configuration Management
Docker lets you add custom metadata to images, containers, and processes (daemons) via labels. Labels are key-value pairs that are used to specify custom configuration like versioning and environment particulars.

To avoid naming collisions, Docker encourages the use of namespaces in these labels, but doesn’t enforce them. Docker Label Inspector is a utility by Gareth Rushgrove, a senior engineer at Puppet Labs, that checks published Docker images against these guidelines or a given JSON schema.

#### **Security Auditing**
As some have raised questions about the inherent security of container-based applications, and although Docker itself has plugged many of the holes over the years, vendors have offered solutions to further secure Docker apps. One example is Scalock, a company that has developed software to scan containers for security issues, control access to containers, and monitor containers at runtime to make sure they don’t overstep their authorization profile.
