# ANSIBLE PLAYBOOK
#### **Systems Operations - Technical Challenge** 
(https://github.com/oxie/sysops_tech_challenge)
###
Description:
A simple 3-tier tech stack, using the following components:
- A load balancer.
- Application server.
- Database server with persistent storage.
- Deployment REST API to update the deployed application.
- All tiers must be running as containers, that also implies high availability, and in the case of the database, persistent storage.

Requirements:
 - Be executable, we should be able to run it in a simple way. That means a  - command/script/tool to spin up the environment and to be able to access the ghost application. We do not expect any content except the default from the ghost application.
 - Use containers.
 - Use an automation tool (we prefer ansible, but use what you know).
 - Extra points for using an orchestrator (docker swarm, kubernetes, apache  - marathon).
 - All your work must be shared using a git repository that we can clone.


---------
###
##### **Ghost(2x) + Mariadb(master) + Mariadb(slave) + HaProxy (loadbalancer)**  
###
###
-------------------
##
##### Run ansible towards custom host file.
##
`ansible-playbook -i hostsfile playbook.yml -vvv`

##### **Ansible during deployment options - "swarm" or "compose"**
###
##

##### ***Based on:***
###
##
| Image| Source|
| ------ | ------ |
| bitnami/mariadb:latest| [https://github.com/bitnami/bitnami-docker-mariadb]  |
| bitnami/ghost:lates| [https://github.com/bitnami/bitnami-docker-ghost] |
| dockercloud/haproxy | [https://github.com/docker/dockercloud-haproxy] |
| djenriquez/sherpa| [https://github.com/djenriquez/sherpa] |


### **Featured Setup:**
- Docker swarm mode initiated for orchistration.
- 2x docker-compose file used  - for v2 and v3 of compose and stack.
- Additional Swarm Network - ghost-tier.
- Containers started as scalable services.
- Used docker container for exposing Docker REST API to HTTP on port 8080.

**Example Curl Request:**
` curl http://localhost:8080/images/json `


### Final Thoughts:
Hello, I have expored and tested different Docker Orchistration tools ( Marathon, DC/OS/, Shipyard, Portainer, Swarmui etc..), but i've come up with the conclusion that if i want to keep the environment clean and light-weight to its possible maximum i should put aside all unessessary containers. That is the reason for which i decided to use the Docker Swarm Orchistration in combination with docker-compose and docker stack as most optimized option. Docker Swarm mode is a completely integrated scalable platform that has great features out of the box with a simple CLI command management.

### [**Docker Research of Trends 2017 and Use Cases**](/Thoughts.md)
##
#### Additional Technologies tested:
Ansible - Docker modules. ( After I explored this option and tested on environment, decided to skip it as this gives another type of functionalities are releated with further dependency management.
##
##






