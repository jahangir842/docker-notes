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
version: '3.7'

services:
  prometheus:
    image: prom/prometheus
    container_name: prometheus
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml
      - ./data:/prometheus
    ports:
      - "9090:9090"

  grafana:
    image: grafana/grafana
    container_name: grafana
    ports:
      - "3000:3000"
    environment:
      - GF_SECURITY_ADMIN_USER=admin
      - GF_SECURITY_ADMIN_PASSWORD=admin
    volumes:
      - grafana-storage:/var/lib/grafana

volumes:
  grafana-storage:

         
 
**************************************************************************************
ave this file as `docker-compose.yml` in the `prometheus_grafana` directory.
**************************************************************************************             
permission to the data folder will be required to run prometheus container	
	sudo chmod -R 777 ./data    
**************************************************************************************
Run Docker Compose on Offline System

Navigate to the `prometheus_grafana` directory:

   cd prometheus_grafana
   
Start the services using Docker Compose:**

   docker-compose up -d
  
**************************************************************************************

Access the prometheus:
	http://localhost:9090
	
Access the prometheus:
	http://localhost:3000

















