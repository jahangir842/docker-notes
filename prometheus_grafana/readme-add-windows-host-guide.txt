**************************************************************************************
Prometheus Add Windows host
**************************************************************************************

Download the Windows Exporter:
   - Go to https://github.com/prometheus-community/windows_exporter/releases/tag/v0.25.1
Download  windows_exporter-0.25.1-amd64.exe and install on windows host.

**************************************************************************************


Edit the Prometheus configuration file (prometheus.yml):**

   sudo vim /etc/prometheus/prometheus.yml

Add a new job for the Node Exporter:**


**************************************************************************************
     scrape_configs:
       - job_name: 'windows_exporter'
         static_configs:
           - targets: ['<windows-host-ip>:9182']
     
**************************************************************************************
Replace `<Linux-host-IP>` with the IP address of your Linux host. The default port for Node Exporter is `9100`.
**************************************************************************************

Restart Prometheus

	sudo docker-compose restart prometheus
	
**************************************************************************************	

Test Connectivity in terminal:


    curl http://<your_rocky_linux_ip>:9100/metrics

**************************************************************************************
Test Connectivit in browser:

Verify Prometheus is scraping the Node Exporter:**

   Open your Prometheus web interface (usually available at `http://<prometheus-server-IP>:9090`) and go to `Status -> Targets`. You should see the Node Exporter listed and marked as `UP`.
**************************************************************************************	
