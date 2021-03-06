# Process

## Critical System Processes

* Idle and System: 
  * These are not real processes \(in the sense that they have no corresponding executable on disk\). 
  * Idle is just a container that the kernel uses to charge CPU time for idle threads. 
  * System serves as the default home for threads that run in kernel mode. Thus, the System process \(PID 4\) appears to own any sockets or handles to files that kernel modules open.
* **csrss.exe**: 
  * The client/server runtime subsystem plays a role in **creating** and **deleting processes and threads**. It maintains a private list of the objects that you can use to cross-reference with other data sources. 
  * On systems before Windows 7, this process also served as the broker of commands executed via cmd.exe, so you can **extract command history** from its memory space. 
  * Expect to see **multiple CSRSS processes** because each session gets a dedicated copy; however, watch out for attempts to exploit the naming convention \(csrsss.exe or cssrs.exe\). 
  * Located in the **system32** directory. 
* **services.exe**: 
  * The Service Control Manager \(SCM\) manages Windows services and maintains a list of such services in its private memory space. 
  * **Parent** for any **svchost.exe** \(service host\) instances and processes such as **spoolsv.exe** and **SearchIndexer.exe** that implement services. 
  * There should be only **one** copy of **services.exe** on a system
  * Should be running from the **system32** directory.
* **svchost.exe**: 
  * A clean system has multiple shared host processes running concurrently, each providing a container for DLLs that implement services.    _Their **parent** should be **services.exe**, and the path to their executable should point to the \*system32_ directory. 
  * A few of the common names \(such as scvhost.exe and svch0st.exe\) can be used by malware to blend in with these processes.
* **lsass.exe**: 
  * The local security authority subsystem process is responsible for enforcing the security policy, verifying passwords, and creating access tokens. As such, it’s often the target of code injection because the **plaintext password hashes** can be found in its private memory space. 
  * There should be only **one instance** of **lsass.exe** running from the **system32** directory
  * Its **parent** is **winlogon.exe** on **pre-Vista machines**, and **wininit.exe** on **Vista and later systems**. 
  * Stuxnet created two fake copies of lsass.exe, which caused them to stick out like a sore thumb.
* **winlogon.exe**: 
  * This process presents the interactive logon prompt, initiates the screen saver when necessary, helps load user profiles, and responds to Secure Attention Sequence \(SAS\) keyboard operations such as CTRL+ALT+DEL. 
  * This process monitors files and directories for changes on systems that implement Windows File Protection \(WFP\). 
  * Its executable is located in the **system32** directory.
* **explorer.exe**: 
  * **One** Windows Explorer process for each logged-on user. 
  * It is responsible for handling a variety of user interactions such as GUI-based folder navigation, presenting the start menu, and so on. 
  * It also has access to sensitive material such as the documents you open and credentials you use to log in to FTP sites via Windows Explorer.
* **smss.exe**: 
  * The session manager is the first real user-mode process that starts during the boot sequence. 
  * It is responsible for creating the sessions that isolate OS services from the various users who may log on via the console or Remote Desktop Protocol \(RDP\).

![](../.gitbook/assets/windows-process-diagram.jpg)

