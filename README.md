# Volatility: Process Memory Analysis

<h2>Description</h2>
In this Digital Forensics task, I used volatility to list out processes and investigate a suspicious pid using its processtree and the commandline. 

<h2>Languages and Utilities Used</h2>

- <b>python3</b>
- <b>volatility</b>

<h2>Environments Used </h2>

- <b>Ubuntu</b> 

<br />
<br />
Running volatility windows.pslist to generate a process list for the windows 10 memory dump. 

![1) volatility windows pslist](https://github.com/user-attachments/assets/b2e78e83-e658-4f7d-ad3c-dd3ffa076b9f)

<br />
<br />
There is an abnormal svchost witht he suspicious processid 5792, grepping out its parent pid 3728 shows it spawn from explorer.exe. 

![2) svchost with abnormal parentprocessid ](https://github.com/user-attachments/assets/23d75dad-4e30-4da1-bf9d-7e2bdc369420)

<br />
<br />  
Using windows.pstree on pid 5792 shows the full path for the suspicious svchost.exe. 

![3) running volatility pstree pid 5792 sus pid](https://github.com/user-attachments/assets/eed5a93e-37bc-4cff-9b29-e255927289e5)

<br />
<br />
Using windows.cmdlin and grepping svchost.exe shows all svchosts with the -k flag execept for one. 

![4) running volatility cmdline grep for svchost shows 1 svchost malicious](https://github.com/user-attachments/assets/f04a2e4e-3c2d-4264-8bf0-80bb5610d058)

<br />
<br />
Performing a dump on pid5792 from windows.pslist with output -o onto the ~/Desktop then checking that it is a portable executable with the MZ file signature in its header and generating a sha256 hash. 

![5) extracting malicious PE into dump and sha256](https://github.com/user-attachments/assets/94c712a1-170b-443a-9517-533f6a161e08)

<br />
<br />  
The hash on virustotal shows it is malicious. 

![6) vtotal](https://github.com/user-attachments/assets/ac6247e6-6a18-4cd5-aa15-5fc665feba80)

<br />
<br />
Using windows.dlllist against --pid 5792 lists all the dlls imported from pid 5792.

![7) list of all dlls imported from malicious process](https://github.com/user-attachments/assets/7cfd98fb-c092-4e70-806d-c052be8e5194)

<br />
<br />
