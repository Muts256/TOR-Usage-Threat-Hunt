<h1>Hi, I'm Michael! <br/><a href="https://www.linkedin.com/in/michael-musoke/">Cybersecurity Professional</a></h1>

<h2>👨‍💻 TOR Usage Threat Hunt </h2>

- <b> Detection of Unauthorised TOR Browser Installation and Use</b>

    <h2> Scenario: </h2>
    Management suspects that some employees may be using TOR browsers to bypass network security controls because recent network logs show unusual encrypted traffic patterns and connections to known TOR entry nodes. Additionally, there have been anonymous reports of employees discussing ways to access restricted sites during work hours. The goal is to detect any TOR usage and analyse related security incidents to mitigate potential risks.

    <h2> Steps Taken: </h2>
       <b> 1. Querying the Logs</b> 
       
  <b>2. Chronological Assessment.</b>

  <b>3. Summary Report.</b>

  <b>4.Response Taken</b>
  
   <h2> 1. Querying the Logs</h2>
    The first search was conducted in the DeviceFileEvents for any file containing the string “tor”. The results reveal that a user, labuser1, had something to do with the tor file.

    Query used to get this information: The query searches the DeviceFileEvents logs for the device name of interest (mm-mde-onboardi) for any file name that starts with tor and displays the desired columns. 

     ![image alt ](https://github.com/Muts256/TOR-Usage-Threat-Hunt/blob/0e8ca97df3e2e2a30b5688bb45bd49c542b7ae0e/T6.png)


  Further investigation of events on that particular day shows that the user had several files on the desktop. 

    ![image alt](https://github.com/Muts256/TOR-Usage-Threat-Hunt/blob/7fc5182039620638c371289e22208ea8a45584bb/T2.png)

    One file of interest had the name "tor-brower-windows". The logs showed that a command starting with this file name was executed to install the browser silently. Evidence of this is shown by querying the DeviceProcessEvent logs

    ![image alt](https://github.com/Muts256/TOR-Usage-Threat-Hunt/blob/c702c4978329397958fa87ec7caef715075bbbd8/T7.png)

    Other files of interest that were seen on the desktop included one named "shopping list" created and InitiatingProcessAccountName by the user.

    ![image alt](https://github.com/Muts256/TOR-Usage-Threat-Hunt/blob/b2d8a9f2c225bff8b2c430b57e5f12aab93ebef9/T4.png)

    Checking network activities to find if there was any connection made by the Tor browser that was installed by the user. Results obtained by querying the DeviceNetworkEvent logs for InitiatingFileName tor.exe and firefox.exe show that there were some connections made to a remote IP address on port 9001

    ![image alt](https://github.com/Muts256/TOR-Usage-Threat-Hunt/blob/fd8507dc02a772348dd4982132afbb947f2ea3fd/T10.png)


 <h2> 2. Chronological Assessment.</h2>

### 
**Time:** 11:49:28 AM  
**Event Type:** Process Creation  
**Details:** A process that later created *Shopping List.txt* was started.  
**User:** labuser1  
**Notes:** This is not the file creation time, only the creation time of the process responsible for it.

### 
**Time:** 12:18:27 PM  
**Event Type:** ProcessCreated  
**Details:** The Tor Browser installer `tor-browser-windows-x86_64-portable-15.0.2.exe /S` was executed silently.  
**User:** labuser1  
**Notes:** This marks the beginning of the Tor Browser installation.

### 
**Time:** 12:19:14 PM  
**Event Type:** ProcessCreated  
**Details:** Firefox (Tor Browser interface) was launched.  
**User:** labuser1  
**Notes:** This begins the Tor Browser user interface startup.

### 
**Time:** 12:19:14 PM  
**Event Type:** ProcessCreated  
**Details:** Another Firefox content process was spawned during startup.  
**User:** labuser1  
**Notes:** Tor Browser uses multiple Firefox subprocesses.

### 
**Time:** 12:19:20 PM  
**Event Type:** ProcessCreated  
**Details:** A Firefox GPU process was started.  
**User:** labuser1  
**Notes:** Normal Firefox/Tor Browser rendering behavior.

### 
**Time:** 12:19:21 PM  
**Event Type:** ProcessCreated  
**Details:** A Firefox content process (tab) was created.  
**User:** labuser1  
**Notes:** Part of multi-process browser architecture.

### 
**Time:** 12:19:22 PM  
**Event Type:** ProcessCreated  
**Details:** The Tor routing service `tor.exe` was started using its full torrc configuration.  
**User:** labuser1  
**Notes:** This is where Tor begins building circuits.

### 
**Time:** 12:19:22 PM  
**Event Type:** ProcessCreated  
**Details:** Additional Firefox content processes were started.  
**User:** labuser1  
**Notes:** Multiple tabs and processes are launched by design.

### 
**Time:** 12:19:33 PM  
**Event Type:** Network Connection  
**Details:** `tor.exe` connected to IP 45.137.70.158 over port 9001.  
**User:** labuser1  
**Notes:** This is a Tor entry/guard node connection.

### 
**Time:** 12:19:35 PM  
**Event Type:** Network Connection  
**Details:** `tor.exe` made another connection to IP 45.137.70.158 on port 9001.  
**User:** labuser1  
**Notes:** Continued Tor circuit establishment.

### 
**Time:** 12:19:44 PM  
**Event Type:** ProcessCreated  
**Details:** A Firefox content process (tab 8) was created.  
**User:** labuser1  
**Notes:** Indicates active tab loading in Tor Browser.

### 
**Time:** 12:19:51 PM  
**Event Type:** Network Connection  
**Details:** `firefox.exe` connected to 127.0.0.1 on port 9150.  
**User:** labuser1  
**Notes:** This is the SOCKS proxy allowing Firefox traffic to enter the Tor network.

### 
**Time:** 12:28:57 PM  
**Event Type:** FileCreated  
**Details:** The file *Shopping List.txt* was created in `C:\Users\labuser1\Desktop`.  
**User:** labuser1  
**Notes:** This appears to be a user-created file and is not related to Tor Browser activity


<h2> 3. Summary Report.</h2>

  This report summarises the user and system activity observed on the endpoint mm-mde-onboardi on 29 November 2025, focusing on the installation and operation of the Tor Browser and the subsequent creation of a user-generated text file.

1. Initial Process Activity
**At 11:49:28 AM:**, a process associated with labuser1 was started. Although this process did not immediately create any files, it was later identified as the parent process responsible for creating Shopping List.txt. This timestamp represents the process creation, not the file creation itself.

2. Tor Browser Installation and Launch
**Between 12:18 PM and 12:19 PM**, the Tor Browser portable installer was executed silently (/S flag silently), signalling the start of installation. Shortly afterwards, multiple Firefox-related processes were created, representing: At 12:19:22 PM, the tor.exe process began running using the system’s Tor configuration. This marks the point where the Tor routing service initialises and begins establishing encrypted circuits.

3. Tor Network Communications
**Network telemetry** shows Tor network activity beginning at 12:19:33 PM, with tor.exe connecting to IP address 45.137.70.158 on port 9001. A second connection to the same node was made shortly afterwards. These appear to be standard Tor entry/guard node connections.

4. File Creation Unrelated to Tor
**At 12:28:57 PM**, the file Shopping List.txt was created on the desktop by user labuser1. This action is not related to Tor Browser activity and appears to be a normal user-generated file.


<h2> 4.Responce Taken.</h2>

TOR usage was confirmed on endpoint mm.mde.onboardi. The device was isolated, and the user's direct manager was notified




<h2> Recommendations to Prevent Similar Activity </h2>

1. Enforce Application Control (High Priority)

    - Allow only trusted, signed applications.

    - Block portable executables launched from user folders (Desktop, Downloads).

    - Restrict execution in all user-writable directories.

2. Strengthen Software Installation Controls

    - Remove local administrator rights from standard users.

    - Require elevated approval and auditing for any software installation.

    - Deploy applications only through managed solutions (Intune, SCCM).

3. Block and Detect Tor at the Network Layer

    - Enable TLS inspection to identify Tor handshake behaviour.

    - Block Tor-related domains using DNS/web filtering.

    - Monitor outbound connections to known Tor ports (9001, 9030, 9050, 9150).

4. Improve Endpoint Detection & Monitoring

    - Configure custom detections for tor.exe or Firefox launched from Tor directories.

    - Monitor the execution of portable applications from uncommon locations.

5. Apply Web Filtering and Download Restrictions

    - Route all downloads through monitored, policy-enforced gateways.

    - Block categories such as “anonymisers,” “circumvention tools,” and “dark web tools.”

6. Strengthen User Awareness and Policy Enforcement

    - Train users on the risks of anonymity tools and unauthorised installations.

    - Update the Acceptable Use Policy to explicitly prohibit privacy software like Tor Browser.

7. Harden Local File System Permissions

    - Make Desktop and Downloads read-only for non-admin users.

    - Restrict write access to system directories to prevent abuse of portable software.

<h2> Lessons Learned </h2>

- KQL Proficiency: Using KQL to query logs.
- Investigative reasoning: What logs to query from the given clues.
- Event Correlation: Reconstruction Time frame of the events.
- Baseline behaviour: To make finding anomalies faster.
- Importance of user education to avoid risky behaviour.
- Necessity of custom detection rules to detect usual/undesirable processes.

<h2> 🤳 Connect with me:</h2>

[<img align="left" alt="michael-musoke | LinkedIn" width="22px" src="https://cdn.jsdelivr.net/npm/simple-icons@v3/icons/linkedin.svg" />][linkedin]

[linkedin]: https://linkedin.com/in/michael-musoke
