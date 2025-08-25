## ✅ Step-by-Step: Run mysqld_exporter as a Service

### 🐬 Install mysql server in target machine if not already Installed.
```
apt update
apt install mysql-server
systemctl start mysql
systemctl enable mysql
systemctl status mysql
```
Installs and starts MySQL on the target machine.
Ensures MySQL starts automatically on boot.

### 📝 create mysql user and database for mysqld_exporter
```
mysql -u root -p
mysql> CREATE USER 'mysqld_exporter'@'localhost' IDENTIFIED BY 'StrongPassword';
mysql> GRANT PROCESS, REPLICATION CLIENT, SELECT ON *.* TO 'mysqld_exporter'@'localhost';
mysql> FLUSH PRIVILEGES;
mysql> EXIT
```
Creates a MySQL user with minimal privileges needed for monitoring.


### 📦 Download mysqld_exporter Binary
#### Get the latest version from Prometheus GitHub:
https://prometheus.io/download/#mysqld_exporter
```sh
sudo curl -LO https://github.com/prometheus/mysqld_exporter/releases/download/v0.17.2/mysqld_exporter-0.17.2.linux-amd64.tar.gz
```
#### or RUN below cmd to automatically get the latest version:
```sh
curl -s https://api.github.com/repos/prometheus/mysqld_exporter/releases/latest | grep browser_download_url | grep linux-amd64 | cut -d '"' -f 4 | wget -qi -
```
Fetches the latest release URL for Linux from GitHub and downloads it using wget.
#### unzip using tar
```sh
sudo tar xvf mysqld_exporter*.tar.gz
```
#### rename the mysqld_exporter-0.17.2.linux-amd64 to a shorter name - mysqld_exporter
```sh
sudo mv mysqld_exporter-*.linux-amd64 mysqld_exporter
```
### 👤 Create a System User
```sh
sudo useradd -rs /bin/false mysqld_exporter
```
Creates a system user and group named mysqld_exporter with no login shell or home directory.
This user will run the mysqld_exporter service securely.
### 📝 Configure Credentials
```sh
sudo vim /etc/.mysqld_exporter.cnf
```
paste the following
```sh
[client]
user=mysqld_exporter
password=StrongPassword
```
Stores MySQL credentials in a config file.  
Used by mysqld_exporter to authenticate. 

Update ownership so only the exporter can read its MySQL credentials:
```sh
sudo chown mysqld_exporter:mysqld_exporter /etc/.mysqld_exporter.cnf
sudo chmod 640 /etc/.mysqld_exporter.cnf
```
### 📂 Move Binary to /usr/local/bin
```sh
sudo mv mysqld_exporter-*.linux-amd64/mysqld_exporter /usr/local/bin/
sudo chmod +x /usr/local/bin/mysqld_exporter
sudo chown mysqld_exporter:mysqld_exporter /usr/local/bin/mysqld_exporter
```
### 🔍 Check Version
```sh
mysqld_exporter --version
```
Verifies that the exporter is installed correctly.


### 4️⃣ Create a Systemd Service File
#### Create the service unit:

```sh
sudo vi /etc/systemd/system/mysql_exporter.service
```
#### Paste the following:

```sh
[Unit]
Description=Prometheus MySQL Exporter
After=network.target
User=mysqld_exporter
Group=mysqld_exporter
 
[Service]
Type=simple
Restart=always
ExecStart=/usr/local/bin/mysqld_exporter \
--config.my-cnf /etc/.mysqld_exporter.cnf \
--collect.global_status \
--collect.info_schema.innodb_metrics \
--collect.auto_increment.columns \
--collect.info_schema.processlist \
--collect.binlog_size \
--collect.info_schema.tablestats \
--collect.global_variables \
--collect.info_schema.query_response_time \
--collect.info_schema.userstats \
--collect.info_schema.tables \
--collect.perf_schema.tablelocks \
--collect.perf_schema.file_events \
--collect.perf_schema.eventswaits \
--collect.perf_schema.indexiowaits \
--collect.perf_schema.tableiowaits \
--collect.slave_status \
--web.listen-address=0.0.0.0:9104
 
[Install]
WantedBy=multi-user.target
```
Save and exit (:wq in Vim).
### 5️⃣ Start and Enable mysqld_exporter
```sh
sudo systemctl daemon-reload
sudo systemctl enable mysqld_exporter
sudo systemctl start mysqld_exporter
```
### 6️⃣ Verify mysqld_exporter is Running
#### Check status:

```sh
sudo systemctl status mysqld_exporter
```

#### Open in browser:

```sh
http://<server-ip>:9104/metrics
```
### 7️⃣ Add to Prometheus Targets
Edit your Prometheus config (prometheus.yml):
```sh
sudo vi /etc/prometheus/prometheus.yml
```

```sh
  - job_name: 'mysqld_exporter' # Name Identifier
    scrape_interval: 5s
    static_configs:
      - targets: ['server_ip:9104']
```
Then restart Prometheus:

```sh
sudo systemctl restart prometheus
```



Configure database credentials
```
vim /etc/.mysqld_exporter.cnf
```
```
[client]
user=mysqld_exporter
password=StrongPassword
```
Set ownership permissions
```
chown root:prometheus /etc/.mysqld_exporter.cnf
```
Create systemd unit file
```
vi /etc/systemd/system/mysql_exporter.service
```
```
[Unit]
Description=Prometheus MySQL Exporter
After=network.target
User=prometheus
Group=prometheus
 
[Service]
Type=simple
Restart=always
ExecStart=/usr/local/bin/mysqld_exporter \
--config.my-cnf /etc/.mysqld_exporter.cnf \
--collect.global_status \
--collect.info_schema.innodb_metrics \
--collect.auto_increment.columns \
--collect.info_schema.processlist \
--collect.binlog_size \
--collect.info_schema.tablestats \
--collect.global_variables \
--collect.info_schema.query_response_time \
--collect.info_schema.userstats \
--collect.info_schema.tables \
--collect.perf_schema.tablelocks \
--collect.perf_schema.file_events \
--collect.perf_schema.eventswaits \
--collect.perf_schema.indexiowaits \
--collect.perf_schema.tableiowaits \
--collect.slave_status \
--web.listen-address=0.0.0.0:9104
 
[Install]
WantedBy=multi-user.target
```
reload the daemon, start and enable the service
```
systemctl daemon-reload
systemctl enable mysql_exporter
systemctl start mysql_exporter
```
 
In prometheus server add to scrape config file
```
vim /etc/prometheus/prometheus.yml
```
```
- job_name: 'server1_db'
    scrape_interval: 5s
    static_configs:
      - targets: ['server_ip:9104']
```
In alert rules add customised rule for mysqld
for mysqld_exporter down alert rule
```
vim /etc/prometheus/rules/alert-rules.yml
```
```
alertmanager rules:
- alert: MysqlDown
    expr: mysql_up == 0
    for: 0m
    labels:
      severity: critical
    annotations:
      summary: MySQL down (instance {{ $labels.instance }})
      description: "MySQL instance is down on {{ $labels.instance }}\n  VALUE = {{ $value }}\n  LABELS = {{ $labels }}"
```
 
```
systemctl restart prometheus
systemctl restart grafana
systemctl restart node_exporter
systemctl restart alertmanager
```
 
mysqld exporter panel json file
```
https://github.com/prometheus/mysqld_exporter/blob/main/mysqld-mixin/dashboards/mysql-overview.json#L3
```
