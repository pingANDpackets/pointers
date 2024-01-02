# pointers


1. Db deploymenets on k8s clusters have their own set of problems as Velero sometimes fails to backup. It thinks it is backing up but it fails

2. network-troubleshooting -

   (A) check hostfile entry of the service you are trying to connect
   (b) ping the service and see if response is coming
   (c) check if the service is listening on 0.0.0.0 as some services are configured to listen on localhost only. That means the remote connections are enabled so services on other machines can connect here . means listen from all the ip addresses 0.0.0.0 means all ipv4


3. We have to always restart any service after config changes

4. in case systemd's config is tweaked ( example in case of tomcat server setup) , we have to use systemctl daemon reload before starting the service ( systemctl start tomcat)

5. 
