- ssh into ubuntu server 
- Copy appropriate download link address for Kibana
- use wget (appropriate download link) for kibana. 
- Install with command `dpkg -i (downloaded file)
- edit the configuration file of kibana(kibana.yml)
- Changes that are to be done are : server.port and server.host.

```

root@Shellwizz1337-ELK:~# ls
elasticsearch-8.15.0-amd64.deb  kibana-8.15.0-amd64.deb  snap
root@Shellwizz1337-ELK:~# dpkg -i kibana-8.15.0-amd64.deb
Selecting previously unselected package kibana.
(Reading database ... 86887 files and directories currently installed.)
Preparing to unpack kibana-8.15.0-amd64.deb ...
Unpacking kibana (8.15.0) ...
Setting up kibana (8.15.0) ...
Creating kibana group... OK
Creating kibana user... OK
Kibana is currently running with legacy OpenSSL providers enabled! For details and instructions on how to disable see https://www.elastic.co/guide/en/kibana/8.15/production.html#openssl-legacy-provider
Created Kibana keystore in /etc/kibana/kibana.keystore
root@Shellwizz1337-ELK:~# nano /etc/kibana/kibana.yml
```


- After done configuring, start the service and check status of kibana.
```
root@Shellwizz1337-ELK:~# nano /etc/kibana/kibana.yml
root@Shellwizz1337-ELK:~# systemctl daemon-reload
root@Shellwizz1337-ELK:~# systemctl enable kibana.service
Created symlink /etc/systemd/system/multi-user.target.wants/kibana.service → /lib/systemd/system/kibana.service.
root@Shellwizz1337-ELK:~# systemctl start kibana.service
root@Shellwizz1337-ELK:~# systemctl status kibana.service
● kibana.service - Kibana
     Loaded: loaded (/lib/systemd/system/kibana.service; enabled; vendor preset: enabled)
     Active: active (running) since Thu 2024-09-05 06:52:00 UTC; 13s ago
       Docs: https://www.elastic.co
   Main PID: 5439 (node)
      Tasks: 11 (limit: 19042)
     Memory: 298.1M
        CPU: 8.564s
     CGroup: /system.slice/kibana.service
             └─5439 /usr/share/kibana/bin/../node/glibc-217/bin/node /usr/share/kibana/bin/../src/cli/dist

Sep 05 06:52:00 Shellwizz1337-ELK kibana[5439]: Kibana is currently running with legacy OpenSSL providers enabled! For details and instructions on how to disable see https://www.elastic.co/guide/en/kibana/8.15/production.html#openssl-legacy-provider
Sep 05 06:52:00 Shellwizz1337-ELK kibana[5439]: {"log.level":"info","@timestamp":"2024-09-05T06:52:00.783Z","log.logger":"elastic-apm-node","ecs.version":"8.10.0","agentVersion":"4.7.0","env":{"pid":5439,"proctitle":"/usr/share/kibana/bin/../node/glibc-217/bin/node","os":"linux 5.15.0-119-generic","arch":"x64","hos>
Sep 05 06:52:00 Shellwizz1337-ELK kibana[5439]: Native global console methods have been overridden in production environment.
Sep 05 06:52:01 Shellwizz1337-ELK kibana[5439]: [2024-09-05T06:52:01.751+00:00][INFO ][root] Kibana is starting
Sep 05 06:52:01 Shellwizz1337-ELK kibana[5439]: [2024-09-05T06:52:01.802+00:00][INFO ][node] Kibana process configured with roles: [background_tasks, ui]
Sep 05 06:52:06 Shellwizz1337-ELK kibana[5439]: [2024-09-05T06:52:06.844+00:00][INFO ][plugins-service] The following plugins are disabled: "cloudChat,cloudExperiments,cloudFullStory,profilingDataAccess,profiling,securitySolutionServerless,serverless,serverlessObservability,serverlessSearch".
Sep 05 06:52:06 Shellwizz1337-ELK kibana[5439]: [2024-09-05T06:52:06.908+00:00][INFO ][http.server.Preboot] http server running at http://144.202.4.95:5601
Sep 05 06:52:07 Shellwizz1337-ELK kibana[5439]: [2024-09-05T06:52:07.027+00:00][INFO ][plugins-system.preboot] Setting up [1] plugins: [interactiveSetup]
Sep 05 06:52:07 Shellwizz1337-ELK kibana[5439]: [2024-09-05T06:52:07.037+00:00][INFO ][preboot] "interactiveSetup" plugin is holding setup: Validating Elasticsearch connection configuration…
Sep 05 06:52:07 Shellwizz1337-ELK kibana[5439]: [2024-09-05T06:52:07.067+00:00][INFO ][root] Holding setup until preboot stage is completed.
lines 1-21/21 (END)
```
- Generate a elasticsearch enrollment token fo Kibana
```
 root@Shellwizz1337-ELK:~# cd /usr/sahre/elasticsearch/bin
root@Shellwizz1337-ELK:~# cd /usr/share/elasticsearch/bin
root@Shellwizz1337-ELK:/usr/share/elasticsearch/bin# ls
elasticsearch           elasticsearch-cli                      elasticsearch-env            elasticsearch-keystore  elasticsearch-reconfigure-node  elasticsearch-service-tokens   elasticsearch-sql-cli             elasticsearch-users
elasticsearch-certgen   elasticsearch-create-enrollment-token  elasticsearch-env-from-file  elasticsearch-node      elasticsearch-reset-password    elasticsearch-setup-passwords  elasticsearch-sql-cli-8.15.0.jar  systemd-entrypoint
elasticsearch-certutil  elasticsearch-croneval                 elasticsearch-geoip          elasticsearch-plugin    elasticsearch-saml-metadata     elasticsearch-shard            elasticsearch-syskeygen
root@Shellwizz1337-ELK:/usr/share/elasticsearch/bin# ./elasticsearch-create-enrollment-token --scope kibana
```

- Add rule to the firewall allowing tcp connection from all the ports with only your ip and save the rule then proceed to browse the http://ipaddress:port
- It may not render the elastic configure website. To troubleshoot, try looking for service status for both kibanasearch and elastic. And allow port 5601 to your ubuntu server too using ufw .
- Now, the website gets loaded. Paste in the box the elasticsearch enrollment token you saved before. After that it will ask for the verification which you can find following way:
  ```
  root@Shellwizz1337-ELK:/usr/share/elasticsearch/bin# cd /usr/share/kibana/bin
  root@Shellwizz1337-ELK:/usr/share/kibana/bin# ./kibana-verification-code
  ```
  - Then you will get login prompt code. if you had forgot the password for elastic(as i did), you can reset using the following command:
    `Your verification code is:  315 393
root@Shellwizz1337-ELK:/usr/share/kibana/bin# /usr/share/elasticsearch/bin/elasticsearch-reset-password -u 'elastic'
This tool will reset the password of the [elastic] user to an autogenerated value.
The password will be printed in the console.
Please confirm that you would like to continue [y/N]y`

- Boom!!! Now you are logged in to elastic..... Poke around the web GUI.
- Go the the Security > alert > asks for `API integration key required. A new encryption key is generated for saved objects each time you start Kibana. Without a persistent key, you cannot delete or modify rules after
  Kibana restarts. To set a persistent key, add the xpack.encryptedSavedObjects.encryptionKey setting with any text value of 32 or more characters to the kibana.yml file.` . To get those, use command :
  `root@Shellwizz1337-ELK:/usr/share/kibana/bin# ./kibana-encryption-keys generate`
- To clear all those warning, we need to add the three xpack keys.
```  
root@Shellwizz1337-ELK:/usr/share/kibana/bin# ls
kibana  kibana-encryption-keys  kibana-health-gateway  kibana-keystore  kibana-plugin  kibana-setup  kibana-verification-code
root@Shellwizz1337-ELK:/usr/share/kibana/bin# ./kibana-keystore add
error: missing required argument 'key'
root@Shellwizz1337-ELK:/usr/share/kibana/bin# ./kibana-keystore add xpack.encryptedSavedObjects.encryptionKey
Enter value for xpack.encryptedSavedObjects.encryptionKey:
root@Shellwizz1337-ELK:/usr/share/kibana/bin# ./kibana-keystore add xpack.reporting.encryptionKey
Enter value for xpack.reporting.encryptionKey: ********************************
root@Shellwizz1337-ELK:/usr/share/kibana/bin# ./kibana-keystore add xpack.encryptedSavedObjects.encryptionKey
Setting xpack.encryptedSavedObjects.encryptionKey already exists. Overwrite? [y/N] y
Enter value for xpack.encryptedSavedObjects.encryptionKey: ********************************
root@Shellwizz1337-ELK:/usr/share/kibana/bin# ./kibana-keystore add xpack.security.encryptionKey
Enter value for xpack.security.encryptionKey: ********************************
root@Shellwizz1337-ELK:/usr/share/kibana/bin# systemctl restart kibana.service
```


- After restarting kibana service, and reloading the website, kibana is successfully installed. 
