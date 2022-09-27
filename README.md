# Prometheus Agent mode steps for linux
-------------------------------------

1. Download the binary - wget https://github.com/prometheus/node_exporter/releases/download/v0.18.1/node_exporter-0.18.1.linux-amd64.tar.gz


2. Extract the binary - tar -zxf node_exporter-0.18.1.linux-amd64.tar.gz

3. move the config to /usr/local/bin/ folder
cd node_exporter-0.18.1.linux-amd64
cp node_exporter /usr/local/bin/

3. Create a Linux Service for the binary
vi /etc/systemd/system/node_exporter.service

4. Service file content

START OF FILE CONTENT --------> 
[Unit]
Description=Node Exporter
After=network.target
 
[Service]
User=root
Group=root
Type=simple
ExecStart=/usr/local/bin/node_exporter  --collector.bcache --collector.bonding --collector.conntrack --collector.cpu --collector.cpufreq --collector.diskstats --collector.drbd --collector.edac --collector.entropy --collector.filefd --collector.filesystem --collector.hwmon --collector.infiniband --collector.interrupts --collector.ipvs --collector.ksmd --collector.loadavg --collector.logind --collector.mdadm --collector.meminfo --collector.meminfo_numa --collector.mountstats --collector.netclass --collector.netdev --collector.netstat --collector.nfs --collector.nfsd --collector.ntp --collector.pressure --collector.processes --collector.qdisc --collector.runit --collector.sockstat --collector.stat --collector.supervisord --collector.systemd --collector.tcpstat --collector.time --collector.timex --collector.uname --collector.filesystem.ignored-mount-points="" --collector.perf --collector.diskstats.ignored-devices=""

 
[Install]
WantedBy=multi-user.target

-----> END of content

4. Allow the port securely through firewall
ufw enable
ufw allow 9100
ufw reload

5. Start, enable and check the status of the prometheus node exporter service
sudo systemctl daemon-reload
sudo systemctl start node_exporter
sudo systemctl status node_exporter
sudo systemctl enable node_exporter
