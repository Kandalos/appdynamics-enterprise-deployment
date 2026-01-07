
## Machine Agent Installation Guide

1. **Prepare Directory Structure**
Create a dedicated path for organization:
```bash
sudo mkdir -p /opt/appdynamics/agents/machine-agent

```


2. **Deploy Binaries**
Copy the compressed agent zip to the host and extract it:
```bash
sudo unzip machine-agent-xxx.zip -d /opt/appdynamics/agents/machine-agent

```


3. **Configure Connection**
Edit `conf/controller-info.xml`. Ensure the following parameters are accurate:
* **Controller Host:** Your Controller IP/FQDN
* **Controller Port:** (Default `8090` for HTTP or `8181` for HTTPS)
* **Account Access Key:** Retrieve from *Settings > License > Account*


4. **Enable Server Visibility**
Inside `controller-info.xml`, set `<sim-enabled>true</sim-enabled>` to view hardware metrics (CPU, Memory, Disk).
5. **Launch Agent**
Start the agent in the background so it continues running after you close the terminal:
```bash
nohup ./bin/machine-agent &

```



---

## Database Agent Installation Guide

1. **Prepare Directory Structure**
```bash
sudo mkdir -p /opt/appdynamics/agents/db-agent
sudo unzip db-agent-xxx.zip -d /opt/appdynamics/agents/db-agent

```


2. **Configure Controller Identity**
Edit `conf/controller-info.xml`. Enter your Controller Host, Port, and Account Access Key.
3. **Database User Provisioning**
Access the integrated AppDynamics MySQL to create the monitoring user:
```bash
cd /opt/appdynamics/platform/mysql
./bin/mysql --socket=mysql.sock -u root -p

```


Execute the MySQL 8.0 compatible script:
```sql
DROP USER IF EXISTS 'DBMon_Agent_User'@'%';
CREATE USER 'DBMon_Agent_User'@'%' IDENTIFIED BY 'Aa123456';
GRANT SELECT, PROCESS, SHOW DATABASES, REPLICATION CLIENT ON *.* TO 'DBMon_Agent_User'@'%';
FLUSH PRIVILEGES;

```


4. **Start the Agent**
Ensure **Java 17** or **Java 11** is installed (`java -version`). Run the startup script:
```bash
./start-dbagent &

```


5. **Configure Collector in UI**
* Navigate to: **Database** > **Configuration** > **Collectors** > **Add**.
* Choose **MySQL**.
* **Hostname:** Use the Controller IP.
* **Port:** `3388` (Default for AppD Integrated DB).
* **Credentials:** Use `DBMon_Agent_User` / `Aa123456`.
