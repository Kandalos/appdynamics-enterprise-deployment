## To start, run the following command:
Change directory to /opt/appdynamics/platform/product/eum/orcha/orcha-manager/bin
./orcha-manager -d mysql.groovy -p ../../playbooks/mysql-orcha/start-mysql.orcha -o ../conf/orcha.properties -c local

---

## nginx as CDN server
•	Add the following section to the nginx config file:

server {
   listen 8080;
   location /adrum {
root   /opt/jsagent;
   }
}
