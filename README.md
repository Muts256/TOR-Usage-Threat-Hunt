<h1>Hi, I'm Michael! <br/><a href="https://www.linkedin.com/in/michael-musoke/">Cybersecurity Professional</a></h1>

<h2>👨‍💻 TOR Usage Threat Hunt </h2>

- <b> Detection of Unauthorized TOR Browser Installation and Use</b>

    <h2> Scenario: </h2>
    Management suspects that some employees may be using TOR browsers to bypass network security controls because recent network logs show unusual encrypted traffic patterns and connections to known TOR entry nodes. Additionally, there have been anonymous reports of employees discussing ways to access restricted sites during work hours. The goal is to detect any TOR usage and analyze related security incidents to mitigate potential risks.

    <h2> Steps Taken: </h2>
       <b> 1. Querying the Logs</b> 
       
  <b>2. Chronological Assessment.</b>

  <b>3. Summary Report.</b>
  
   <h2> 1. Querying the Logs</h2>
    The first search was conducted in the DeviceFileEvents for any file containing the string “tor”. The results reveal that a labuser1 had something to do with the tor file.

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

### 1
**Time:** 11:49:28 AM  
**Event Type:** Process Creation  
**Details:** A process that later created *Shopping List.txt* was started.  
**User:** labuser1  
**Notes:** This is not the file creation time — only the creation time of the process responsible for it.

### 2
**Time:** 12:18:27 PM  
**Event Type:** ProcessCreated  
**Details:** The Tor Browser installer `tor-browser-windows-x86_64-portable-15.0.2.exe /S` was executed silently.  
**User:** labuser1  
**Notes:** This marks the beginning of the Tor Browser installation.

### 3
**Time:** 12:19:14 PM  
**Event Type:** ProcessCreated  
**Details:** Firefox (Tor Browser interface) was launched.  
**User:** labuser1  
**Notes:** This begins the Tor Browser user interface startup.

### 4
**Time:** 12:19:14 PM  
**Event Type:** ProcessCreated  
**Details:** Another Firefox content process was spawned during startup.  
**User:** labuser1  
**Notes:** Tor Browser uses multiple Firefox subprocesses.

### 5
**Time:** 12:19:20 PM  
**Event Type:** ProcessCreated  
**Details:** A Firefox GPU process was started.  
**User:** labuser1  
**Notes:** Normal Firefox/Tor Browser rendering behavior.

### 6
**Time:** 12:19:21 PM  
**Event Type:** ProcessCreated  
**Details:** A Firefox content process (tab) was created.  
**User:** labuser1  
**Notes:** Part of multi-process browser architecture.

### 7
**Time:** 12:19:22 PM  
**Event Type:** ProcessCreated  
**Details:** The Tor routing service `tor.exe` was started using its full torrc configuration.  
**User:** labuser1  
**Notes:** This is where Tor begins building circuits.

### 8
**Time:** 12:19:22 PM  
**Event Type:** ProcessCreated  
**Details:** Additional Firefox content processes were started.  
**User:** labuser1  
**Notes:** Multiple tabs and processes are launched by design.

### 9
**Time:** 12:19:33 PM  
**Event Type:** Network Connection  
**Details:** `tor.exe` connected to IP 45.137.70.158 over port 9001.  
**User:** labuser1  
**Notes:** This is a Tor entry/guard node connection.

### 10
**Time:** 12:19:35 PM  
**Event Type:** Network Connection  
**Details:** `tor.exe` made another connection to IP 45.137.70.158 on port 9001.  
**User:** labuser1  
**Notes:** Continued Tor circuit establishment.

### 11
**Time:** 12:19:44 PM  
**Event Type:** ProcessCreated  
**Details:** A Firefox content process (tab 8) was created.  
**User:** labuser1  
**Notes:** Indicates active tab loading in Tor Browser.

### 12
**Time:** 12:19:51 PM  
**Event Type:** Network Connection  
**Details:** `firefox.exe` connected to 127.0.0.1 on port 9150.  
**User:** labuser1  
**Notes:** This is the SOCKS proxy allowing Firefox traffic to enter the Tor network.

### 13
**Time:** 12:28:57 PM  
**Event Type:** FileCreated  
**Details:** The file *Shopping List.txt* was created in `C:\Users\labuser1\Desktop`.  
**User:** labuser1  
**Notes:** This appears to be a user-created file and is not related to Tor Browser activity


<h2> 3. Summary Report.</h2>

  
<h2> 🤳 Connect with me:</h2>

[<img align="left" alt="michael-musoke | LinkedIn" width="22px" src="https://cdn.jsdelivr.net/npm/simple-icons@v3/icons/linkedin.svg" />][linkedin]

[linkedin]: https://linkedin.com/in/michael-musoke
