🔓 WIFI Password Cracking using aircrack-ng:

**Step1:** Check the wlan0 mode. It shows the mode(manage).

**iwconfig:** This command lists all wireless interfaces and their current modes. Look for interfaces like wlan0 to identify your wireless adapter. 

<img width="1677" height="943" alt="Picture1" src="https://github.com/user-attachments/assets/83e69783-6b83-4bab-b40a-1cf71ca64130" />

**Step2:** Change the manage of wlan0mode to monitor mode. We are using a tool (airmon –ng).

**airmon-ng –help:** airmon-ng is a script that simplifies enabling and disabling monitor mode
on wireless interfaces. It also helps detect and manage processes that may
interfere with packet capture and injection.

**Sytnax:** Usage: airmon-ng <start|stop|check> <interface> [channel or frequency]

**Options:**
-	Start:Start monitor mode on an interface
-	Stop:Stop monitor mode on an interface
-	Check: Check for processes that might interfere with monitor mode
<img width="1627" height="915" alt="Picture1" src="https://github.com/user-attachments/assets/49a29d18-f24a-443c-b844-de59603f1f3a" />

**Step3:** Before enabling monitor mode use the following command.

**airmon-ng check kill:** This command detects and kills background processes that can interfere with WiFi monitor mode and packet injection.

<img width="1627" height="915" alt="Picture1" src="https://github.com/user-attachments/assets/0f867ced-46ad-4cf8-9af7-7fd820e519bb" />

**Step4:** Enable /Starting monitor mode for wlan0.

**airmon-ng start wlan0:** This command is used to start monitor mode on your Wi-Fi adapter (wlan0) using the airmon-ng tool. We again use iwconfig command to check if it is changed to monitor mode.

<img width="1557" height="876" alt="Picture1" src="https://github.com/user-attachments/assets/b2d1cde1-4acb-40ca-8cbf-9e66fc81210d" />
<img width="1540" height="866" alt="Picture1" src="https://github.com/user-attachments/assets/d7683e5b-0c90-4c85-9b61-623ff741cea5" />

**Step5:** Check which access points are being detected. After detecting have to check their BSSID.

**airodump-ng wlan0mon:** This command is one of the most important steps in WiFi pentesting, used to scan nearby WiFi networks and show all the access points (APs) and connected devices. Note the BSSID and channel (CH) of the target WiFi network.
![Picture7](https://github.com/user-attachments/assets/98037b5e-20e7-4654-a5ce-5e13ad197b58)

**Step6:** Target a specific network. Monitor a particular access point.

**airodump-ng wlan0mon -c <CH> --bssid<Target-Mac>:** This command is used in WiFi pentesting to focus only on one target WiFi access point (AP) instead of scanning all the networks. This is often done before trying to capture the WPA/WPA2 handshake.

<img width="1583" height="890" alt="Picture8" src="https://github.com/user-attachments/assets/0c72aec2-39cd-4112-8e89-07476b25222a" />

**Step7:** Perform wi-fi deauthentication attack, for this disconnect target device after reconnecting it handshake will be captured.

**airodump-ng wlan0mon -c <CH> --bssid<Target-Mac> -w target-handshake:** Lock onto the target WiFi using its channel and BSSID it can capture traffic. Then we wait for a device to connect or reconnect to that WiFi. When it does, the WPA/WPA2 handshake is captured, which is needed later to crack the WiFi password.

<img width="1596" height="898" alt="Picture11" src="https://github.com/user-attachments/assets/ca2eb11b-643a-436b-a0c5-1e7f1e3972c2" />


**Step8:** Start deauthentication attack. Firstly check all the available option use for deauthentication attack. Deauthenticate a client to capture handshake.

**aireplay-ng –help:** This command displays all the available options and usage examples for the aireplay-ng tool which is used to inject packets into a network, including performing deauthentication attacks to disconnect clients.

**aireplay-ng --deauth 10 -a [Target_BSSID] wlan0:** This forces the client to disconnect and reconnect, during which the handshake can be captured.

<img width="1591" height="818" alt="Picture10" src="https://github.com/user-attachments/assets/ce6964ed-5abc-4cda-8dd9-a21b65140d8a" />

## **Wordlist:**
<img width="1608" height="905" alt="Picture11" src="https://github.com/user-attachments/assets/fb77ec51-ccee-4ae2-806a-d96dc639f876" />

**Step9:** Key is found.

**aircrack –ng –w wordlist.txt handshake.cap:** It is used to crack Wi-Fi passwords captured during a handshake between a device and a wireless access point.

<img width="1568" height="882" alt="Picture11" src="https://github.com/user-attachments/assets/85ec2b74-1aa4-4eed-8034-ec04490d9e09" />

<img width="1547" height="781" alt="Picture14" src="https://github.com/user-attachments/assets/217d4f99-dd6b-4b30-9f72-d47ce254c6bd" />

**Step10:** Stop the monitor mode. Using iwconfig we can check the mode.

**airmon-ng stop wlan0mon:** It is used to stop monitor mode on your wireless interface.

<img width="1570" height="884" alt="Picture14" src="https://github.com/user-attachments/assets/37fcbbaf-5c0b-41ce-a48e-daa4de998c03" />

**Step11:** Start network manager it  controls wifi-adapter.

**service network-manager start:** Start or restart your system's network management service, so that it can automatically handle your Wi-Fi, Ethernet, VPN, and other network connections.

<img width="1604" height="903" alt="Picture14" src="https://github.com/user-attachments/assets/b8c6a026-f20f-4bbb-a425-71cafde618d0" />

**Step12:** Check if the entered password is working or not.

ping google.com: It is used to check if your internet connection is working and to test network reachability.

<img width="1601" height="901" alt="Picture1" src="https://github.com/user-attachments/assets/370ede24-5558-412a-a353-ce0673d3a6ff" />

![Picture2](https://github.com/user-attachments/assets/09715684-ad9e-44d1-88d6-d20588f9ea98)


