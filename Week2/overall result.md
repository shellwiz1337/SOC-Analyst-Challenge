
## Looking for failed SSH
All the servers were running for around 20 days so i could get more data to analyze. Using discover menu in elastic with the 
required filters help to get lots of mapping on what was going on all the deployed servers 

Looking for the alerts(bruteforce attacks) on the dashboard shows  alot of alerts from these countries : 


![image](https://github.com/user-attachments/assets/69f64ba7-47d5-4fe1-8d2a-5adfe0d3e774)

### Failed Attempts

Looking for the failed attempts really shocked me within such short period of time. Hmm lets see down here 
all those failed attempts lol!  73,557 ????????


![image](https://github.com/user-attachments/assets/e3dc2dee-a2c6-449d-ac16-222c4dc36c89)


So, in real world we should probably create alert as a soc analyst. For that, we can go to the top bar and create rule and alerts
with our specific need and criteria. Lets just say i want my alert to check on every last 5 mins, when there is attempt of bruteforcing
with the count more than 5. I can simple create rule like this: 

![image](https://github.com/user-attachments/assets/f47a4d1b-c501-40fa-aceb-11285b88e5c1)

## Visualization Map

Creating map also helps in visualising easily. Below map shows failed ssh attempts :

![image](https://github.com/user-attachments/assets/7ddacb65-8602-4f9c-97df-0a7cbd81911c)



