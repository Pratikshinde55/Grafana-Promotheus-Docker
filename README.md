# Grafana-Promotheus-Docker
Grafana Connect to Prometheus and Prometheus is connect to docker 


### Docker Setup:

I use amazon linux2 AMI instance for docker.

 Install Docker command:

    yum install docker -y 

 Start Docker service:

     systemctl start docker

- Note:

  Docker collects there own metrics on localhost, When we want to collect that Docker metrics then need to expose docker metrics to outside world.

  For this Docker and prometheus provide a file - Search on Google "Docker connect to prometheus" (Refer Link-https://docs.docker.com/engine/daemon/prometheus/)

 #### Prometheus Agentless or Pull type connection to Target:

   This method is known as "Pull method" or "Aagentless" connection. This is possible because Docker collects their own metrics.

Expose Docker metrics:

      vim /etc/docker/daemon.json

![image](https://github.com/user-attachments/assets/296ef590-a28c-46ee-a2fa-b882ab179511)

Here, 

" /etc/docker/daemon.json " => This location for "linux host system" where install docker and expose metrics.

"metrics-addr" => This is endpoint means metrics exposes to IP and Port no.

"0.0.0.0:9323" => '0.0.0.0' means what ever Public IP of Docker Host that take here and '9323' is port no for exposing metrics.




 
