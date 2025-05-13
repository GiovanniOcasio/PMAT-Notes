# Static Analysis

## Table of Contents
[Hashing Malware](#hashing-malware) </br>
[Strings and FLOSS](#strings-and-floss) </br>
[PEViewer Analysis](#peviewer) </br>

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

## PEViewer
