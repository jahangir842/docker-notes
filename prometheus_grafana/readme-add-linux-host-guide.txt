**************************************************************************************
Prometheus Configuration: Add a Linux host 
**************************************************************************************

Install the Node Exporter

Download the Node Exporter:**

   wget https://github.com/prometheus/node_exporter/releases/download/v1.5.0/node_exporter-1.5.0.linux-amd64.tar.gz
   
************************************************************************************** 
Extract the archive:**

   tar xvfz node_exporter-1.5.0.linux-amd64.tar.gz
   cd node_exporter-1.5.0.linux-amd64
**************************************************************************************
To run the Node Exporter Temporarily

   ./node_exporter
**************************************************************************************
To run the Node Exporter as a Permanant service, you can create a systemd service file:

   sudo nano /etc/systemd/system/node_exporter.service
**************************************************************************************
Add the following content to the service file:
**************************************************************************************
[Unit]
Description=Node Exporter
Wants=network-online.target
After=network-online.target

[Service]
User=node_exporter
ExecStart=/usr/local/bin/node_exporter
Restart=on-failure

[Install]
WantedBy=default.target

**************************************************************************************
   Replace `/path/to/node_exporter` with the actual path where `node_exporter` is located.
   
************************************************************************************** 
   
Create Node Exporter User

Create a dedicated user for running Node Exporter.

	sudo useradd --no-create-home --shell /bin/false node_exporter

Set the ownership of the Node Exporter binary to the new user.

	sudo chown node_exporter:node_exporter /usr/local/bin/node_exporter   
   
**************************************************************************************
Enable and start the Node Exporter service:**

   sudo systemctl daemon-reload
   sudo systemctl enable node_exporter
   sudo systemctl start node_exporter

**************************************************************************************
Restart the system if services having errors
**************************************************************************************
Edit the Prometheus configuration file (prometheus.yml):**

   sudo vim /etc/prometheus/prometheus.yml

Add a new job for the Node Exporter:**
**************************************************************************************
   scrape_configs:
     - job_name: 'node_exporter'
       static_configs:
         - targets: ['<Linux-host-IP>:9100']

**************************************************************************************
Replace `<Linux-host-IP>` with the IP address of your Linux host. The default port for Node Exporter is `9100`.
**************************************************************************************

Restart Prometheus

	docker-compose restart prometheus
	
**************************************************************************************	

1. **Check the status of Node Exporter:**


   sudo systemctl status node_exporter

**************************************************************************************	

Test Connectivity in terminal:


    curl http://<your_rocky_linux_ip>:9100/metrics

**************************************************************************************
Test Connectivit in browser:

Verify Prometheus is scraping the Node Exporter:**

   Open your Prometheus web interface (usually available at `http://<prometheus-server-IP>:9090`) and go to `Status -> Targets`. You should see the Node Exporter listed and marked as `UP`.

**************************************************************************************
configure the firewall (if enabled)
**************************************************************************************
    Check the Firewall Status:

	sudo firewall-cmd --state
	sudo firewall-cmd --list-all
**************************************************************************************
Allow Port 9100:

sudo firewall-cmd --permanent --add-port=9100/tcp
sudo firewall-cmd --reload
**************************************************************************************
Verify the Change:

sudo firewall-cmd --list-all
**************************************************************************************






