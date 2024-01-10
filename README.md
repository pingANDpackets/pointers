# pointers


1. Db deploymenets on k8s clusters have their own set of problems as Velero sometimes fails to backup. It thinks it is backing up but it fails

2. network-troubleshooting -

   (A) check hostfile entry of the service you are trying to connect
   (b) ping the service and see if response is coming
   (c) check if the service is listening on 0.0.0.0 as some services are configured to listen on localhost only. That means the remote connections are enabled so services on other machines can connect here . means listen from all the ip addresses 0.0.0.0 means all ipv4


3. We have to always restart any service after config changes

4. in case systemd's config is tweaked ( example in case of tomcat server setup) , we have to use systemctl daemon reload before starting the service ( systemctl start tomcat)

5. Networking -

   (a) OSI model

   ![image](https://github.com/pingANDpackets/pointers/assets/120235206/b33fb12f-1077-4be8-8826-9b1d12984e54)

   (b) general commands -
   ifconfig / ip addr show - info abut nics (loopback address is the local area network)
   
   ping <ip> / ping <servername> {must be present in hostsname for name resolution)
   
   traceroute - to identify the complete path to the destination { can help in identifying the latency between the hops }
   
   netstat -antp/ ss -tunlp - show all the tcp ports that are opened on the system

   nmap <server> - scan the ports on the server { troubleshoot if ports ar eopen if 2 servcice are not connecting)

   dig <server-name > / nslookup <server >   -  shows the correct name of the server is resolving to the correct ip

   route -n   - to look for the gateways for route tables

   arp - shows the mapping of the servers to their mac addresses

   mtr <server-name >  - shows the hops taken to reach the server and identify the places for packet loss

   telnet <server>  <port>  - investigate if we are able to connect

6.  Docker commands -

    
systemctl status docker
docker run hello-world

docker images
docker ps
docker ps -a

# Run a container
docker run --name web01 -d -p 9080:80 nginx
docker ps
docker inspect web01
curl http://172.17.0.2:80

ip addr show
docker ps

# Go to browser enter IP:HostPort

# Building an Image
mkdir images
cd images/
vim Dockerfile

# Paste below content
FROM ubuntu:latest AS BUILD_IMAGE
RUN apt update && apt install wget unzip -y
RUN wget https://www.tooplate.com/zip-templates/2128_tween_agency.zip
RUN unzip 2128_tween_agency.zip && cd 2128_tween_agency && tar -czf tween.tgz * && mv tween.tgz /root/tween.tgz

FROM ubuntu:latest
LABEL "project"="Marketing"
ENV DEBIAN_FRONTEND=noninteractive

RUN apt update && apt install apache2 git wget -y
COPY --from=BUILD_IMAGE /root/tween.tgz /var/www/html/
RUN cd /var/www/html/ && tar xzf tween.tgz
CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
VOLUME /var/log/apache2
WORKDIR /var/www/html/
EXPOSE 80

# Build Image
docker build -t tesimg .
docker images

# Run container from our Image. -   -P commmand automatically picks a port from the host without explicitly mentioning it
docker run -P -d tesimg
docker ps


docker ps
ip addr show
docker ps

# Go to browser enter IP:HostPort


# CLEAN UP
docker ps
docker stop web01 heuristic_hugle
docker ps -a
docker rm heuristic_hugle web01 competent_gates elastic_ramanujan relaxed_sammet
clear
docker images
docker rmi a54ee9c44b3b 6130c26b5558 057d51c0049c 825d55fb6340 12766a6745ee feb5d9fea6a5




   nmap <server > 

   

