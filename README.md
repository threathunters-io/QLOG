# What is Qlog
QLOG provides enriched Event Logging for security related events on Windows based systems.
It is under heavy development and currently in alpha state. QLOG doesn’t use API hooks and it doesn’t 
require a driver to be installed on the target system, QLOG only uses ETW to retrieve its telemetry. 
Currently QLOG supports “process create” events only, but other enriched events will follow soon. 
QLOG runs as a Windows Services, but can also run in console mode, if you want to stream the enriched events to console directly.

# How does it work
QLOG reads from ETW, enriches events and writes enriched events to Event Channel “QLOG”. 
It creates and uses a new event source named “QMonitor” to write to Windows Eventlog.

Here is sequence of event processing:
* Create ETW session & Subscribe to relevant kernel and userland ETW providers
* Read Events from ETW providers
* Enrich Events
* Write enriched events to eventlog channel QLOG

# Development & License
QLOG is being developed by threathunters.io community and will be open sourced once it reaches production grade maturity.

# Why we created QLOG?
Sysmon does a great job, but we wanted to create a tool which is open source and doesn't require drivers to be installed on target systems. 
Also, Sysmon is NOT SUPPORTED by Microsoft at all. So, if you run into problems in prod, you're at your own. Sure, QLOG doesn't have support either, 
but it will be open sourced so we can fix issues with the power of the security community and develop new features based on the requirements of the community.

# Usage & install
QLOG requires .NET Framework >=4.7.2 to be installed.

To run in interactive console mode, just run
```
qlog.exe
```
To install / deinstall as Windows service, run:
```
#install service
qlog.exe -i 

#deinstall service
qlog.exe -u 
```


# Do you want to contribute?
Please see https://threathunters.io/ on how to join threathunters.io community.

# Example output of enriched PROCESS CREATE events
```
{
  "EventGuid": "68795fe8-67e7-410b-a5c0-8364746d7ffe",
  "StartTime": "2021-07-11T11:06:56.9621746+02:00",
  "QEventID": 100,
  "QType": "Process Create",
  "Username": "TESTOS\\TESTUSER",
  "Imagefilename": "TEAMS.EXE",
  "KernelImagefilename": "TEAMS.EXE",
  "OriginalFilename": "TEAMS.EXE",
  "Fullpath": "C:\\Users\\TESTUSER\\AppData\\Local\\Microsoft\\Teams\\current\\Teams.exe",
  "PID": 21740,
  "Commandline": "\"C:\\Users\\TESTUSER\\AppData\\Local\\Microsoft\\Teams\\current\\Teams.exe\" --type=renderer --autoplay-policy=no-user-gesture-required --disable-background-timer-throttling --field-trial-handle=1668,499009601563875864,12511830007210419647,131072 --enable-features=WebComponentsV0Enabled --disable-features=CookiesWithoutSameSiteMustBeSecure,SameSiteByDefaultCookies,SpareRendererForSitePerProcess --lang=de --enable-wer --ms-teams-less-cors=522133263 --app-user-model-id=com.squirrel.Teams.Teams --app-path=\"C:\\Users\\jocke",
  "Modulecount": 41,
  "TTPHash": "42AC63285408F5FD91668B16F8E9157FD97046AB63E84117A14E31A188DDC62F",
  "Imphash": "F14F00FA1D4C82B933279C1A28957252",
  "sha256": "155625190ECAA90E596CB258A07382184DB738F6EDB626FEE4B9652FA4EC1CC2",
  "md5": "9453BC2A9CC489505320312F4E6EC21E",
  "sha1": "7219CB54AC535BA55BC1B202335A6291FDC2D76E",
  "ProcessIntegrityLevel": "None",
  "isOndisk": true,
  "isRunning": true,
  "Signed": "Signature valid",
  "AuthenticodeHash": "B8AD58EE5C35B3F80C026A318EEA34BABF6609C077CB3D45AEE69BF5C9CF8E11",
  "Signatures": [
    {
      "Subject": "CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US",
      "Issuer": "CN=Microsoft Code Signing PCA 2010, O=Microsoft Corporation, L=Redmond, S=Washington, C=US",
      "NotBefore": "15.12.2020 22:24:20",
      "NotAfter": "02.12.2021 22:24:20",
      "DigestAlgorithmName": "SHA256",
      "Thumbprint": "E8C15B4C98AD91E051EE5AF5F524A8729050B2A2",
      "TimestampSignatures": [
        {
          "Subject": "CN=Microsoft Time-Stamp Service, OU=Thales TSS ESN:3BBD-E338-E9A1, OU=Microsoft America Operations, O=Microsoft Corporation, L=Redmond, S=Washington, C=US",
          "Issuer": "CN=Microsoft Time-Stamp PCA 2010, O=Microsoft Corporation, L=Redmond, S=Washington, C=US",
          "NotBefore": "12.11.2020 19:26:02",
          "NotAfter": "11.02.2022 19:26:02",
          "DigestAlgorithmName": "SHA256",
          "Thumbprint": "E8220CE2AAD2073A9C8CD78752775E29782AABE8",
          "Timestamp": "15.06.2021 00:39:50 +02:00"
        }
      ]
    },
    {
      "Subject": "CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US",
      "Issuer": "CN=Microsoft Code Signing PCA 2011, O=Microsoft Corporation, L=Redmond, S=Washington, C=US",
      "NotBefore": "15.12.2020 22:31:47",
      "NotAfter": "02.12.2021 22:31:47",
      "DigestAlgorithmName": "SHA256",
      "Thumbprint": "C774204049D25D30AF9AC2F116B3C1FB88EE00A4",
      "TimestampSignatures": [
        {
          "Subject": "CN=Microsoft Time-Stamp Service, OU=Thales TSS ESN:F87A-E374-D7B9, OU=Microsoft Operations Puerto Rico, O=Microsoft Corporation, L=Redmond, S=Washington, C=US",
          "Issuer": "CN=Microsoft Time-Stamp PCA 2010, O=Microsoft Corporation, L=Redmond, S=Washington, C=US",
          "NotBefore": "14.01.2021 20:02:23",
          "NotAfter": "11.04.2022 21:02:23",
          "DigestAlgorithmName": "SHA256",
          "Thumbprint": "ED2C601EDD49DD2A934D2AB32DCACC19940161EF",
          "Timestamp": "15.06.2021 00:39:53 +02:00"
        }
      ]
    }
  ],
  "ParentProcess": {
    "EventGuid": null,
    "StartTime": "2021-07-11T09:54:28.9558001+02:00",
    "QEventID": 100,
    "QType": "Process Create",
    "Username": "TEST-OS\\TESTUSER",
    "Imagefilename": "",
    "KernelImagefilename": "",
    "OriginalFilename": "TEAMS.EXE",
    "Fullpath": "C:\\Users\\TESTUSER\\AppData\\Local\\Microsoft\\Teams\\current\\Teams.exe",
    "PID": 16232,
    "Commandline": "C:\\Users\\TESTUSER\\AppData\\Local\\Microsoft\\Teams\\current\\Teams.exe ",
    "Modulecount": 162,
    "TTPHash": "",
    "Imphash": "F14F00FA1D4C82B933279C1A28957252",
    "sha256": "155625190ECAA90E596CB258A07382184DB738F6EDB626FEE4B9652FA4EC1CC2",
    "md5": "9453BC2A9CC489505320312F4E6EC21E",
    "sha1": "7219CB54AC535BA55BC1B202335A6291FDC2D76E",
    "ProcessIntegrityLevel": "Medium",
    "isOndisk": true,
    "isRunning": true,
    "Signed": "Signature valid",
    "AuthenticodeHash": "B8AD58EE5C35B3F80C026A318EEA34BABF6609C077CB3D45AEE69BF5C9CF8E11",
    "Signatures": [
      {
        "Subject": "CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US",
        "Issuer": "CN=Microsoft Code Signing PCA 2010, O=Microsoft Corporation, L=Redmond, S=Washington, C=US",
        "NotBefore": "15.12.2020 22:24:20",
        "NotAfter": "02.12.2021 22:24:20",
        "DigestAlgorithmName": "SHA256",
        "Thumbprint": "E8C15B4C98AD91E051EE5AF5F524A8729050B2A2",
        "TimestampSignatures": [
          {
            "Subject": "CN=Microsoft Time-Stamp Service, OU=Thales TSS ESN:3BBD-E338-E9A1, OU=Microsoft America Operations, O=Microsoft Corporation, L=Redmond, S=Washington, C=US",
            "Issuer": "CN=Microsoft Time-Stamp PCA 2010, O=Microsoft Corporation, L=Redmond, S=Washington, C=US",
            "NotBefore": "12.11.2020 19:26:02",
            "NotAfter": "11.02.2022 19:26:02",
            "DigestAlgorithmName": "SHA256",
            "Thumbprint": "E8220CE2AAD2073A9C8CD78752775E29782AABE8",
            "Timestamp": "15.06.2021 00:39:50 +02:00"
          }
        ]
      },
      {
        "Subject": "CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US",
        "Issuer": "CN=Microsoft Code Signing PCA 2011, O=Microsoft Corporation, L=Redmond, S=Washington, C=US",
        "NotBefore": "15.12.2020 22:31:47",
        "NotAfter": "02.12.2021 22:31:47",
        "DigestAlgorithmName": "SHA256",
        "Thumbprint": "C774204049D25D30AF9AC2F116B3C1FB88EE00A4",
        "TimestampSignatures": [
          {
            "Subject": "CN=Microsoft Time-Stamp Service, OU=Thales TSS ESN:F87A-E374-D7B9, OU=Microsoft Operations Puerto Rico, O=Microsoft Corporation, L=Redmond, S=Washington, C=US",
            "Issuer": "CN=Microsoft Time-Stamp PCA 2010, O=Microsoft Corporation, L=Redmond, S=Washington, C=US",
            "NotBefore": "14.01.2021 20:02:23",
            "NotAfter": "11.04.2022 21:02:23",
            "DigestAlgorithmName": "SHA256",
            "Thumbprint": "ED2C601EDD49DD2A934D2AB32DCACC19940161EF",
            "Timestamp": "15.06.2021 00:39:53 +02:00"
          }
        ]
      }
    ],
    "ParentProcess": null
  }
}
```
