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

docker pull <image_name>:<tag/version> ---To get/download the image
docker pull <image_name> --> It will take latest image
docker images 
* from where it is taking images (docker hub)
* now we need to create container from the image
docker container
----------------
it is the live application created from image
we can run,stop and delete the conatiners

docker create    ---> to create container
docker ps -a ----> It will all containsers including all status 
docker ps ---> running conatiner
# start the container
docker start <container_id>
docker ps 
# to remove container
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

- used to execute commands during image build
- RUN instruction configure the image like installing packages and doing some configurations
- RUN executes at the time of image building
- we can have multiple run commands beacuse we will install lot of packages

```bash
docker build -t run:v1 .
```

## nginx run

```bash
systemctl start nginx
```

It will run service files

```text
/etc/systemd/system/nginx.service
```

it command will execute

```dockerfile
CMD ["nginx", "-g", "daemon off;"]
```

- `-g` ---> means set the configuration directories

## what happen if i remove run:v1 in the file

```bash
docker rmi -f run:v1
docker images
docker build -t cmd:v1 .
docker images
```

here we gave base image is `run:v1` but here we can't see image for that it will check Docker Hub

```bash
docker pull nginx
```

first it will check locally is there any nginx image, if doesn't exists it will check in Docker Hub.

we will get error.

then go to run folder

```bash
docker build -t run:v1 .
docker images
```
---

## CMD

It will run/executes at the time of container creation, i.e., at the time of `docker run`.

```bash
docker run -d cmd:v1
docker ps
```

- we cannot have multiple `CMD` commands.
- `CMD` should be the only `CMD` instruction inside the Dockerfile. 

---

## COPY

- It will copy the local code into container.

- deamon off ---> run the deamon on background

```bash
docker build -t copy:v1 .
docker ps
docker rm -f `docker ps -a -q`
docker run -d -p 80:80 --name copy nginx
```

---

## ADD

## ADD

- COPY and ADD both copies the code from local to conatiner, but it has 2 advantages.
- it can directly fetch the file from the internet.
- it can directly untar the files into conatiners.

```bash
docker rm -f copy
docker build -t add:v1 .
docker run -d -p 80:80 --name add add:v1
```

- here it will download the file but it can directly give the read acess no we need to do that.

```bash
docker rm -f add
docker build -t add:v1 .
docker run -d -p 80:80 --name add add:v1
```

## to see the content

```bash
docker exec -it add bash
cd /usr/share/nginx/html
```

---
## Docker Storage

```bash
df -hT
```

- here we are increasing `/var`.

- `/var/lib/docker` ---> here containers are stored / home directory.

- images count is increased then memory usage also increased.

- so here we need to increase the `/var` folder size.
  

---
## LABEL

- it is like a tag it can conatin key values pairs.
- It can used at the time of fliteration.
- ex: we have multiple images so we want filter using lables.

```bash
docker images --filter label=COURSE="devops"
```

## how can you push the images to docker hub

log into dockerhub:

```bash
docker login -u lakshmireddy77
docker push URL/username/imagename:version
docker push label
```

it will give an error. for this we need to retag the lables.

```bash
docker tag label:v1 lakshmi315/label:v1
```

- 1st adding the tags then push.

```bash
docker push lakshmi315/label:v1
```
---

## EXPOSE

- It can be used for users to see which port is open.
- This is for documentation purposes, not for any functionality.

```bash
docker build -t lakshmi315/expose:v1 .
docker inspect lakshmi315/expose:v1
```

- to check ports.

```bash
docker push lakshmi315/expose:v1
```

- here if we give `run` in the `FROM` command, first it will check locally, so we can directly give.

```dockerfile
FROM lakshmi315/run:v1
```

```bash
docker push lakshmi315/expose:v1
```

- to push the image.

---

## ENV

- these variables are accessible inside the container.

```bash
docker build -t lakshmi315/env:v1 .
docker run -d lakshmi315/env:v1
docker ps -a
```

- It is exited because we haven't given any command to run.
- here I cannot use daemon because we are not installing nginx. Instead, I will give:

```dockerfile
CMD ["sleep","1000"]
```

## to login into container

```bash
docker exec -it <container_id> bash
env
```

- `env` ---> it will show environment variables.
    

---

## ENTRYPOINT

```bash
docker build -t entry:v1 .
docker run entry:v1
```

- it continuously runs on the foreground.

```bash
docker ps -a
```

- we can override the `CMD` instruction.
- we can't override the `ENTRYPOINT` instruction. If we try, it will override the `CMD`.

```bash
docker run entry:v1 ping facebook.com
```

## to see the errors/full info

```bash
docker ps -a --no-trunc
```

```text
ping google.com ping facebook.com
```

- o/p for `ENTRYPOINT`.

- we can use a combination of `CMD` and `ENTRYPOINT` for better results.
- `ENTRYPOINT` will have the command. Default arguments can be supplied by `CMD`.
- you can also override the default arguments through the command line.

```bash
docker exec -it <container_id> bash
```

- login, we are getting root access.

- does container have separate storage or it will use host storage??
- it uses whatever the host uses, the host storage.
- if we give root access to the container, it will block the entire storage.
- `USER` ---> for this we need to create a user and use that user.
  

---

## WORKDIR

```bash
docker build -t workdir:v1 .
```

```bash
docker build -t workdir:v1 --no-cache --progress=plain .
```

- for human readable.

```bash
docker run -d workdir:v1
docker exec -it <CID> bash
``` 

---

## ARG

- It is like an `ENV` variable. It contains key-value pairs.

```bash
docker build -t arg:v1 . --progress=plain --no-cache
```

- here we are able to access the ARGs and variables.

```bash
docker run -d arg:v1
docker exec -it aa bash
env
```

- Here we do not get the ARGs.
- `ARG` is a build-time variable.
- they can't be accessed inside the container.
- `ENV` can be accessed at build time and inside the container also.

## we can override also

```bash
docker build -t arg:v1 . --progress=plain --no-cache --build-arg trainer=lakshmi
```

- `ARG` instruction variables can be overridden.

- In an exceptional case, `ARG` can be the first instruction to supply the base OS in `FROM`.
- you can't use that variable after the `FROM` instruction.

## how we can access ARGs inside container 

---

## ONBUILD

- while developing images, you can put some conditions while others are using your images.

```bash
docker build -t onbuild-test:v1 --progress=plain --no-cache .
docker run -d -p 80:80 onbuild-test:v1
```

```text
<public_ip>
```

- open it in the browser.
