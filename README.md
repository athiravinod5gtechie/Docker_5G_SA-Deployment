# Docker_5G_SA-Deployment
**Reference** : https://github.com/herlesupreeth/docker_open5gs/tree/master <br>
Deploying 5G Standalone (5G SA) networks using Docker introduces a modern and efficient approach to network architecture. Docker, a containerization platform, enables the encapsulation of network functions into lightweight, portable containers. This approach facilitates seamless deployment, scalability, and resource optimization. By leveraging Docker in 5G SA deployment, operators can achieve rapid and consistent deployment across various environments, improving agility, flexibility, and overall operational efficiency in delivering advanced, high-performance 5G services. <br>
# Mandatory requirements:
* docker-ce - Version 22.0.5 or above
* docker compose - Version 2.14 or above <br>

# Steps for Deployment:
**Step 1** : git clone https://github.com/herlesupreeth/docker_open5gs <br>
**Step 2** : cd docker_open5gs/base <br>
**Step 3** : docker build --no-cache --force-rm -t docker_open5gs . <br>
**Step 4** : cd .. <br>
**Step 5** : set -a <br>
**Step 6** : source .env <br>
**Step 7** : sudo ufw disable <br>
**Step 8** : sudo sysctl -w net.ipv4.ip_forward=1 

**Configuration Changes** <br>

**Change the MCC,MNC and docker host ip (Open5GS VM ip) and UPF Advertise IP** <br>
**Step 9** : cd open5gs/docker_open5gs <br>
**Step 10**: Change IP in .env file.  (sample .env file attached) <br>
**Step 11**: Under amf section in docker compose file (sa-deploy.yaml), uncomment the following part (sample sa-deploy.yaml file attached) <br>
under amf section <br>
 ports: <br>
   - "38412:38412/sctp" 
Then, uncomment the following part under upf section <br>
  ports: <br>
    - "2152:2152/udp" <br>

**Subscriber Addition** <br>

**Step 12**: Open (http://<DOCKER_HOST_IP>:3000) in a web browser, where <DOCKER_HOST_IP> is the IP of the machine/VM running the open5gs containers. <br>
            Login with the following credentials. <br>
            **Username** : admin <br>
            **Password** : 1423 <br>
**Step 13**: Run the open5gs core <br>
            
             sudo docker-compose -f sa-deploy.yaml up --remove-orphans 
**Step 14**: To stop the open5gs core <br>
              Press two times ctrl+c <br>
**Step 15**: Verify Docker process  <br>

              sudo docker ps



