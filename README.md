<h1> Phishing Mail Analyses </h1>

<h2>Description</h2>
This lab exercise showcases ways new security professionals can effectively analyze suspicious mails. It also creates awareness for the general public on indicators/red flags to look out for on mails and maybe investigate further using the outlined methodology and tools.
<br />

<h2>Objective</h2>
- Spot the indicators within the body of the mail<br />
- Identify and decode any hidden URL within the body of the mail<br />
- Analyze the header information 


<h2>Tools used include:</h2>

- <b>CyberChef</b>, <b>URLScan</b>, <b>VirusTotal</b>, <b>Any.run</b>, <b>MxToolbox</b>, <b>AbuseIPDB</b>, <b>Talos Intelligence</b>, <b>PhishTool</b>, <b>Hybrid-analysis</b>


<h2>Sample 1 </h2>

Before we delve into analyzing the intriguing mail samples, I want to encourage you especially if you're new to this concept, to explore the diverse phishing indicators available [here](https://github.com/custyblak/Phishing_MindMap/tree/main). It's a valuable resource that will enhance your understanding as we navigate through this analysis."

<p align="center">
<img src="https://imgur.com/SJohW8K.png" height="100%" width="80%" alt="Phishing Sample 1"/> 
<br />

The sample mail pretends to be legitimate coming from Microsoft (sender's address). However, the content of the mail focuses on **cryto**, which is absurd because the services rendered by Microsoft doesn't include Crytocurrent and then the closure signature references a different domain (Binance.com) and a [WHOIS](https://whois.domaintools.com) lookup on Binance.com, shows no relationship with Microsoft Corporation.

<p align="center">
<img src="https://imgur.com/4r7V2XN.png" height="100%" width="80%" alt="WHOIS INFO"/> 
<br />
  
Lets explore other indicators (from the start of the mail):<br />
- Multiple spelling errors observed (Inappropriate spacing within words)
- Created a sense of urgency in "**...the first 2500 to apply...**", "**The airdrop will end on July 29, 2023, 18:00 UTC, with a limited supply...**" and "**...on a first come, first served basis...**"
- Reward lure up to $80,000 mentioned to entice the user
- The "Join Airdrop" button redirects to a different destination that is not related to either "Binance.com" or "Microsoft.com" when hovered over. This will be investigated later.

Having seen the obvious indicators, let's analyze the header information.

Tools like PhishTool or MxToolbox can be used to effienctly analyze the header information.

Copy and paste the raw HTML header information into the **MxToolbox** mail header analyzer column and then click on "Analyze header". The result comprises of:

- Email Authentication- SPF, DKIM & DMARC Compliance: From the output below, it is seen that the mail doesn't have any DKIM & DMARC records which adds to the suspicion. Because both are crucial in enhancing the security email communication, prevent phishing attacks, and build trust with both email service providers and recipients.
  
  <p align="center">
  <img src="https://imgur.com/xCxU89q.png" height="100%" width="80%"> 
  <br />
  
  <p align="center">
  <img src="https://imgur.com/OdH2b8e.png" height="100%" width="80%"> 
  <br />

- Email Path: This shows all intermediary SMTP servers inbetween the sender and receiver through which the mail was routed.
  <p align="center">
  <img src="https://imgur.com/uFwxD3q.png" height="100%" width="80%"> 
  <br />
- Other header information such as X-headers,
  <p align="center">
  <img src="https://imgur.com/aS3Xm2L.png" height="100%" width="80%"> 
  <br />
Similar information is also seen using **PhishTool**. However, the header information are splitted into sections- 
- Headers: This contains the basis information of the mail such as sender's & receiver's addresses, Reply-to, Timestamp, Reply-path
  <p align="center">
  <img src="https://imgur.com/cCz0tO1.png" height="100%" width="80%"> 
  <br />
- Received Lines: This lists the different hops through which the mail got to the receiver.
  <p align="center">
  <img src="https://imgur.com/8rJIlv3.png" height="100%" width="80%"> 
  <br />
- X-Headers: 
  <p align="center">
  <img src="https://imgur.com/wGj89eU.png" height="100%" width="80%"> 
  <br />
- Security: This shows the authentication results of SPF, DKIM & DMARC.
  <p align="center">
  <img src="https://imgur.com/MlavY8O.png" height="100%" width="80%"> 
  <br />
- Attachment & Message URLs: This shows embedded attachment and links within the body of the mail.
  <p align="center">
  <img src="https://imgur.com/O5Sf10S.png" height="100%" width="80%"> 
  <br />

  <p align="center">
  <img src="https://imgur.com/PH9ig4N.png" height="100%" width="80%"> 
  <br />
On checking the raw format of the email, it was noticed that the body of the mail was encoded using base64 as shown below.

<p align="center">
<img src="https://imgur.com/8CXliYI.png" height="100%" width="80%"> 
<br />

Utilizing CyberChef, unveil concealed URLs within the email body by decoding it. The recommended approach involves inputting the raw HTML, encompassing both the email header and body. Apply the "Extract URLs" recipe to retrieve the embedded URLs. For this sample, given that the header wasn't encoded, we are focusing solely on the body by excluding the mail header.

Employing a sequence of recipes, namely "From Base64," "Regular expression (with URL built-in regex) selected," and "Extract URLs," the obscured URL was exposed. The revealed URL has been defanged for safety measures, appearing as hxxps[://]click[.]pstmrk[.]it/3s/sweedbuy[.]com%2Fblog%2F/ahc/k_CuAQ/AQ/44a54f89-410d-4729-b21c-32c30d6eb945/1/qOoKiS9V1s?/23687658rodrigofp.
<p align="center">
<img src="https://imgur.com/89e0qvi.png" height="100%" width="80%"> 
<br />

Utilizing urlscan.io


