# Docker

Java/j2EE  
1.5,1.6,1.7  

ear ---> Enterprize archive  
war ---> web archive  
jar ---> java archive  

.ear ---> it is the combination of (frontend+backend) ---> catalogue+cart+shipping+user+payment  
It can use only 1 db ---Oracle DB  
.ear ---> multiple wars file + jar(dependies/libraries)  

webspahere, weblogic,JBOSS ----> Application servers  

servlet(base for any web frame woorks)+ JSP (java server pages)  
100 mb ---> 120 mb  

---

## release process

new features  
defects  

Business analyst(client side) + business analyst + developers + testing team + le support + l1 support + managers + leads + architect + build  
realse manager ----> co ordinate with all team members and make sure the realse is going as per the plan and continously update the client  

9-6 PM downtime  
application servers stopped  
build new application  
remove old ear  
place new ear  
check the modules and versions  
restart the server  

if major defects  

slow, no response ....  
restart  

2.30 application was slow, no response  
send the logs to developers  
if the issue was not able to replicate  

Bridge --> Clients + L2 support + L1 support + Service Desk + Networking team + Linux team + DB team + testing team  

jQuery and angularJs  

here backend and frontend are separated  
frontend ----> backend  
API ---> rest API  

war file ---> wildfly, jboss  
it contain only backend  

catalogue+cart+shipping+user+payment ---> if any component is not working or slow they will backend side = entre application we need to check here  

---

## Microservices Architecture

In a microservices architecture, an application is divided into multiple independent components (services), such as:

* Catalogue
* Cart
* Shipping
* User
* Payment

### Key Characteristics

* All components are separated and operate independently. If one component fails, the remaining components continue to function without interruption.
* Each component can be developed using different programming languages and technologies.
* The architecture follows **loose coupling**, meaning services have minimal dependencies on each other.
* This results in greater flexibility, scalability, and ease of maintenance.

---

# real time example

## Joint Families vs Small Families vs Individuals

15-20 members --> .ear file --> Physical Server --> Dedicated Host  
Big House  

**Landed House**

### advantages

Privacy  

### Disadvantages

Costly  
More time to construct  
Maintanace --> Electricity, Water, Security etc.  

---

## Small Families

4 members --> VM --> Shared  
small flat --> 1bhk or 2bhk  

### advantages

less cost  
less time to construct  
no maintanance  

### disadvantages

privacy  

---

Individuals --> Microservices  

hostels, pgs --> Containers  

### advantages

least cost  
less time  
no maintanance  

### disadvantages

0 privacy  

---

## diagram

### physical server

hardware (cpu,ram)--> OS ---> application  

- hardware means CPU, RAM, Motherboard  
* we installed OS on hardware  

---

## VM

Hardware → Host OS → Hypervisor → Guest OS → Applications  

• Hypervisor = software that creates and manages VMs.  
• VM logically divides physical hardware into multiple virtual servers.  
• Guest OS can be Ubuntu, Windows, RedHat, CentOS, etc.  
• Need to install, configure, and manage the hypervisor.  
• Hypervisor management can be difficult.  
• Each VM has its own OS, so it uses more CPU, RAM, and storage.  
• Resource consumption is higher compared to containers.  

---

## Containers / Docker

Physical Server → Hardware → Host OS → Docker Engine → Containers  

• Containers provide only what is required to run the application.  
* container/image ---> (bare min OS )+ system packages + application code and dependies  
* Docker Engine is the software that creates and manages containers.  
* Containers run your applications.  
• Containers are lightweight and take very less storage and memory.  
• Containers share the Host OS kernel.  
• No separate Guest OS is required.  
* it cannot block the resource utilization  

---

## VM vs Containers

costly                     costly  
more time                  less time  
more size                  less size  
more resources             less resources  
resources block            dynamic resources allocation  
hypervisior                no need of extra components  
not protable               portable  
more security              less security  

---

## Docker installation

sudo dnf -y install dnf-plugins-core  
sudo dnf config-manager --add-repo https://download.docker.com/linux/rhel/docker-ce.repo  

sudo dnf install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin  

sudo systemctl start docker  
sudo systemctl enable docker  
sudo systemctl status docker  

docker ps ---permission denied  

add your normal group to docker group  

sudo usermod -aG docker ec2-user  

exit  

docker ps --- It gives running containers  

---

AMI ---> OS + configuration(system packages + app runtime + app librairies )  
image ---> bare min os + system packages + app runtime + app librairies  

AMI → Launch/Run → EC2 Instance (Server)  

Docker Image → Run → Container  

---

## docker images

docker images  
It will show images that avaliable in system  
It is read only template used to craete conatiners  

docker pull <image_name>:<tag/version>  
docker pull <image_name>  

---

## docker container

docker create  
docker ps -a  
docker ps  

docker start <container_id>  

docker rm -f <container_ID>  

docker rmi nginx  

docker run <image>:<tag>  
docker run -d <image>  

docker run -d -p 80:80 <image>  

docker ps -a -q  
docker rm -f `docker ps -a -q`  

docker run -d -p 80:80 --name nginx nginx  

docker exec -it nginx bash  

cat /etc/nginx/nginx.conf  

docker inspect nginx  

docker logs nmginx  

---

## Dockerfile

FROM  
RUN  
CMD  
COPY  
ADD  
LABEL  
EXPOSE  
ENV  
ENTRYPOINT  
WORKDIR  
ARG  
ONBUILD  

---

## RUN

used to execute commands during image build  

---

## CMD

runs when container starts  

---

## COPY

copies files from local to image  

---

## ADD

same as COPY + url + unzip  

---

## LABEL

key value metadata  

---

## EXPOSE

for documentation of ports  

---

## ENV

environment variables  

---

## ENTRYPOINT

fixed command  

---

## WORKDIR

working directory  

---

## ARG

build time variables  

---

## ONBUILD

triggers when used by another image  
