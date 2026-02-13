# Purpose
Find and retreive information about the cartridge run in the log

## Variables
DATE_TIME_FORMAT: yyyy-mm-dd hh:mm:ss

## Instructions
1. Read the log 
2. Find the time when the run started
3. Find the time when the run completed
4. Calculate the total run time of the cartridge
5. Return the result using Output-format


## Output-format
    Start: <run-started-date-time: DATE_TIME_FORMAT>, Finish: <run-started-date-time: DATE_TIME_FORMAT>, Total time: <total-run-time>

## Pattern Examples

### Run Start Pattern
Look for `actionOnRunStatusChanged` messages where `hw_running` transitions from 0 to 1:
- "actionOnRunStatusChanged - run enabled (previous state): 0, hw fault: 0, hw running: 1, ... run status: 2"
- Example: Feb 26 10:29:37.891 userinterface.610350 8344 actionOnRunStatusChanged - run enabled (previous state): 0, hw fault: 0, hw running: 1, temp invalid: 0, pressure invalid: 0, ...

### Run Finish Pattern
Look for either:
1. `actionOnRunStatusChanged` messages where `hw_running` transitions from 1 to 0:
   - "actionOnRunStatusChanged - run enabled (previous state): 0, hw fault: 0, hw running: 0, ... run status: 2"
   - Example: Feb 26 10:48:01.224 userinterface.610350 8344 actionOnRunStatusChanged - run enabled (previous state): 0, hw fault: 0, hw running: 0, ...

2. Result completion messages:
   - "[AE_RESULT_RECORD]Test result sent successfully"
   - Example: Feb 26 10:48:01.776 assayengine.610318 3223 [AE_RESULT_RECORD]Test result sent successfully (db id=52)
   - "[AE_SCRIPT_PARSER]Script Process Line ... completed PASS"
   - Example: Feb 26 10:47:43.338 assayengine.610318 3194 [AE_SCRIPT_PARSER]Script Process Line 212 : #CK>PCR completed PASS
