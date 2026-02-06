# elevate_2025

---
## Purpose
This repository contains the code and configurations used for Elevate 2025. It covers detection-as-code, threat intelligence, and MCP set up.

- all MCP servers were cloned and treated as standalone folders within the repo for simplicity
  - ai-runbooks-elevate25 are cloned as of 5 Jan 2026
    - ai-runbooks-elevate25 was cloned from https://github.com/dandye/ai-runbooks
  - mcp-security-elevate25 updated on 5 Jan 2026
    - mcp-security-elevate25 was clone from https://github.com/google/mcp-security
  - opencti-mcp and github-mcp-server are cloned as of 28 May 2025 to keep the information frozen for simplicity sake
    - opencti-mcp was cloned from https://github.com/Spathodea-Network/opencti-mcp
    - github-mcp-server was cloned from https://github.com/github/github-mcp-server
  - virustotal-mcp-server was purpose-built to create Livehunt Rules and create IOC Collections. They currently append the "-elevate2025" for tracking purpose

Most of the folders will have it's own readme / instruction guide, taken from the original repository. 

## General Pre-requisities
1. Visual Studio Code installed
2. UV installed 
3. Cline installed
4. Python 3.11 or greater
5. Credentials / API tokens for the integrations (SecOps, Google Threat Intelligence, Github, etc)

## Quick Start
1. Clone this repository
    - This will also include Github Actions for the DaC portion
2. Update your cline settings. look at the example_cline_mcp_settings.json can be found 

## What does the future hold aka going down the rabbit hold
- integrate AIP? 
- include more actionable content - leverage secops-soar to push indicators, contain devices, build more complex hunting rules
- more malware analysis with ghidra? 