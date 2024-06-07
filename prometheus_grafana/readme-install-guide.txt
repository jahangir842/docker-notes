**************************************************************************************
	Docker Compose to manage both Prometheus and Grafana with a single YAML 
**************************************************************************************
create a directory for prometheus_grafana and open this with following command

	touch prometheus_grafana
	cd prometheus_grafana

**************************************************************************************
Download Docker Images on Online System

   
   docker pull prom/prometheus 
   docker pull grafana/grafana
   
**************************************************************************************
Create Docker Compose File

   mkdir prometheus_grafana
   cd prometheus_grafana
   
**************************************************************************************
Create the Prometheus configuration file (`prometheus.yml`)
**************************************************************************************
   global:
     scrape_interval: 15s

   scrape_configs:
     - job_name: 'prometheus'
       static_configs:
         - targets: ['prometheus:9090']
   
**************************************************************************************
Save this file as `prometheus.yml` in the `prometheus_grafana` directory
**************************************************************************************
Create the Docker Compose file (`docker-compose.yml`)
**************************************************************************************
version: '3.8'

services:
  prometheus:
    image: prom/prometheus
    container_name: prometheus
    restart: unless-stopped
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml
      - prometheus-storage:/prometheus
    ports:
      - "9090:9090"

  grafana:
    image: grafana/grafana
    container_name: grafana
    restart: unless-stopped
    ports:
      - "3000:3000"
    environment:
      - GF_SECURITY_ADMIN_USER=admin
      - GF_SECURITY_ADMIN_PASSWORD=admin
    volumes:
      - grafana-storage:/var/lib/grafana

volumes:
  grafana-storage:
  prometheus-storage:

**************************************************************************************
Grafana Persistant Data:
**************************************************************************************     
 By default, Grafana uses an embedded SQLite version 3 database to store configuration, users, dashboards, and other data in /var/lib/grafana
**************************************************************************************
Save this file as `docker-compose.yml` in the `prometheus_grafana` directory.
**************************************************************************************             
permission to the data folder will be required to run prometheus container	
	sudo chmod -R 777 ./data 
	sudo chmod -R 777 ./grafana-storage   
**************************************************************************************
Run Docker Compose on Offline System

Navigate to the `prometheus_grafana` directory:

   cd prometheus_grafana
   
Start the services using Docker Compose:**

   docker-compose up -d
  
**************************************************************************************
start Docker containers automatically using Docker Compose
**************************************************************************************
Create a systemd service file:

sudo nano /etc/systemd/system/docker-compose-app.service
**************************************************************************************
Define the systemd service:
**************************************************************************************

[Unit]
Description=Prometheus
After=network.target docker.service
Requires=docker.service

[Service]
WorkingDirectory=/home/username/myproject
ExecStart=/usr/local/bin/docker-compose up
ExecStop=/usr/local/bin/docker-compose down
Restart=always
User=root
Group=root

[Install]
WantedBy=multi-user.target

**************************************************************************************
Replace /home/username/myproject with the path to your Docker Compose file. Also, replace username with your actual username.
**************************************************************************************
Reload systemd and enable the service:

	sudo systemctl daemon-reload
	sudo systemctl enable docker-compose-app.service

**************************************************************************************
Start the service:

	sudo systemctl start docker-compose-app.service
**************************************************************************************
Check the status:

	sudo systemctl status docker-compose-app.service
**************************************************************************************
If you need to make any changes to your Docker Compose setup, simply modify your docker-compose.yml file and restart the service using:

	sudo systemctl restart docker-compose-app.service


**************************************************************************************

Access the prometheus:
	http://localhost:9090
	
Access the prometheus:
	http://localhost:3000

















