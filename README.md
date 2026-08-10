<img width="241" height="241" alt="image" src="https://github.com/user-attachments/assets/33252ee5-8751-4e2c-9b5f-8a46583793af" />

# HarpocratesEngine
HarpocratesEngine is a JAVA-based threat-detection and simulation engine environment that models out attack progression in a localized environment, combining incrementally trained ML model for anomaly based detection and a hivemind approach towards collaborating against pre-existing and zero-day threats.  

# Priorities 

1) Ground attack models in a credible framework rather than a taxonomy 
2) Support autonomous, attack framework and defensive framework through a shared interface 
3) provide visual, interactive connectivity in connection with the detection engine 
4) Log results and information logistics for review and audit support 
5) Encapsulate security validation 
6) Identify gaps in environmental control
7) Provide adequate security awareness of one's personalized environment
7) address resource allocation issues and path frequency 


<img width="2720" height="2400" alt="image" src="https://github.com/user-attachments/assets/fc976a04-2e9b-4620-b6b4-45ff36a47c55" />

# INFRASTRUCTURE ZONE 

IaC Provisioning -> Automating the creation, configuration and management of cloud infrastructure using machine-readable definition files instead of a manual setup. Allows infrastructure to act as software for version control, testing and CI/CD pipeline integration (Automated workflow moving software from code commit to production deployment - Continuous Integration and Continuous Delivery) - Utilized to define the desired state of our infrastructure (Servers, Networks, Storage and DBs) - provides consistency, speed, version control, scalability and security 

TOOL FOR IaC Provisioning -> Terraform, Ansible 

Lab Hosts -> Splunk lab environment on host machine and then universal forwarded sends logs from other hosts to Splunk interface. Search head and indexer cluster, ensures deployment is consistent across members. Data is taken from the detection engine and fed to the Splunk environment. 

TOOLS FOR Lab Hosts -> Splunk, Zeek, Hosts 

Wireguard -> encryption and communication protocol that a VPN uses to protect traffic channel opened up between devices and VPN servers. This provides multi-user access by assigning IP addresses and peers with public.private keys and the port the peers are listening on

Encryption used in WireGuard - ChaCha20 

Compatible with Android, IOS, Linux, macOS, and Windows 7+ 

# SIMULATION & ATTACK ENVIRONMENT

Attack Path Engine -> 
1) Ingests live data from local environment (EDR, sensors, events) 
2) Maps events to simulation nodes 
3) Updates the path of the attacker in detect events ~ IF event.X.isfound() THEN UPDATE graph.DATA() 
4) Streams path data to 3D simulation engine e.g., Unity or WebGL 

Algorithm Analysis -> 
1) Graph Traversal - Updates the affected part of the attack graph
2) Dijkstra Algorithm - Used to find the shortest possible attack path that COULD be taken through your local environment. This provides a failover between the CURRENT damaged path and the POTENTIAL damaged path 
3) Map Event to Node - Telemetry event maps to a specific node position in attack graph ~ NODE[X][Y] = event.RandomEvent() -> UPDATE GRAPH 
4) Path Reconstruction - Conducted through fixed mathematical operations
5) Low Latency - append the path of the tree rather than the tree itself 

Detection Engine -> 
1) Focus: Endpoint Threats and Network Attacks          `
2) Incremental Anomaly based detection with ML integration
3) Alert and feed data into simulation engine 
4) Collect data sources: 

|- Network Traffic - PCAP (Packet Capture), NetFlow, Zeek Logs (Network Meta-Data) 
|- Endpoint Telemetry - EDR logs, Sysmon (System Monitor - Windows system service and driver that remains resident across ssytem reboots to monitor and log system activity to the Windows event logger.)
|- Application logs - Web Server, DB 
|- Cloud Server logs - AWS CloudTrail (Management and Governance service that records and monitors all API calls and actions taken in a AWS account, auditing, compliance and operational troubleshooting), Azure Activity Logs 
|- Logs must be normalized into ECS or similar to ensure rules are consistently applied 


Machine Learning Framework Tool: Weka 
Data Ingestion: Apache Kafka, Parsing into JSON 
Feature Extraction: Raw Logs converted into Numerics (Java Stream)
Training Model: Train using Weka and save model into serialized format 

# Simulation Logic 
TOOL -> JBullet : dependency added using building tool E.G., Maven

It is required to add a physics world which is a dynamic environment. Local computerized environments are stored in a data file and this is loaded into the simulation class via. package importing . 

The environment base infrastructure includes a dispatcher and collision detection system in the event objects in the environment should interact with one another. 

Once data is loaded into the simulation class. Rigid bodies will be initialized with their corresponding objects from the loaded data environment. E.G., Computer Body = Scanned Local Computer Data Path | IDS = Detected Anti-Virus .exe Path 
