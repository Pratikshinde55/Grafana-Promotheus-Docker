# Grafana-Promotheus-Docker
Grafana Connect to Prometheus and Prometheus is connect to docker 


### Docker Setup:

I use amazon linux2 AMI instance for docker.

- Note:

  Docker collects there own metrics on localhost, When we want to collect that Docker metrics then need to expose docker metrics to outside world.

  For this Docker and prometheus provide a file - Search on Google "Docker connect to prometheus" (Refer Link-https://docs.docker.com/engine/daemon/prometheus/)

 #### Prometheus Agentless or Pull type connection to Target:

   This method is known as "Pull method" or "Aagentless" connection. This is possible because Docker collects their own metrics.


 Install Docker command:

    yum install docker -y 

 Start Docker service:

     systemctl start docker
