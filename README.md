# Network Traffic Analysis

# Here is a background information on the task
Suspicious network activity has been detected coming from a user on the ANZ network.

A laptop has been flagged up on our security systems due to suspicious internet traffic, and we need you to investigate the network traffic in order to establish what the user accessed and downloaded.

Your task is to examine their network activity and gather what information you can on what images they viewed and what files they accessed.

You have been provided with a packet capture file (pcap) containing all their recent network activity. There may be a number of artifacts contained within the packet capture file, and you will be expected to identify and report as many as possible.

Note: Before you begin, please note that the relevant traffic is all in http.

# Below is also a document that details how I am expected to carry out each of these tasks.

![Image1](https://github.com/JosephAdeoye/packet-analysis/assets/66190309/52d462f8-81f4-4798-acb4-527def063bd6)

# Tools I used to carry out this task

- Wireshark
- HxD (Hex Editor)
- Paint — for image annotation

#  Network Traffic Analysis Workflow
Network Traffic Analysis workflows can be approached in various ways, but the method I have observed experts use, which I've also adopted, typically follows this pattern:

- Ingest Traffic: refers to the initial step of collecting and importing network data, often through packet capture or log files, for further analysis and examination of network activity.

- Reduce Noise by Filtering: aims to eliminate irrelevant or extraneous data to focus on meaningful network traffic patterns.

- Analyse and Explore: involves examining and investigating network data by applying specific filters to uncover valuable insights and anomalies.

- Detect and Alert: involves identifying suspicious or significant network events by applying specific filters to network traffic data, triggering alerts or notifications for further investigation.

It is also important to note that the steps above are iterative which means we can go over the steps severally as we discover new information about our network traffic. Using the above workflow I will be carrying out this Network Traffic Analysis task as provided by ANZ.

# Ingest Traffic
I will begin by importing the traffic data into our Network Traffic Analyzer, in this case, Wireshark. ANZ has provided the Packet Capture file, which I will open using Wireshark.

![image2](https://github.com/JosephAdeoye/packet-analysis/assets/66190309/48a7b828-6fbf-41d2-96f0-96031d6ff17d)

So, the image above is what we typically see when we open a packet capture file with Wireshark. There are three main panes in the Wireshark GUI

- Packet List: This is the area highlighted in yellow. Here, we see a summary line of each packet including source and destination IP addresses, protocol, time, etc.

- Packet Details: This is the area highlighted in green. This window allows us to drill down into the packet to inspect the protocols with greater detail. It will break it down into chunks that we would expect following the typical OSI Model reference.

- Packet Bytes: This is the area highlighted in red. The Packet Bytes window allows us to look at the packet contents in ASCII or hex output.

# Reduce Noise by filtering
From the instruction provided by ANZ, we understand that the relevant traffic for this task is all in HTTP. We therefore take the next step in the Network Traffic Analysis workflow by reducing noise by filtering.

![image](https://github.com/JosephAdeoye/packet-analysis/assets/66190309/d50826de-3d18-425f-b90f-edf3efd98d95)

In the image above, I applied the HTTP filter in the area highlighted in red. As a result in our Packet list window highlighted in yellow, if we take a look at the protocol field, we can see that every protocol here is HTTP showing that our filter has been effectively applied. The benefit of this is that we are able to focus on traffic that actually matters in our case study. In the packet details window, highlighted in green, we can see more information about the packet, the user-agent, the type of file, etc.

# Analyse and Explore
The first task we are required to complete according to the documentation provided is:

anz-logo.jpg and bank-card.jpg are two images that show up in the users’ network traffic.

Extract these images from the Pcap file and attach them to your report.
