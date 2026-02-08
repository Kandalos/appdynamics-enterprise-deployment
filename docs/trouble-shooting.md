# If Java Script Database Failed to start 
Change directory to``` /opt/appdynamics/platform/product/eum/orcha/orcha-manager/bin```
Run:
```
./orcha-manager -d mysql.groovy -p ../../playbooks/mysql-orcha/start-mysql.orcha -o ../conf/orcha.properties -c local
```

---
# AirG-gapped Real User Monitoring Using a Localized cdn
nginx as CDN server
•	Add the following section to the nginx config file:
```
server {
   listen 8080;
   location /adrum {
root   /opt/jsagent;
   }
}
```
