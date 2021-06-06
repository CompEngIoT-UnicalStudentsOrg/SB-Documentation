# EdgeCloudSim 

It supports three architecture in which we can test our system:

- 1-tier -> where we have devices directly connectend in a WLAN with the AP of a single edge server.
- 2-tier -> where devices are linked, not only whit their edge server but also through WAN to the CLOUD.
- 2-tier + EO -> here it is used and Edge Orchestrator that connects many edge servers and forms the edge level, now any devices connected can offfload tasks to another edge server that is not directly connected.

# 1-tier

![1-tier](https://user-images.githubusercontent.com/59933159/120916945-dc710100-c6ac-11eb-985f-bc11f6e65db9.png)

# 2-tier

![2-tier](https://user-images.githubusercontent.com/59933159/120916944-db3fd400-c6ac-11eb-99eb-3c03a07eac07.png)

# 2-tier + EO

![2-tier + EO](https://user-images.githubusercontent.com/59933159/120916946-dc710100-c6ac-11eb-8736-6b1dbe806b14.png)

# Modelling

Now we can use three different .xml configuration file in order to model the following componets:

- Scenario, for the scenario features like number of devices, edge servers, bandwidth ...
- Server, for modelling edge/cloud servers putting number of VM (istances), of cores, MIPS of CPU and so on ...
- Application, for modelling the application/service tasks putting DataAcquisitionRate (seconds), Task length (MI) and so on ... 

![modelling](https://user-images.githubusercontent.com/59933159/120917087-8781ba80-c6ad-11eb-8170-0c4f906d8066.png)
