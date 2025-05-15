# Dynamic Analysis

## Table of Contents
[Before Running the Malware](#before-running-the-malware) </br>
[Strings and FLOSS](#strings-and-floss) </br>
[PEView Analysis](#peview) </br>
[PEStudio](#pestudio)</br>

<p align="center">
  <img src="../imgs/Flare-VM.png" alt="Flare-VM">
</p>

## Before Running The Malware

The first thing an analyst should do when working with malware is to gather the binary's hash and compare it to a known hash. If there is no known hash, the analyst should still collect it:

<p align="center">
  <img src="../imgs/sha256_hash.png" alt="SHA-256 Hash">
</p>

<p align="center">
  <img src="../imgs/md5_hash.png" alt="MD5 Hash">
</p>

These hashes can be submitted to tools like VirusTotal to help identify the malware.

## Strings and FLOSS

Strings and FLOSS are tools that can be used to extract an array of characters (typically longer than 4 bytes) from a binary. FLOSS offers enhanced functionality by analyzing and compiling obfuscated strings, presenting them in the output.

<p align="center">
  <strong>Strings Output</strong><br>
  <img src="../imgs/strings.png" alt="Strings Output">
</p>

<p align="center">
  <strong>FLOSS Output</strong><br>
  <img src="../imgs/FLOSS.png" alt="FLOSS Interface">
  <br>
  <img src="../imgs/FLOSS_Output.png" alt="FLOSS Extracted Strings">
</p>

## PEView
Another tool that can assist in static analysis of malware is PEViewer. This tool will allow us to view the structure of the binary and the date it was compiled, along with other information. For example when we open the binary in PEView we can check the Magic Number to determine what kind of binary it is:</br>

<p align="center">
  <img src="../imgs/magic_byte.png" alt="Magic Byte">
</p>

We can also see the date the binary was compiled by going to IMAGE_NT_HEADER → IMAGE_FILE_HEADER and viewing the Time Date Stamp:</br>

<p align="center">
  <img src="../imgs/date_stamp.png" alt="Time Date Stamp">
</p></br>

We can then compare the Virtual Size and the Raw Data Size in the IMAGE_SECTION_HEADER .text section to determine if the malware is packed or unpacked. If the virtual size is significantly larger than the Raw Data Size than it is safe to assume that the malware is packed. We can convert the HEX Data Value to determine the size in bytes using the programmer calculator:

<p align="center">
  <img src="../imgs/virt_size.png" alt="Virtual Data Size">
</p></br>

Now looking at a packed Malware we notice certain differences like SECTION UPX0 which is an indicator that the binary was packed with the UPX packer. We can also see that in the IMPORT Address Table is significantly smaller than a normal IMPORT Address Table would be.

<p align="center">
  <img src="../imgs/packed_mal1.png" alt="Packed Malware">
</p></br>

We can also compare virtual size and raw data size and now we notice there is a big difference in size:

<p align="center">
  <img src="../imgs/packed_mal2.png" alt="Packed Malware">
</p></br>

We can also check what Windows APIs the binary may be leveraging under SECTION.rdata → IMPORT Address Table. We can also check if the APIs are commonly used by malicious binaries by checking MalAPI.io or reading the Windows Documentation:
<p align="center">
  <img src="../imgs/import_address.png" alt="IMPORT Address Table">
</p></br>

## PEStudio

Lastly we can automate a lot of these processes by using a tool known as PEStudio. PEStudio can generate file hashes, pull strings from binaries, view libraries and identify potentially malicious ones, etc.:

<p align="center">
  <img src="../imgs/pestudio.png" alt="PEStudio">
</p></br>
