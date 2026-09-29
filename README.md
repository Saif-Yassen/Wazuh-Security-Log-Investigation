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
<img width="1214" height="684" alt="image" src="https://github.com/user-attachments/assets/5e91bbec-950f-4746-87d2-9307f9ccc9d7" />


In these details we can import a lot of important informations:

1- data.win.eventdata.logontype --> 2 :
This type means that the interactive 
happened from device’s keyboard or screen directly.

2- data.win.evendata.status --> 0xc000006d :

(0xc000006d) this code means general failure
"unknown username or wrong passwords".

3- data.win.eventdata.subjectUserName ---> (THT$):
name the actual machine.

4- "data.win.system.eventID" --->"4625".

ID number of Authentication failure of Windows logs.

## Action performed:-

1- failed logins attempts on windows agent.
2- good dealing with Threat Hunting dashboard interface.
3-Applied authentication failure filter to determine failed login events.

## Conclusion 

Successfully detected and identified failed windows logins 
using Wazuh SEIM. This scenario explained how to identify authentication 
failure.

Next step: identifying successful login events and correlate them with failed  logins to identify 
the potential of suspicious authentication activity.

## Scenario Two (Successful logins).

To start comeback to "Threat Hunting Dashboard" interface and apply
"Authentication success" filter


<img width="1212" height="688" alt="image" src="https://github.com/user-attachments/assets/78789837-496b-4e19-97b7-dda059c6519c" />


where is "Tht" machine???
the reason why agent "Tht" not existed that there is no filter dedicated 
to receive signals from Windows rule groups, all the filters designed to catch signals
from Linux/PAM rule groups.

So, the next step is creating a filter specialised for Windows:-

Go to "Threat Hunting" interface :

<img width="1211" height="681" alt="image" src="https://github.com/user-attachments/assets/d10b597e-9375-4e9e-99b3-6bbf20b03370" />

Click on "Add filter":

<img width="1216" height="684" alt="image" src="https://github.com/user-attachments/assets/2dcfed48-16d2-4f2d-82e9-852c2ae14c8b" />

1- In this field type "data.win.system.eventID".
-> When Wazuh receive Windows log it divide it into fields.
This field hold Windows event id number.

2- In Operator choose "is".
->  "is" in operators means that we want only this value,
in our case we want 4624 --->> which is the event ID.

3- choose "4624" in Value field.
 -> In Windows means that the account was successfully logged in. 
 

<img width="1207" height="495" alt="image" src="https://github.com/user-attachments/assets/3bc79947-da6f-41b8-8856-8ff6ee47ee28" />


Click on "Save"


<img width="1216" height="685" alt="image" src="https://github.com/user-attachments/assets/d17d1bfc-2a0b-429e-a2fe-5300c1f29631" />

Big question here!!!...

## Why it still ZEROO??

Reason:
Wazuh dashboard’s cards runs by Wazuh rule.groups and rule.level don't have Windows
event IDs. 
To show Windows logs Click on "Events" in Wazuh "Threating Events":


<img width="1212" height="688" alt="image" src="https://github.com/user-attachments/assets/93fdd54c-3e39-46c0-a82a-c7be85815b04" />


Click on the icon beside "timestamp":-

<img width="1211" height="686" alt="image" src="https://github.com/user-attachments/assets/500a181c-0764-4ff9-9dd9-9ae29752f185" />

<img width="1216" height="688" alt="image" src="https://github.com/user-attachments/assets/323d26ed-e298-47dd-b80b-d28bf93c254c" />

Scroll down to "data.win.system.eventID" showing up the ID number is "4624".

<img width="1216" height="684" alt="image" src="https://github.com/user-attachments/assets/c6241e00-581c-4b24-8696-a181c5ac3f4c" />

## Action performed

1.Generating successful logins on Windows agent.
2.Applying "Authentication success" filter in "Threating Hunting" dashboard 
and discovering issue with Windows agent.

3.Creating a custom filter in "data.win.system.eventID" with the operator "is"
and value "4624".
4.Explaining why dashboard cards still zero.
5. showing the windows events ID rule.group in Events interface.

## Conclusion 
Successfully finding Windows successful login events in Wazuh.
The dashboard cards didn't show Windows events. So, I used a custom filter and 
the Events interface showed them. This scenario showed us that Windows events must 
be searched by it own fields, not only by the built in cards.

Next step: correlate failed logins (4625) with successful logins (4624)
to detect suspicious authentication activity.


## Scenario Three (Investigate suspicious authentication)
-> In this scenario we want to simulate brute force attack potential.
To simulate it lock your Windows agent account and try failed logins 5 times
then do successful one. 

Go to Wazuh "Threating Hunting" dashboard Click on "Events":-

<img width="1210" height="686" alt="image" src="https://github.com/user-attachments/assets/06aaaef1-8174-4d2a-97dd-cddca5d3b40a" />

Click on "Add filter":-

<img width="1213" height="357" alt="image" src="https://github.com/user-attachments/assets/6ad75bd6-44d4-46b6-ab91-06283a1a65c3" />

In "Field" search bar type "data.win.system.eventID". 
In "Operator" choose "is one of".
In Values type 4625 and press Enter then type 4624 and press Enter.

<img width="1209" height="387" alt="image" src="https://github.com/user-attachments/assets/5b65a208-0cbf-460f-a3d4-0007a0fc8811" />

Then Click Save.










