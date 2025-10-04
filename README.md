# Ex 10 Using-Wireshark---analyzing-web-browser-artifacts-email-header-analysis
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
## PROGRAM AND OUTPUT:
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
<img width="1919" height="1079" alt="Screenshot 2025-10-04 140800" src="https://github.com/user-attachments/assets/4e61b9ab-8c97-4315-811e-09463e89243e" />





2. Perform activities like opening a website or sending an email through a
client (e.g., Gmail via browser or Thunderbird).

<img width="1919" height="663" alt="Screenshot 2025-10-04 150151" src="https://github.com/user-attachments/assets/ff0560e3-706d-4b7b-b0f2-2cb6274ef4f0" />





3. Stop the capture once done.


## B. Analyzing Web Browser Artifacts
1. Apply filters like: http, tcp.port == 443 (for HTTPS), or dns to isolate
browser traffic.


<img width="1919" height="856" alt="Screenshot 2025-10-04 150225" src="https://github.com/user-attachments/assets/325032c9-9676-4a24-ac4a-c38716bb3aaa" />




3. Inspect HTTP GET/POST requests:
o Look for URLs, hostnames, user agents, and cookies in the HTTP
headers.
o Follow TCP Stream to reconstruct page request flow:
▪ Right-click a packet → Follow → TCP Stream.
<img width="1408" height="746" alt="Screenshot 2025-10-04 150422" src="https://github.com/user-attachments/assets/ed68d610-bf1d-43bf-988b-a5a37390fa3f" />




Analyze DNS Queries:
o Filter: dns
o Reveal domains the browser tried to resolve.


<img width="1919" height="1079" alt="Screenshot 2025-10-04 140826" src="https://github.com/user-attachments/assets/66d32592-aa13-4c5c-b25c-72d984ce2397" />



## C. Email Header Analysis
1. Apply relevant filters:
o For POP3: tcp.port == 110
o For SMTP: tcp.port == 25 or 587
o For IMAP: tcp.port == 143 or 993


<img width="1909" height="985" alt="Screenshot 2025-10-04 150449" src="https://github.com/user-attachments/assets/aaa91121-96df-4a13-8fcb-be7a8311d14d" />


3. Locate email data:
o Look for SMTP packets to see sender/receiver email addresses.
o Use "Follow TCP Stream" to view the full email headers and body if
unencrypted.


<img width="1414" height="335" alt="Screenshot 2025-10-04 150551" src="https://github.com/user-attachments/assets/5e29dbbe-e6a8-4a87-94c6-49a5a63d4db6" />




5. Extract Email Header Fields:
o Analyze From, To, Subject, Date, Message-ID, and relay servers used
in sending the email.


<img width="1916" height="1078" alt="497424983-fd8fc3f0-298c-4504-ab96-adae65be8453" src="https://github.com/user-attachments/assets/f1e4f9eb-979c-4eaa-92ff-fb2d718a369d" />



Captured Web Activity and Email Header Information

## RESULT:
Web browser artifacts and email headers were successfully analyzed using Wireshark.

