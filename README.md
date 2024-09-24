# Grafana Connect to Prometheus and Prometheus is connect to docker 
![alt text](image.jpg)
### Step-1: SetUp- Grafana connect to prometheus

Link-  [Grafana-Connect-prometheus](https://github.com/Pratikshinde55/Grafana-prometheus-linuxOS.git) 

### Step-2 Docker Setup

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


- Note:

  After do change in settings then need to restart docker services to apply changes

Command for restart docker service:

     systemctl restart docker


we can also check docker exposing metrics on google -->> Docker EC2 public IP : 9323 

![image](https://github.com/user-attachments/assets/1bf91637-f964-4e73-a369-fc2d996345d6)

Docker Host EC2 inbound rules must allow.


### Step-3: ADD Docker on Prometheus

Prometheus is used for monitoring metrics and Alerting. Prometheus collect data and store at own DataBase(TSDB).

Prometheus collect metrics from any system with help of Agent or Agentless.

Add target node to prometheus

On Prometheus EC2 terminal we add target node that Docker linux OS where i installed docker metrics exposing program.

- Note:

  "promethus.yml" this is prometheus config file here we add target node details.

Open prometheus.yml file:

     vim prometheus.yml
     
![image](https://github.com/user-attachments/assets/4692af69-cdcb-4a7a-886f-bc638d1f9dd0)

Here, Target means Docker EC2 public IP + port no of exposing.

- Note:

  Docker Host EC2 instance Inbound rules must be allow.

After doing change in prometheus.yml config file then need restart Prometheus server for apply change:

Command for delete prometheus process :

     pkill prometheus

Command for Start Prometheus server:

     ./prometheus &

 ![image](https://github.com/user-attachments/assets/3c2b8933-51e5-447c-898e-b80a1e5ca584)

 ![image](https://github.com/user-attachments/assets/a422f3ec-745c-48eb-a677-f25841e85f7a)


### Step-4: On Grafana 

We can get info of docker because Grafana is connected to Prometheus DataSource.

![image](https://github.com/user-attachments/assets/a00f0dc1-1dc7-4a34-9821-cfcf514f6d6d)


Create DashBoard using Grafana

![image](https://github.com/user-attachments/assets/8f5f2afd-cf8e-40e8-a7d8-51c5473694f4)

 
