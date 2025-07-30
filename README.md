# Deploying and Monitoring a React Application on AWS using Prometheus, Grafana & Node Exporters.

### Deployment Video
```

```
### Set up an two separate AWS EC2 instances one for Application Deployment and Another one for monitoring tools & Node Exporters.

1. Create an IAM user & login to your AWS Console
    - Access Type - Password
    - Permissions - Admin
2. Create an EC2 instance -1
    - Select an OS image - Ubuntu
    - Create a new key pair & download `.pem` file
    - Instance type - t2.micro
3. Create an EC2 instance -2
    - Select an OS image - Ubuntu
    - Instance type - t2.medium
4. Connecting to the instance using ssh
```
ssh -i instance.pem ubuntu@<IP_ADDRESS>
```

### Configure the both Ubuntu on remote VM

1. Updating the outdated packages and dependencies
```
sudo apt update
```
### On Ec2 -1 (Application)
1. Install Git 
```
sudo apt install git
```
2. Configure Node.js and npm
```
sudo apt install node
sudo apt install npm
```
3. Clone this project in the remote VM
```
git clone https://github.com/Mr-Surendar/App-Monitoring-with-Prometheus-Grafana.git
```
4. initialize and start the project
```
npm install
npm run start
```

> NOTE - We will have to edit the **inbound rules** in the security group of our EC2, in order to allow traffic from our required ports

5. Install Node Exporter
```
wget https://github.com/prometheus/node_exporter/releases/download/v1.9.1/node_exporter-1.9.1.linux-amd64.tar.gz
```
  - Unzip using
  ```
  xvf node_exporter-1.9.1.linux-amd64.tar.gz
  ```
  - Run the Package 
  ```
  ./ -exe
  ```
### On Ec2 -2 (Monitoring)
1. Install Prometheus
```
wget https://github.com/prometheus/prometheus/releases/download/v3.5.0/prometheus-3.5.0.linux-amd64.tar.gz
```
 - Unzip using
  ```
  xvf prometheus-3.5.0.linux-amd64.tar.gz
  ```
 - Run the Package 
  ```
  ./ -exe
  ```
2. Install Blackbox exporter
```
wget https://github.com/prometheus/blackbox_exporter/releases/download/v0.27.0/blackbox_exporter-0.27.0.linux-amd64.tar.gz
```
 - Unzip using
  ```
  xvf blackbox_exporter-0.27.0.linux-amd64.tar.gz
  ```
 - Run the Package 
  ```
  ./ -exe
  ```
3. Install Grafana
```
wget https://dl.grafana.com/enterprise/release/grafana-enterprise-12.1.0.linux-amd64.tar.gz
```
 - Unzip using
  ```
  xvf prometheus-3.5.0.linux-amd64.tar.gz
  ```
 - Run the Package 
  ```
  sudo systemctl daemon-reload
  sudo systemctl start grafana-server
  ```
### Link the Node Exporters with Prometheus 
1. Navigate to the Prometheus.yaml and setup the paths.
```
./prometheus --config.file=/path/to/your/prometheus.yml
```

### And finally link Prometheus with Grafana

## Done!