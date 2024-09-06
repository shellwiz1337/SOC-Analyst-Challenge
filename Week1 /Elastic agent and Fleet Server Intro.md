## Elastic Agent
Elastic Agent is a single, unified way to add monitoring for logs, metrics, and other types of data to a host. It can also protect hosts from security threats, query data from operating systems,
forward data from remote services or hardware, and more. A single agent makes it easier and faster to deploy monitoring across your infrastructure. Each agent has a single policy you can update to
add integrations for new data sources, security protections, and more.

As the following diagram illustrates, Elastic Agent can monitor the host where it’s deployed, and it can collect and forward data from remote services and hardware where direct deployment is not possible.
![agent-architecture](https://github.com/user-attachments/assets/28d25303-42bc-4d23-a125-32c815aaef4a)

We will deploy elastic agent by the mode of managed by fleet . This mode can easily deploy services with the Fleet UI. Once installed, the Elastic agent lifecycle and policy/configuration is managed from a central point. 


## Fleet Server

Fleet Server is a component of the Elastic Stack used to centrally manage Elastic Agents. It’s launched as part of an Elastic Agent on a host intended to act as a server. One Fleet Server process can support many Elastic Agent connections, and serves as a control plane for updating agent policies, collecting status information, and coordinating actions across Elastic Agents.

Fleet Server is the mechanism Elastic Agents use to communicate with Elasticsearch:

  When a new agent policy is created, it’s saved to Elasticsearch.
  
  To enroll in the policy, Elastic Agents send a request to Fleet Server, using the enrollment key generated for authentication.
  
  Fleet Server receives the request and gets the agent policy from Elasticsearch, then ships the policy to all Elastic Agents enrolled in that policy.
  
  Elastic Agent uses configuration information in the policy to collect and send data to Elasticsearch.

  Elastic Agent checks into Fleet Server for updates, maintaining an open connection.
  
  When a policy is updated, Fleet Server retrieves the updated policy from Elasticsearch and sends it to the connected Elastic Agents.
  
    

![fleet-server-communication](https://github.com/user-attachments/assets/1e7f5704-05d2-46f9-b09f-5d495c977263)




