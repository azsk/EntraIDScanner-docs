## Addressing control failures

## Contents
- [Understanding scan logs and CSV report](README.md#Understanding-scan-logs-and-CSV-report)
----------------------------------------------

## Understanding scan logs and CSV report

Each AAD scan cmdlet writes output to a folder whose location is determined as below:
- AzSK.AAD-Root-Output-Folder = %LocalAppData%\Microsoft\AzSK.AADLogs  
	```
	E.g., "C:\Users\userName\AppData\Local\Microsoft\AzSK.AADLogs"
	```
- Sub-Folder = Sub_\<Subscription Name>\\\<Timestamp>_\<CommandAbbreviation>  
	```
	E.g., "Org_[yourOrganizationName]\20201120_140515_gads"  
	```	
Thus, the full path to an output folder might look like:  
```
E.g., "C:\Users\userName\AppData\Local\Microsoft\AzSK.AADLogs\Org_[yourOrganizationName]\20201120_140515_gads\
```


The contents of the output folder are organized as under:  

- *\SecurityReport-\<timestamp>.csv*- This is the summary CSV file listing all applicable controls and their evaluation status. 

- *\Etc*  
	- *\PowerShellOutput.log* - This is the raw PS console output captured in a file.  
	- *\EnvironmentDetails.log* - This is the log file containing environment data of current PowerShell session.  
	- *\README.txt* - This README file describes how to interpret the different files created when AzSK cmdlets are executed 

You can use these outputs as follows - 
1. The SecurityReport.CSV file provides a quick glimpse of the control results. Investigate those that say 'Verify' or 'Failed'.  
2. For 'Failed' or 'Verify' controls, look in the LOG files (search for 'failed' or by control-id). Understand what caused the control to fail.
3. For some controls, you can also use the 'Recommendation' field in the control output to get the PS command you may need to use.
4. Rerun the cmdlet and verify that the controls you tried to fix are passing now.

[Back to top…](README.md#contents)


