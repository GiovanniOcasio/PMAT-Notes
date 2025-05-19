# Dynamic Analysis

## Table of Contents
- [Before Running the Malware](#before-running-the-malware)  
- [Running Malware and Network Signatures](#running-malware-and-network-signatures)  
- [Host-Based Indicators](#host-based-indicators)
  - [Procmon](#procmon)
  - [TCPView](#tcpview) 

<p align="center">
  <img src="../imgs/Flare-VM.png" alt="Flare-VM">
</p>

## Before Running the Malware

Before we run the malware for Dynamic Analysis, we want to ensure our environment is set up to capture any network traffic that may be occurring. Within Remnux, we want to ensure INetSim is running, as well as Wireshark, and on the Flare-VM host we want to ensure that our DNS is configured to be the Remnux host:

<p align="center">
  <img src="../imgs/dast_setup.png" alt="Setup">
</p>

Next, we can use information gathered from our Static Analysis to configure Wireshark to search for certain traffic:

<p align="center">
  <img src="../imgs/static_notes.png" alt="Notes">
</p>

We can have Wireshark search for HTTP requests with certain parts of the URL:

<p align="center">
  <img src="../imgs/wireshark_search.png" alt="Wireshark">
</p>

## Running Malware and Network Signatures

We can run the malware on our Flare-VM and monitor the network behavior on our Remnux machine in Wireshark:

<p align="center">
  <img src="../imgs/wireshark_output.png" alt="Wireshark Output">
</p>

<p align="center">
  <strong>FLOSS Output</strong><br>
  <img src="../imgs/FLOSS.png" alt="FLOSS Interface"><br>
  <img src="../imgs/FLOSS_Output.png" alt="FLOSS Extracted Strings">
</p>

## Host-Based Indicators

After analyzing what the malware could be doing on the network, it is imperative that we revert to a clean snapshot of our Flare-VM. Since we were focused on the network actions the malware was taking we didn't analyze what it was doing on the host. We can monitor host activity using a tool known as Procmon

## Procmon

<p align="center">
  <img src="../imgs/procmon.png" alt="Procmon">
</p>

We can run the malware and filter procmon to display actions taken by the malware:

<p align="center">
  <img src="../imgs/procmon_filter.png" alt="Filtering in Procmon">
</p>

Now when we run the malware we can see all the actions the malware takes:

<p align="center">
  <img src="../imgs/malware_in_procmon.png" alt="Malware Process">
</p>

From here we would want to monitor the actions the malware takes like making changes to the registry or creating files. We should also run the malware without INetSim running to see how the malware interacts with the host if it's not connected to the network:

<p align="center">
  <img src="../imgs/no_inetsim.png" alt="INetSim Disabled">
</p>

## TCPView

TCPView is a Windows program that will show you detailed listings of all TCP and UDP endpoints on your system, including the local and remote addresses and state of TCP connections. TCPView also reports the name of the process that owns the endpoint.

<p align="center">
  <img src="../imgs/tcpview.png" alt="TCPView">
</p>

This tool is useful because it can monitor TCP connections made locally that WireShark won't be able to capture:

<p align="center">
  <img src="../imgs/tcpview_analysis.png" alt="TCPView Analysis">
</p>
