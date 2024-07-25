# Configure Security Operations using Microsoft Sentinel

## Objective

The "Configure SIEM for Security Operations Using Microsoft Sentinel" lab focuses on equipping me with the practical skills needed to configure and manage a Security Information and Event Management (SIEM) system using Microsoft Sentinel. This lab covers key aspects of security operations, including the setup, configuration, and optimization of Sentinel for monitoring and responding to security threats. I will also learn how to create and manage workbooks, analytics rules, incidents, and automation playbooks, enabling them to effectively leverage Sentinel for enhancing organizational security posture.

### Skills Learned

- Azure administration
- Configuring Microsoft Sentinel for security monitoring
- Creating and managing workbooks for data visualization
- Setting up and tuning analytics rules for threat detection
- Designing and implementing automation playbooks for efficient operations

### Tools Used

- Azure
- Microsoft Sentinel
- Log Analytics
- IAM Access Control

### Prerequisites 
Azure Subscription

## Steps
Following Microsoft policy I cannot share the detailed steps and screenshots of what I did to complete the lab. But all updated steps to complete this lab can be found on [MS Learn - Configure SIEM security operations using Microsoft Sentinel](https://learn.microsoft.com/en-us/credentials/applied-skills/configure-siem-security-operations-using-microsoft-sentinel/). After taking this lab and completing the assesment I earned the [applied skills certification](https://learn.microsoft.com/api/credentials/share/en-gb/JaedynDamms-1608/E40E566641FAFAA9?sharingId=592CAF5B8FD33BDB).

### Step 1 - [Configure SIEM operations using Microsoft Sentinel](https://learn.microsoft.com/en-gb/training/modules/configure-siem-security-operations-using-microsoft-sentinel/2-exercise)
![image](https://github.com/user-attachments/assets/92ebee21-7a5f-44ce-9abb-58cf16724255)

1. Create Azure Log Analytics workspace
2. Deploy Microsoft Sentinel to the Log Analytics workspace
3. Assign Microsoft Sentinel role to a user via IAM Access Control
4. Configure data retention period (180 days) for Log Analytics workspace


### Step 2 - [Install Microsoft Sentinel Content Hub solutions and data connectors](https://learn.microsoft.com/en-gb/training/modules/configure-siem-security-operations-using-microsoft-sentinel/3-exercise)
![image](https://github.com/user-attachments/assets/6a4b76a3-861e-4c4a-84ef-704493410118)

1. Deploy Microsoft Sentinel Content Hub solution (Windows Security Events)
2. Setup data connector for Azure Activity
3. Setup Defender for Cloud data connector
4. Create anaytics rule based on the _Suspicious number of resource creation or deployment activities template_ using the below query scheduling

| **Setting** | **Value** |
|-------------|-----------|
| Run query every | 1 Hours |
| Lookup data from the last | 1 Hours |

5. Check that the Azure Activity workbook is available in My workbooks


### Step 3 - [Configure a data connector Data Collection Rule](https://learn.microsoft.com/en-gb/training/modules/configure-siem-security-operations-using-microsoft-sentinel/4-exercise)
![image](https://github.com/user-attachments/assets/3f57f087-5e95-4b8d-98fd-82ab7afee1a0)

1. Configure data collection rules for Windows Security Events
2. Create near real time query detection using the below KQL query

```
SecurityEvent 
| where EventID == 4732
| where TargetAccount == "Builtin\\Administrators"
```

3. Configure an automation in Microsoft Sentinel to assign the owner of the incident to a user



### Step 4 - [Perform a simulated attack to validate the Analytic and Automation rules](https://learn.microsoft.com/en-gb/training/modules/configure-siem-security-operations-using-microsoft-sentinel/5-exercise)
![image](https://github.com/user-attachments/assets/0fa01547-5abf-4c09-b2d0-484e1f4d5a2b)

1. Spin up a Windows VM in Azure
2. Select the Windows VVM and run the below PowerShell script to perform a simulated Privilege Escalation attack

```
 net user theusernametoadd /add
 net user theusernametoadd ThePassword1!
 net localgroup administrators theusernametoadd /add
```
3. Verify that an incident has been created in Microsoft Sentinel

