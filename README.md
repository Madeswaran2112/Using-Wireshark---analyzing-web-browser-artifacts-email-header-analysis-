# Using-Wireshark---analyzing-web-browser-artifacts-email-header-analysis
## AIM:
To use Wireshark to analyze web browser activities and inspect email headers from captured network traffic.
## Architecture Diagram:
```mermaid
flowchart TD
    A[User System] --> B[Web Browser]
    A --> C[Email Client]
    B --> D[Network Traffic]
    C --> D
    D --> E[Wireshark Capture Engine]
    E --> F[Protocol Decoders HTTP SMTP IMAP POP]
    F --> G[Browser Artifacts URLs Cookies Auth]
    F --> H[Email Headers Source IP Server Timestamps]
    G --> I[Findings and Reports]
    H --> I
```
## DESIGN STEPS:
### Step 1:
- Install Wireshark and ensure correct network adapter selection.
- Enable packet capturing for your active interface (Wi-Fi/Ethernet).

### Step 2:
**Web Browser Artifact Analysis**
- Open a browser and visit websites with login forms (use dummy credentials).
- In Wireshark, filter traffic with:
    - ```http``` for normal HTTP requests
    - ```http.cookie``` for cookies
    - ```http.authbasic``` for basic authentication
- Identify:
    - URLs visited
    - GET/POST requests
    - Cookies & session IDs
    - Credentials (if plaintext HTTP is used)
### Step 3:
- Capture email traffic by sending/receiving emails (dummy mail server or provided PCAP).
- Use filters:
    - ```smtp``` (Simple Mail Transfer Protocol)
    - ```pop``` / ```imap``` (for received mail)
- Inspect email headers:
    - Source IP
    - Mail server hostname
    - Timestamps
    - Possible forged headers
## PROGRAM:
```mermaid
flowchart TD
    A[Start Wireshark Capture] --> B[Generate Traffic: Web Browsing & Emails]
    B --> C[Apply Protocol Filters: HTTP/SMTP/IMAP/POP]
    C --> D[Extract Browser Artifacts: URLs, Cookies, Credentials]
    C --> E[Analyze Email Headers: Source, Server, Metadata]
    D --> F[Save Findings]
    E --> F[Save Findings]
    F --> G[Generate Digital Forensic Report]
```

## A. Capturing Traffic in Wireshark

1. Open Wireshark and start capturing on the active interface (Wi-
Fi/Ethernet).

<img width="952" height="1079" alt="Screenshot 2025-10-04 091420" src="https://github.com/user-attachments/assets/77442335-5ba6-4e2c-ad51-97ea7ed841d8" />


2. Perform activities like opening a website or sending an email through a
client (e.g., Gmail via browser or Thunderbird).




<img width="1593" height="1058" alt="Screenshot 2025-10-04 122124" src="https://github.com/user-attachments/assets/f6708345-f026-4254-b910-eff909703ea2" />


4. Stop the capture once done.


## B. Analyzing Web Browser Artifacts
1. Apply filters like: http, tcp.port == 443 (for HTTPS), or dns to isolate
browser traffic.


<img width="1920" height="1080" alt="Screenshot 2025-10-04 122203" src="https://github.com/user-attachments/assets/3e1487b9-2861-41a6-85e4-b3a2ae03ab7c" />





3. Inspect HTTP GET/POST requests:
o Look for URLs, hostnames, user agents, and cookies in the HTTP
headers.
o Follow TCP Stream to reconstruct page request flow:
▪ Right-click a packet → Follow → TCP Stream.

<img width="1920" height="1080" alt="Screenshot 2025-10-04 122654" src="https://github.com/user-attachments/assets/363cf0b1-f8de-4ffb-8063-a841344c214b" />

<img width="1920" height="1080" alt="Screenshot 2025-10-04 122310" src="https://github.com/user-attachments/assets/5fdcdcf9-befa-4481-a150-f77a090ab706" />


Analyze DNS Queries:
o Filter: dns
o Reveal domains the browser tried to resolve.

<img width="1920" height="1080" alt="Screenshot 2025-10-04 122613" src="https://github.com/user-attachments/assets/ab87a646-36ac-4b00-8afb-a97e3fd99225" />




## C. Email Header Analysis
1. Apply relevant filters:
o For POP3: tcp.port == 110
o For SMTP: tcp.port == 25 or 587
o For IMAP: tcp.port == 143 or 993

<img width="1920" height="1080" alt="Screenshot 2025-10-04 122654" src="https://github.com/user-attachments/assets/55518584-41e6-4722-832d-6b9027cb41aa" />




3. Locate email data:
o Look for SMTP packets to see sender/receiver email addresses.
o Use "Follow TCP Stream" to view the full email headers and body if
unencrypted.



<img width="1920" height="1080" alt="Screenshot 2025-10-04 123001" src="https://github.com/user-attachments/assets/d3d60bc5-450a-4766-ab5a-574c7cb04294" />



5. Extract Email Header Fields:
o Analyze From, To, Subject, Date, Message-ID, and relay servers used
in sending the email.


<img width="1920" height="1080" alt="Screenshot 2025-10-04 122930" src="https://github.com/user-attachments/assets/0bcaf15e-2968-405b-8ac9-dd3f5bfb5964" />



## OUTPUT:
Captured Web Activity and Email Header Information

## RESULT:
Web browser artifacts and email headers were successfully analyzed using Wireshark.

