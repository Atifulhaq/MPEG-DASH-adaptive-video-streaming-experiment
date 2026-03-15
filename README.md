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
 
1. Operating system: Debian (64 bit)
2. CPU: 2
3. Memory: 2048MB
4. Storage: 20 GB virtual disk
5. Network: NAT with internet access

Client VM

1. Operating system: Ubuntu (64 bit)
2. CPU: 2
3. Memory: 2048MB
4.	Storage: 20 GB virtual disk
5.	Network: NAT with internet access

VM System Details

<img width="513" height="290" alt="image" src="https://github.com/user-attachments/assets/b4e10474-7f58-4e78-b825-de67706adc9c" />


# FFmpeg Installation

FFmpeg was installed on the server virtual machine to perform video transcoding and DASH packaging.

Installation commands:

sudo apt update
sudo apt install ffmpeg

To verify:

ffmpeg -version

<img width="499" height="389" alt="image" src="https://github.com/user-attachments/assets/fbdd9c95-af02-4c38-b548-d9fd9319a941" />


# Video transcoding

The original video file was transcoded into three different bitrate representations in order to enable adaptive streaming.

Transcoding commands:

ffmpeg -i videoOne.mp4 -b:v 1500k videoOne_1500.mp4

ffmpeg -i videoOne.mp4 -b:v 2000k videoOne_2000.mp4

ffmpeg -i videoOne.mp4 -b:v 4000k videoOne_4000.mp4

These bitrate levels allow the DASH player to dynamically adapt video quality depending on the available bandwitdh.

<img width="483" height="380" alt="image" src="https://github.com/user-attachments/assets/f2bf76f2-b608-4be0-8774-29ee6705a34f" />



# MPEG-DASH stream generation 

After transcoding, the video files were packaged into the MPEG-DASH streaming format.

DASH packaging command:

ffmpeg -i videoOne.mp4 -map 0 -f dash videoOne_manifest.mpd


This process generates: DASH video segments and media presentation manifest file (MPD).

<img width="498" height="390" alt="image" src="https://github.com/user-attachments/assets/c6a18758-dc49-4b23-bfb8-801524a1eb3e" />


# Apache web server deployment

An Apache web server was installed on the server virtual machine to host the DASH video content.

Installation command:

sudo apt install apache2

The DASH files were placed in:

/var/www/html/

The video sream was then accessible via a web browser using the public server URL link.




# Video playback

The client virtual machine accessed the streaming server through a web browser by using a DASH compatible video player.

The player retrieves the MPD manifest file and dynamically downloads video segments based on current network conditions.


<img width="515" height="261" alt="image" src="https://github.com/user-attachments/assets/408a66cf-1cae-4aae-8867-feeec3a06a61" />


# Network traffic generation 

Network traffic was generated using iperf to simulate background network congestion.

iperf server command:

iperf -s

iperf client command:

iperf -c 10.0.2.15 -b 1M -t 60

This created background network traffic while the video stream was active.

<img width="514" height="403" alt="image" src="https://github.com/user-attachments/assets/64d8a7d4-7a83-4344-bc65-20ec91241057" />


# Traffic control experiments

Linux traffic control (tc) was used to emulate different network conditions.

Three different configurations were tested.


Token bucket filter (TBF)

The TBF mechanism was used to limit bandwidth to 2.5Mbps.

Configuration command:

tc qdisc add dev enp0s3 root tbf rate 2.5mbit burst 32kbit latency 50ms


Hierarchical token bucket (HTB)

HTB was used to prioritize video streaming traffic over background traffic.

Configuration command:

sudo tc qdisc add dev enp0s3 root handle 1: htb default 20


Traffic policing 

Traffic policing was applied to enforce strict bandwidth limits by dropping packets that exceed the defined rate.

This configuration resulted in frequent playback interruptions due to packet loss.
