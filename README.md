# pointers


1. Db deploymenets on k8s clusters have their own set of problems as Velero sometimes fails to backup. It thinks it is backing up but it fails

2. network-troubleshooting -

   (A) check hostfile entry of the service you are trying to connect
   (b) ping the service and see if response is coming
   (c) check if the service is listening on 0.0.0.0 as some services are configured to listen on localhost only
