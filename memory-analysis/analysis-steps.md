# Analysis Steps

* Identify rogue processes
  * Analyse processes
    * Legitimate process?
    * Name spelled right?
    * Fits with system context?
  * Full path
    * Is the process executable in the usual place?
    * Is it running from user or temp directories?
  * Parent process
    * Is it as expected?
  * Command line
    * Does it have the right switches?
  * Start time
    * Was it started at boot or something else?
    * Did the process start close the time of a known incident?
  * Security ID
    * Does the SID make sense? Would a system process run with a user accounts’ SID?
* Analysing process objects
  * DLLs
  * Handles
    * Files and directories
      * Look at occurrance of use. Malware files should, historically, be the least accessed files on the system
    * Registry
    * Events
    * Threads
    * Sockets
* Network artifacts
  * Suspicious ports
    * out-of-the-ordinary ports
    * listening ports \(backdoors\)
  * Suspicious connections
    * Anything connecting out
    * Known bad-IPs
    * Creation time matching an incident
  * Suspicious processes
    * Should this process have networking capabilities?
* Detecting code injection
  * Look for DLL injection and process hollowing
* Rootkit detection
  * Not a big thing anymore, most AV does a good job at detecting this
  * Hides in
    * System service descriptor tables
    * Interrupt descriptor tables
    * Function import address tables
    * I/O request packets
* Acquiring processes and drivers
  * Submit for reverse engineering or AV analysis
  * Review strings
    * add to bad-words list

