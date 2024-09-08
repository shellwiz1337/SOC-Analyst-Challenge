We need to deploy ner server for fleet.
- I choosed ubuntu 22.04 with 4GB with not much additional features. Make sure to select it is in vpc network.
- Deplyoing it then go to our elastic web gui under management menu which have fleet option.
- From there we can add fleet server
![image](https://github.com/user-attachments/assets/3ca4a0ab-38fd-4c59-9ee4-9b2ea04cf6a7)

- Specify the public ip of our fleet server then generate fleet server policy.
- There will be option to install fleet server to a centralized host which you can copy to fleet server later on.
- Go back to fleet server , copy paste the commands for linux tar which differs according to the ip provided.
- Make sure to allow inbound connection in port 9200 in ELK server so that the fleet server can communicate with fleek server.
- After adding fleet agent, and successfully completing required steps . we can see the  logs on discover dashboard.


![Dashboard](https://github.com/user-attachments/assets/1540a126-f61e-420c-9434-aceec1cff66d)


![image](https://github.com/user-attachments/assets/74f701df-3aa2-4c03-957a-54336a4621b0)

