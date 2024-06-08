# Network Traffic Analysis

# Here is a background information on the task
Suspicious network activity has been detected coming from a user on the ANZ network.

A laptop has been flagged up on our security systems due to suspicious internet traffic, and we need you to investigate the network traffic to establish what the user accessed and downloaded.

Your task is to examine their network activity and gather what information you can on what images they viewed and what files they accessed.

You have been provided with a packet capture file (pcap) containing all their recent network activity. There may be several artefacts contained within the packet capture file, and you will be expected to identify and report as many as possible.

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

In the image above, I applied the HTTP filter in the area highlighted in red. As a result in our Packet list window highlighted in yellow, if we take a look at the protocol field, we can see that every protocol here is HTTP showing that our filter has been effectively applied. The benefit of this is that we can focus on traffic that matters in our case study. In the packet details window, highlighted in green, we can see more information about the packet, the user-agent, the type of file, etc.

# Analyse and Explore
The first task we are required to complete according to the documentation provided is:

**anz-logo.jpg** and **bank-card.jpg** are two images that show up in the users’ network traffic.

Extract these images from the Pcap file and attach them to your report.

![image](https://github.com/JosephAdeoye/packet-analysis/assets/66190309/eab79784-0741-4c28-928e-53bf90087820)

The second packet highlighted in blue in the above image is the response to the GET request from the user. In our Packet details pane, we need to right-click on **“File Data”** highlighted in yellow, then in the popup, we click on **“Export packet Bytes”**. Or we can simply press **“Ctrl + Shift + X”** which will take us to the file save page instantly.

![image](https://github.com/JosephAdeoye/packet-analysis/assets/66190309/588dc7ce-f16d-4e16-a32b-00b6e35f6364)

On the file save page, I entered the file name as shown in the image and then clicked on save. This is for the first image stated in our task. To get the second image, we repeat what we have done for the first image although this time, it would be on the 4th packet in the Packet list pane. After this is done, we can open the folder in which we have been saving these images and can expect to see the two images we exported from the Pcap file.

![image](https://github.com/JosephAdeoye/packet-analysis/assets/66190309/58c78fc6-e26b-4f05-ad53-237b3c563ea5)

In the image above, we can see our newly exported images which include the anz-logo and the image of a bank card. With that, we have completed our first sub-task. This is one method to extract image files from network traffic. Another method is to reconstruct the image with **HexEditor**. The steps to reconstruct with HxD are quite different.

![image](https://github.com/JosephAdeoye/packet-analysis/assets/66190309/c5ecc35f-fed5-4bbc-841a-f5a6277ff42e)

Here, we right-click on the first packet in our stream which is the GET request (we can alternatively select the second packet which is the reply). We then click on follow and in the subsequent popup, we click on **TCP Stream**.

![image](https://github.com/JosephAdeoye/packet-analysis/assets/66190309/6115242b-a82b-4868-8286-5f2d41f53c09)

We then see this window that gives us much more insight into our traffic. Here we can see:

- Host: specifies the domain name of the webserver to/from which the HTTP request is being sent.

- Connection: indicates whether the connection should be kept alive (e.g., "keep-alive") or closed ("close") after the current request/response is completed. "Keep-alive" allows for multiple requests to be made over a single TCP connection, reducing latency.

- Referer: indicates the URL of the page that referred the user to the current resource.

- User-Agent: provides information about the user's web browser or client application. This helps the web server understand the type of client making the request, which can be used for delivering optimized content.

- Accept-Encoding: specifies the encoding algorithms supported by the client for content compression. Common values include "gzip," "deflate," and "br" (Brotli).

- Status Code: The HTTP status code in the response, indicating whether the request was successful or encountered an error (e.g., 200 for success, 404 for "Not Found," 500 for "Internal Server Error").

- Content-Type: specifies the type of the response content, which tells the client how to interpret the data (e.g., "image/jpeg" for a JPEG image).

There are many more information that can appear in this window. Some of the most important have been explained above.

![image](https://github.com/JosephAdeoye/packet-analysis/assets/66190309/da0e5968-7aa6-410b-a7d4-3791f6528059)

The above is what we see when the window opens up. So I made changes to this, in particular, I filtered the conversation to ensure that only data sent from **port 80 to TCP port 49294** are showing. This gets rid of unnecessary information in our stream. Then, I filtered it to show data in its raw format. See the red highlight in the image below.

![image](https://github.com/JosephAdeoye/packet-analysis/assets/66190309/3e172cf8-cd9b-4f4e-a623-43c7e4e62e24)

Now, the window is showing our image in its raw format. Typically, in some raw data formats, there are usually some padding to the actual data. A JPEG file typically begins with the hexadecimal value **"FFD8"** and ends with **"FFD9"**. The **"FFD8"** is the Start of the Image (SOI) marker, and the **"FFD9"** is the End of the Image (EOI) marker in the JPEG file format. These markers indicate the beginning and end of the image data within the file.

So, what we want to do in this case is to look for **FFD8** (Start of the Image indicator) and start copying from there till we get to **FFD9** (End of the Image indicator).

![image](https://github.com/JosephAdeoye/packet-analysis/assets/66190309/d5c60764-9c7d-44ed-b30d-87da4264d6df)

The red highlighted **FFD8** above indicates the Start of the Image marker. I searched that by entering **FFD8** in the find tab highlighted in green. Having copied our raw file, I opened my HxD software and pasted the raw file format.

![image](https://github.com/JosephAdeoye/packet-analysis/assets/66190309/3657ecc4-8158-45ed-9b1b-dbeffeb57271)

After pasting the raw file in HxD, I pressed **ctrl + S** to save the file.

![image](https://github.com/JosephAdeoye/packet-analysis/assets/66190309/9f3f2a29-0b48-44f8-bf91-d7e5dfe5325a)

Here I saved the file with **anz-logo1.jpg** because the first file I extracted directly from the stream is saved as **anz-logo.jpg.**

If I open my ANZ folder, I can expect to see the new image that I just extracted and reconstructed with HxD.

![image](https://github.com/JosephAdeoye/packet-analysis/assets/66190309/c040eec0-7a44-402a-8eda-767e129e730a)

With this, I have demonstrated two ways to extract images from our Pcap file.

To avoid repetition, I will skip the other tasks that require me to extract images from the Pcap file and try something different. To this effect, I will carry out **Sub-task 4** which requires me to:

- *The user accessed 3 pdf documents: ANZ_Document.pdf, ANZ_Document2.pdf, evil.pdf*

- *Extract and view these documents. Include images of them in your report.*

Extracting a PDF from our Pcap file is quite straightforward.

![image](https://github.com/JosephAdeoye/packet-analysis/assets/66190309/636cd5f3-9a60-4b42-afaf-1a637dd01942)

From the image above, first, I clicked on the reply to the GET request (highlighted in blue) for the pdf document (the third packet in this frame). Then in the packet details window, I right-clicked on File Data (highlighted in green). And finally, I clicked on export Packet Bytes.

![image](https://github.com/JosephAdeoye/packet-analysis/assets/66190309/dadec311-e08e-400f-b09c-c7c490a62b78)

I opened the directory where I saved the pdf and opened the pdf, the document contains:

![image](https://github.com/JosephAdeoye/packet-analysis/assets/66190309/614eae08-5d8c-4b88-a7c0-f73e60f4185d)

I repeated the steps above until I was able to extract the remaining files as required by the sub-task.

In conclusion, the network traffic analysis task provided me with valuable insights into traffic filtering, file extraction, and file reconstruction using a Hex Editor. The ability to extract files from a PCAP can assist security analysts in incident response, forensic analysis, as well as network monitoring.

If you are interested in viewing the actual document I submitted for this scenario, please follow this link to my Google Drive https://docs.google.com/document/d/1aX6dQl_P_g4NedKNfxzL5PEHV1A5ZJ7Z/edit?usp=drive_link&ouid=101975040340225214081&rtpof=true&sd=true
