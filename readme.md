### Install KMS Host Role on Windows Server
1. Install the Volume Activation Services role on your server from the Server Manage
2. Enable a Windows Firewall rule that allows clients to access the KMS server: ```Enable-NetFirewallRule -Name SPPSVC-In-TCP``` (this will open port TCP 1688 on the server).
3. Install a new KMS key on the server using the command: ```slmgr /ipk <KMS_host_key_Windows_Server_2022>```
Tip. If the KMS host was enabled with a key for an earlier version of Windows Server, you must first remove the KMS host key: ```slmgr /upk```
4. Activate your KMS server against the Microsoft activation servers: ```slmgr /ato``` (your server must have direct internet access during activation). Or you can activate the KMS host by phone (run the graphical Volume Activation Tools from the Server Manager);
5. To publish an SRV record in the DNS to allow clients to automatically discover the KMS host in the domain, run the command: slmgr /sdns
6. Restart the Software Protection service: ```Restart-Service -Name sppsvc```
Ensure that your KMS server has been successfully activated. Run the command: slmgr.vbs /dlv Make sure the result includes: Description = VOLUME_KMS_WS22 channel and License status = Licensed.