## Failed RDP authentication

I had deployed windows server with RDP port open. After looking up the logs around 20 days later, i could see many authentication failure. 
Event ID 4625 (viewed in Windows Event Viewer) documents every failed attempt at logging on to a local computer. This event is generated on 
the computer from where the logon attempt was made. 

![image](https://github.com/user-attachments/assets/6ece5bdd-a828-4f4a-a5ac-d186142b0ce7)

Let's create the alert for this type of event to lookup easily if any same event triggers for last 5 minutes when the count is above 5. 
The counts wil be usully high within a seconds when someone tries to bruteforce attack it cause attacker usually use different dictionary
attacks and large number of combination of username and password.  

## Rule for SSH-brute-force-attempt on linux server 
 FOR USERNAME : root and failed attempts
![image](https://github.com/user-attachments/assets/33fc48e9-8a98-4bcd-9ba3-a2fef20b1891)

## Map in elastic search for failed RDP on windows server

- Almost 200k were coming from Russia. (As expected)
  ![image](https://github.com/user-attachments/assets/9ea5c024-1a68-45c7-8f5a-da3158042115)

  Attempts from Nepal too :)
![image](https://github.com/user-attachments/assets/cea44b51-cbae-47ad-9421-889782f7fc21)

  
  
