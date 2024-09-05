 For setting up elastic search instance, we will use [vultr](https://vultr.com)

In this guide, we will create a Virtual Private Cloud (VPC) on Vultr, deploy a new server, and set up Elasticsearch on an Ubuntu 22.04 LTS machine.

Step 1: Create a Virtual Private Cloud (VPC)
Navigate to the Vultr dashboard and select VPC 2.0 under the network options.
Choose a network location, ensuring it matches the location of the virtual machine you will deploy later. For this example, I chose New York (NY).
Configure the IP range for the VPC. In my setup, I used the 172.31.0.0/24 IP range.
Assign a network name for your VPC.
Step 2: Deploy the Server
In the same location as your VPC (New York), deploy a new virtual machine with the following specifications:
Operating System: Ubuntu 22.04 LTS (x64)
Storage: 80GB NVMe
vCPUs: 4
Memory: 16GB
Bandwidth: 6TB
After deployment, access the server using SSH with PowerShell instead of the Vultr console. You will need the public IPv4 address, root account, and password provided.
Step 3: Update Repositories and Install Elasticsearch
First, update the server's package repositories:

sudo apt-get update && sudo apt-get upgrade -y


Download and install Elasticsearch:

Visit the official Elasticsearch Downloads Page and select Deb x86_64.

Copy the download link and use wget to download it:

wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-8.15.0-amd64.deb


Install the package using dpkg:
sudo dpkg -i elasticsearch-8.15.0-amd64.deb

Take note of the superuser password provided during installation, as you'll need it later.


Step 4: Configure Elasticsearch
Open the elasticsearch.yml configuration file:

sudo nano /etc/elasticsearch/elasticsearch.yml

Modify the following settings:

network.host: Assign your server’s public IP address to this field.
http.port: No need to change the default port (9200), just uncomment it.
This allows access to Elasticsearch from your Security Operations Center (SOC) analyst’s machine.

Step 5: Configure the Firewall
To secure the server, create firewall rules that only allow access to your IP address and only expose port 22 (SSH).

Block all other ports and restrict access to Elasticsearch from the internet to ensure maximum security.
Step 6: Start the Elasticsearch Service
Finally, enable and start the Elasticsearch service:

```
root@Shellwizz1337-ELK:/etc/elasticsearch# systemctl enable elasticsearch.service
root@Shellwizz1337-ELK:/etc/elasticsearch# systemctl enable elasticsearch.service
root@Shellwizz1337-ELK:/etc/elasticsearch# systemctl start elasticsearch.service
```
Check the service status to ensure it is running
```
root@Shellwizz1337-ELK:/etc/elasticsearch# systemctl status elasticsearch.service
● elasticsearch.service - Elasticsearch
     Loaded: loaded (/lib/systemd/system/elasticsearch.service; enabled; vendor preset: enabled)
     Active: active (running) since Wed 2024-09-04 21:17:57 UTC; 10s ago
       Docs: https://www.elastic.co
   Main PID: 3868 (java)
      Tasks: 91 (limit: 19042)
     Memory: 8.4G
        CPU: 58.567s
     CGroup: /system.slice/elasticsearch.service
             ├─3868 /usr/share/elasticsearch/jdk/bin/java -Xms4m -Xmx64m -XX:+UseSerialGC -Dcli.name=server -Dcli.script=/usr/share/elasticsearch/bin/elasticsearch -Dcli.libs=lib/tools/server-cli -Des.path.home=/usr/share/elasticsearch -Des.path.conf=/etc/elasticsearch -Des.distribution.type=deb -cp "/usr/share/ela>
             ├─3928 /usr/share/elasticsearch/jdk/bin/java -Des.networkaddress.cache.ttl=60 -Des.networkaddress.cache.negative.ttl=10 -Djava.security.manager=allow -XX:+AlwaysPreTouch -Xss1m -Djava.awt.headless=true -Dfile.encoding=UTF-8 -Djna.nosys=true -XX:-OmitStackTraceInFastThrow -Dio.netty.noUnsafe=true -Dio.n>
             └─3951 /usr/share/elasticsearch/modules/x-pack-ml/platform/linux-x86_64/bin/controller

Sep 04 21:17:39 Shellwizz1337-ELK systemd[1]: Starting Elasticsearch...
Sep 04 21:17:43 Shellwizz1337-ELK systemd-entrypoint[3868]: Sep 04, 2024 9:17:43 PM sun.util.locale.provider.LocaleProviderAdapter <clinit>
Sep 04 21:17:43 Shellwizz1337-ELK systemd-entrypoint[3868]: WARNING: COMPAT locale provider will be removed in a future release
Sep 04 21:17:57 Shellwizz1337-ELK systemd[1]: Started Elasticsearch.
lines 1-17/17 (END)
```

With this setup, you have successfully deployed and configured Elasticsearch on your Ubuntu server within a secure VPC environment.
