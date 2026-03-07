# MPEG-DASH-adaptive-video-streaming-experiment

# Project Overview

This repository contains the implementation and experimental evaluation of a MPEG-DASH adaptive video streaming system developed in a virtualized Linux environment. The aim of the project is to investigate how different network control mechanisms affect video streaming performance and quality of experience (QoE).

The experiment evaluates the impact of network bandwitdh limitations, traffic prioritization and packet loss on adaptive streaming performance. Linux traffic control mechanisms such as token bucket filter (TBF), hierarchical token bucket (HTB) and traffic policing were implemented to simulate different network conditions.

The system was deployed by using two virtual machines, one machine acting as the streaming server and the other acting as the streaming client.
