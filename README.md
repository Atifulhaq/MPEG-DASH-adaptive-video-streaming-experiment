# MPEG-DASH-adaptive-video-streaming-experiment

# Project Overview

This repository contains the implementation and experimental evaluation of a MPEG-DASH adaptive video streaming system developed in a virtualized Linux environment. The aim of the project is to investigate how different network control mechanisms affect video streaming performance and quality of experience (QoE).

The experiment evaluates the impact of network bandwitdh limitations, traffic prioritization and packet loss on adaptive streaming performance. Linux traffic control mechanisms such as token bucket filter (TBF), hierarchical token bucket (HTB) and traffic policing were implemented to simulate different network conditions.

The system was deployed by using two virtual machines, one machine acting as the streaming server and the other acting as the streaming client.


# System architecture

The sreaming pipeline follows the standard MPEG-DASH architecture:

1. Obtaining video content
2. Transcoding video into multiple different bitrates
3. DASH segmentation and packaging
4. Hosting segments on an Apache web server
5. Client side playback through a web browser

The adaptive client dynamically selects the suitable video bitrate representation depending on available bandwitdh conditions.


# Virtual machine environment

Two virtual machines were configured using Oracle VirtualBox.


Server VM
 
•	Operating system: Debian (64 bit)
•	CPU: 2
•	Memory: 2048MB
•	Storage: 20 GB virtual disk
•	Network: NAT with internet access

Client VM

•	Operating system: Ubuntu (64 bit)
•	CPU: 2
•	Memory: 2048MB
•	Storage: 20 GB virtual disk
•	Network: NAT with internet access

VM System Details
<img width="513" height="290" alt="image" src="https://github.com/user-attachments/assets/b4e10474-7f58-4e78-b825-de67706adc9c" />



