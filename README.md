# Tor-hidden-services-forensics-tool
Tor hidden services forensics tool was created for final project on (Basics of) Digital forensics course. It is used for forensic analysis of server that contains active website on tor network.

Program works as follows:
 
  - After displaying welcome message, index.html file is created in current directory from strings(complete file is written in multiple strings withing array, which are then written to newly created file). This file is used to replace whole page after seizing website. It contains single image in base64 encoding.
  - Now tool checks if server is active on tor network (by using curl command on socket 9050 to check.torproject.com website and checking replay content).
  - Then it starts checking for "torrc" files. Firstly it checks on default paths, then if file is not found it asks user if he wants to check whole disk (i.e. from root /).
  - If tool finds at least one "torrc" file its proceeds with extracting necessary information, otherwise it displays message that such file is not found.
    - After extracting "HiddenServiceDirectory" and "HiddenServicePort" data, it displays hostname (i.e. website address on tor network) and asks user if he wants to copy website directory elsewhere.
    - Next it displays address and port on which website is locally hosted (using installed web server - Apache, nginx, ...).
    - Finally option for seizing website is shown to user. If answered "Y" website is replaced with index.html file previously created by tool.
    - This process is repeated for every hosted site.
  - Lastly tool starts checking for databases (only MySQL and PostgreSQL are supported). If it finds any, option to copy its files is prompt to user.
  - At the end tool removes index.html form current directory and goodbye message is shown.

This tool works on limited number of scenarios (only websites complete stored in directory written in "torrc" file, or in parent directory of "public" folder) and it has executable for macOS and Linux (compiled with g++ compiler using c++2a).
