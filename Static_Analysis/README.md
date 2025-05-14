# Static Analysis

## Table of Contents
[Hashing Malware](#hashing-malware) </br>
[Strings and FLOSS](#strings-and-floss) </br>
[PEView Analysis](#peview) </br>

<p align="center">
  <img src="../imgs/Flare-VM.png" alt="Flare-VM">
</p>

## Hashing Malware

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

<p align="center">
  <img src="../imgs/raw_size.png" alt="Raw Data Size">
</p></br>
