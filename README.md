<h1> Phishing Mail Analyses </h1>

<h2>Description</h2>
This lab exercise showcases ways new security professionals can effectively analyze suspicious mails. It also creates awareness for the general public on indicators/red flags to look out for on mails and maybe investigate further using the outlined methodology and tools.
<br />

<h2>Objective</h2>
- Spot the indicators within the body of the mail<br />
- Identify and decode any hidden URL within the body of the mail<br />
- 


<h2>Tools used include:</h2>

- <b>CyberChef</b>, <b>URLScan</b>, <b>VirusTotal</b>, <b>Any.run</b>, <b>MxToolbox</b>, <b>AbuseIPDB</b>, <b>Talos Intelligence</b>, <b>PhishTool</b>


<h2>Sample 1 </h2>

Before we delve into analyzing the intriguing mail samples, I want to encourage you—especially if you're new to this concept—to explore the diverse phishing indicators available [here](https://github.com/custyblak/Phishing_MindMap/tree/main). It's a valuable resource that will enhance your understanding as we navigate through this analysis."

<p align="center">
<img src="https://imgur.com/SJohW8K.png" height="100%" width="80%" alt="Phishing Sample 1"/> 
<br />

The sample mail pretends to be legitimate coming from Microsoft (sender's address). However, the content of the mail focuses on **cryto**, which is absurd and then the closure signature references a different domain (Binance.com)

Lets explore other indicators (from the start of the mail):<br />
- Multiple spelling errors observed (Inappropriate spacing within words)
- Created a sense of urgency in "**...the first 2500 to apply...**", "**The airdrop will end on July 29, 2023, 18:00 UTC, with a limited supply...**" and "**...on a first come, first served basis...**"
- Reward lure up to $80,000 mentioned to entice the user
- The "Join Airdrop" button redirects to a different destination that is not related to either "Binance.com" or "Microsoft.com" when hovered over. This will be investigated later.

Having seen the obvious indicators, let's analyze the mail header.
On checking the raw format of the email, it was noticed that the body of the mail was encoded using base64 as shown below.

<p align="center">
<img src="https://imgur.com/8CXliYI.png" height="100%" width="80%"> 
<br />

<p align="center">
<img src="https://imgur.com/SJohW8K.png" height="100%" width="80%" alt="Phishing Sample 1"/> 
<br />

