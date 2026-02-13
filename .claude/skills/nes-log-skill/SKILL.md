---
name: nes-log-skill 
description: Examine the log and retreive the information requested by the user. Use this when the user requests 'read log' or 'read log <command>' or 'find <command> in log' or 'get <command> from log' 
---

# Purpose
Find and retreive information requested by the user in the log provided 

## Instructions
- Read the log
- Based on the users request follow the 'Cookbook' to retreive the information the user asked for
- Return ONLY the requested data, as specified in the 'Cookbook'

## Workflow
1. Understand the users request
2. Follow the 'Cookbook' to determine what information to retrieve


## Cookbook

### Get barcode
IF: The user requests to retreive the barcodes read by the instrument
THEN: Read and execute @.claude/skills/nes-log-skill/prompts/get-barcode.md
EXAMPLES:
    - "get barcodes from <log>"
    - "find barcodes"
    - "list barcodes"  


### Get cartridge id
IF: The user requests to retrieve the cartridge IDs recorded by the instrument
THEN: Read and execute @.claude/skills/nes-log-skill/prompts/get-cartridge-id.md
EXAMPLES:
    - "get cartridge ids from <log>"
    - "find cartridge id"
    - "list cartridge ids"  


### Get self check
IF: The user requests to retrieve self check events or details from the log
THEN: Read and execute @.claude/skills/nes-log-skill/prompts/get-self-check.md
EXAMPLES:
    - "get self check from <log>"
    - "find self checks"
    - "list self check results"  


### Get run time
IF: The user requests to retrieve the run times recorded by the instrument
THEN: Read and execute @.claude/skills/nes-log-skill/prompts/get-run-time.md
EXAMPLES:
    - "get run time from <log>"
    - "find run times"
    - "list run times"  








