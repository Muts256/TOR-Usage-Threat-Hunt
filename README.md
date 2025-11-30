<h1>Hi, I'm Michael! <br/><a href="https://www.linkedin.com/in/michael-musoke/">Cybersecurity Professional</a></h1>

<h2>👨‍💻 TOR Usage Threat Hunt </h2>

- <b> Detection of Unauthorized TOR Browser Installation and Use</b>

    <h2> Scenario: </h2>
    Management suspects that some employees may be using TOR browsers to bypass network security controls because recent network logs show unusual encrypted traffic patterns and connections to known TOR entry nodes. Additionally, there have been anonymous reports of employees discussing ways to access restricted sites during work hours. The goal is to detect any TOR usage and analyze related security incidents to mitigate potential risks.

    <h2> Steps Taken: </h2>

    The first search was conducted in the DeviceFileEvents for any file containing the string “tor”. The results reveal that a labuser1 had something to do with the tor file.

    Query used to get this information:

    DeviceFileEvents
    | where DeviceName == "mm-mde-onboardi"
    | where FileName startswith "tor"
    |project Timestamp, DeviceName, FileName, InitiatingProcessAccountName, InitiatingProcessFileName

<h2> 🤳 Connect with me:</h2>

[<img align="left" alt="michael-musoke | LinkedIn" width="22px" src="https://cdn.jsdelivr.net/npm/simple-icons@v3/icons/linkedin.svg" />][linkedin]

[linkedin]: https://linkedin.com/in/michael-musoke
