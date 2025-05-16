# Dynamic Analysis

## Table of Contents
- [Before Running the Malware](#before-running-the-malware)  
- [Running Malware and Network Signatures](#running-malware-and-network-signatures)  
- [Host-Based Indicators](#host-based-indicators)  
- [PEStudio](#pestudio)

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

Another tool that can assist in static analysis of malware is PEViewer. This tool allows us to view the structure of the binary, the date it was compiled, and other information. For example, when we open the binary in PEView, we can check the Magic Number to determine what kind of binary it is:

<p align="center">
  <img src="../imgs/magic_byte.png" alt="Magic Byte">
</p>

We can also see the date the binary was compiled by going to `IMAGE_NT_HEADER → IMAGE_FILE_HEADER` and viewing the Time Date Stamp:

<p align="center">
  <img src="../imgs/date_stamp.png" alt="Time Date Stamp">
</p>

We can then compare the Virtual Size and the Raw Data Size in the `IMAGE_SECTION_HEADER .text` section to determine if the malware is packed or unpacked. If the virtual size is significantly larger than the Raw Data Size, it is safe to assume that the malware is packed. We can convert the hex data value to determine the size in bytes using the programmer calculator:

<p align="center">
  <img src="../imgs/virt_size.png" alt="Virtual Data Size">
</p>

Now, looking at a packed malware sample, we notice certain differences like `SECTION UPX0`, which is an indicator that the binary was packed with the UPX packer. We can also see that the IMPORT Address Table is significantly smaller than a normal one would be:

<p align="center">
  <img src="../imgs/packed_mal1.png" alt="Packed Malware">
</p>

We can also compare virtual size and raw data size and now notice there is a big difference in size:

<p align="center">
  <img src="../imgs/packed_mal2.png" alt="Packed Malware">
</p>

We can also check what Windows APIs the binary may be leveraging under `SECTION.rdata → IMPORT Address Table`. Additionally, we can check if the APIs are commonly used by malicious binaries by checking [MalAPI.io](https://malapi.io) or reading the Windows Documentation:

<p align="center">
  <img src="../imgs/import_address.png" alt="IMPORT Address Table">
</p>

## PEStudio

Lastly, we can automate many of these processes using a tool known as PEStudio. PEStudio can generate file hashes, extract strings from binaries, view libraries, and identify potentially malicious ones:

<p align="center">
  <img src="../imgs/pestudio.png" alt="PEStudio">
</p>
