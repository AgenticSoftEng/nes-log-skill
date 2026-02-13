# NES Log Skill

A Claude AI skill for extracting and analyzing diagnostic information from NES medical instrument logs.

## Overview

This skill provides structured data extraction from medical device logs, enabling quick retrieval of key diagnostic information including:
- **Barcodes** scanned by external scanner
- **Cartridge IDs** from internal barcode reader
- **Self-check results** and status
- **Run times** (start, finish, duration)

## Usage

Use the skill by requesting information from a log:

```
/nes-log-skill: get barcodes from <log>
/nes-log-skill: find cartridge ids in <log>
/nes-log-skill: list self check results
/nes-log-skill: get run time from <log>
```

### Natural Language Triggers

The skill responds to requests like:
- "read log"
- "read log barcode"
- "find cartridge id in log"
- "get self check from log"
- "list run times"

## What It Extracts

### Barcodes
External scanner readings from `on_barcodeScanResultInd` events
- Formats: CAR^, QCP^, QCN^, NST-MC-...
- Output: `<datetime>, Barcode: <value>, Line: <line-number>`

### Cartridge IDs
Internal barcode reader data, identified by `CAR^` prefix
- Format: `CAR^<model>^<serial>^<variant>^<date>^<checksum>`
- Example: `CAR^NES4251^A00011512^18206N^20240524^055F2376`
- Output: `<datetime>, <cartridge-id>, Line:<line-number>`

### Self-Check Results
Device self-test status events
- Handles multiple self-check events per log
- Output: `<datetime>, Self-check:<result>, Line:<line-number>`

### Run Times
Cartridge execution timing analysis
- Calculates duration from start to finish
- Output: `Start: <start-datetime>, Finish: <finish-datetime>, Total time: <duration>`

## Supported Devices

- Liaison NES

## Output Format

All extractions include:
- **DateTime**: Standardized format `yyyy-mm-dd hh:mm:ss`
- **Extracted Data**: The requested information
- **Line Number**: Source line in the log for reference

## Project Structure

```
.
├── README.md                              # This file
└── .claude/
    └── skills/
        └── nes-log-skill/
            ├── SKILL.md                   # Skill definition & routing
            ├── prompts/
            │   ├── get-barcode.md         # Barcode extraction
            │   ├── get-cartridge-id.md    # Cartridge ID extraction
            │   ├── get-self-check.md      # Self-check extraction
            │   └── get-run-time.md        # Run time calculation
            └── testfiles/                 # Sample log files
```

## How It Works

1. **Skill receives request** - User asks for specific information from a log
2. **Request routing** - SKILL.md determines which extraction prompt to use
3. **Specialized extraction** - Targeted prompt parses the log for requested data
4. **Structured output** - Results formatted with datetime, data, and line number

## Example

**User request:**
```
Get barcodes from this log:
[log content...]
```

**Skill processes and returns:**
```
2024-08-23 10:15:30, Barcode: CAR^NES4251^A00024618^V18629N^20240823^DF432046, Line: 42
2024-08-23 10:16:45, Barcode: QCP^NES4251^23086101^20240326, Line: 87
```
