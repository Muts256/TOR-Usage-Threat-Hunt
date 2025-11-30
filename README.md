<h1>Hi, I'm Michael! <br/><a href="https://www.linkedin.com/in/michael-musoke/">Cybersecurity Professional</a></h1>

<h2>👨‍💻 TOR Usage Threat Hunt </h2>

- <b> Detection of Unauthorized TOR Browser Installation and Use</b>

    <h2> Scenario: </h2>
    Management suspects that some employees may be using TOR browsers to bypass network security controls because recent network logs show unusual encrypted traffic patterns and connections to known TOR entry nodes. Additionally, there have been anonymous reports of employees discussing ways to access restricted sites during work hours. The goal is to detect any TOR usage and analyze related security incidents to mitigate potential risks.

    <h2> Steps Taken: </h2>
       <b> 1. Collecting data</b> 
       
  2. Chronological Assessment.

  3. Report.
  
   <h3>Collection Data</h3>
    The first search was conducted in the DeviceFileEvents for any file containing the string “tor”. The results reveal that a labuser1 had something to do with the tor file.

    Query used to get this information: The query searches the DeviceFileEvents logs for the device name of interest (mm-mde-onboardi) for any file name that starts with tor and displays the desired columns. 

     ![image alt ](https://github.com/Muts256/TOR-Usage-Threat-Hunt/blob/0e8ca97df3e2e2a30b5688bb45bd49c542b7ae0e/T6.png)


  Further investigation of events on that particular day shows that the user had several files on the desktop. 

    ![image alt](https://github.com/Muts256/TOR-Usage-Threat-Hunt/blob/7fc5182039620638c371289e22208ea8a45584bb/T2.png)

    One file of interest had the name "tor-brower-windows". The logs showed that a command starting with this file name was executed to install the browser silently. Evidence of this is shown by querying the DeviceProcessEvent logs

    ![image alt](https://github.com/Muts256/TOR-Usage-Threat-Hunt/blob/c702c4978329397958fa87ec7caef715075bbbd8/T7.png)

    Other files of interest that were seen on the desktop included one named "shopping list" created and InitiatingProcessAccountName by the user.

    ![image alt](https://github.com/Muts256/TOR-Usage-Threat-Hunt/blob/b2d8a9f2c225bff8b2c430b57e5f12aab93ebef9/T4.png)

    Checking network activities to find if there was any connection made by the Tor browser that was installed by the user. Results obtained by querying the DeviceNetworkEvent for InitiatingFileName tor.exe and firefox.exe show that there were some connections made to a remote IP address on port 9001

    ![image alt](https://github.com/Muts256/TOR-Usage-Threat-Hunt/blob/fd8507dc02a772348dd4982132afbb947f2ea3fd/T10.png)


  
<h2> 🤳 Connect with me:</h2>

[<img align="left" alt="michael-musoke | LinkedIn" width="22px" src="https://cdn.jsdelivr.net/npm/simple-icons@v3/icons/linkedin.svg" />][linkedin]

[linkedin]: https://linkedin.com/in/michael-musoke
