# Wazuh-Security-Log-Investigation
A hands-on SOC investigation lab using Wazuh SIEM to analyze Windows security events, investigate failed login attempts, and identify suspicious authentication activity.

##Objective 
How to investigate windows authentication events
using <Wazuh SIEM>.

## lab Environment(operating systems):
1-Ubuntu:Wazuh Manager.
2-Windows: Wazuh Agent.


## Investigation Scenarios:

1-Failed logins(event ID 4625).
2- Successful logins(event ID 4624).
3-Suspicios authentication activity

## Investigation results.

>Scenario num1 (Failed logins)


first in the main interface click at the menu:

<img width="1216" height="686" alt="image" src="https://github.com/user-attachments/assets/a019cc26-156c-4dad-8f71-185a5d5c3d41" />

> click on "Treat intelligence" then "Threat Hunting"

<img width="1215" height="684" alt="image" src="https://github.com/user-attachments/assets/afa8248b-8ed9-4482-a3f6-8a51cbbae2a3" />

And here we are our Threat Hunting Dashboard :-

<img width="1212" height="683" alt="image" src="https://github.com/user-attachments/assets/dc08b96a-19c5-4326-b53c-bc4e8c79cbe9" />

In this scenario on your agent (WINDOWS OS) try failed logins (wrong passwords or username):-

Now in our manager device(UBUNTU OS):-

CLICK ON "Authentication failure" to filter failed logins.

<img width="1217" height="687" alt="image" src="https://github.com/user-attachments/assets/ae240af6-0fa9-40f6-8fa1-da4ebe6f45b3" />

<img width="1213" height="683" alt="image" src="https://github.com/user-attachments/assets/08488293-4d8f-4ce2-982e-3fabdeba2e45" />

Now to see these 7 events details CLICK ON "Events":-

<img width="1210" height="682" alt="image" src="https://github.com/user-attachments/assets/efd226ea-52ac-4ada-a879-4817f2148159" />


And here we are clearly 3 failed logins:-

<img width="1212" height="622" alt="image" src="https://github.com/user-attachments/assets/cacc3d51-f069-48bb-8b8a-238acf91c55a" />

to show the event details click on the icon left side of timestamp :-

<img width="1214" height="686" alt="image" src="https://github.com/user-attachments/assets/78cbb1ef-c3bc-4fb3-8557-d0f857035e96" />

Now we can see all the details about this event (agent ID, agent IP, agent NAME, etc...):-

<img width="1214" height="689" alt="image" src="https://github.com/user-attachments/assets/84b5b3c8-7272-4584-ae47-d79f817285b1" />

In these details we can import a lot of important informations:

1- data.win.eventdata.logontype --> 2 :
This type means that the interactive 
happened from device’s keyboard or screen directly.

2- data.win.evendata.status --> 0xc000006d :

(0xc000006d) this code means general failure
"unknown username or wrong passwords".

3- data.win.eventdata.subjectUserName ---> (THT$):
name the actual machine.

etc.......

## Action performed:-

1- failed logins attempts on windows agent.
2- good dealing with Threat Hunting dashboard interface.
3-Applied authentication failure filter to determine failed login events.

















