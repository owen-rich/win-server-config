# Windows Server Manager Configuration

## Lab Mission
Promote GUI and non-GUI Windows servers to domain controllers and add clients.


## Requirements
- Knowledge of Oracle VirtualBox
- Knowledge of networking
- Fundamental understanding of the Windows operating system

## Resources
- **Environment & Tools**
  - VirtualBox
    - 2 x Windows Server 2016 VMs
    - Windows Client 7 VM
    - Windows Client 10 VM

---

## Lab Task 1: Install Active Directory Domain Services
Add the Active Directory Domain Services feature to Server1.

1. In Server1, open the **Server Manager**. Navigate to **Manage > Add Roles and Features**.
2. Click **Next** until you see **Server Roles** in the left pane, and select **Active Directory Domain Services**. Click **Add Features** when prompted.
3. Click **Next** until you reach the **Confirm installation selections** prompt. Click **Install**.
4. At the end of the installation, click **Close**.

   > **Note:** After finishing the installation, you can close the installation wizard and reopen it by clicking the flag icon in the top pane.

---

## Lab Task 2: Promotion to Domain Controller (DC)
Promote Server1 to a domain controller.

1. Continue from where you left off in the wizard by clicking the flag icon and then selecting **Promote this server to a domain controller**.
2. Create a new forest and name it **cyber.local**.
3. For the password, enter **(Secure Password)**, and click **Next**.
4. In the window with the DNS delegation alert, click **Next**.
5. Leave all other settings as default and continue by clicking **Next** and **Install**.
6. The server will restart. After the restart, log in as **CYBER\Administrator**.

---

## Lab Task 3: Adding Server2 to the Domain

1. On the Windows 2016 server core, type `sconfig` to enter the configuration options.
2. Select **Option 1** to join a domain by typing **D**. Enter the Domain name **cyber.local**, and the authorized domain user **cyber\administrator**.
3. Type in the administrator password for Server1 (**(Secure Password)**). The password will not populate on the screen. When prompted to change the name, press **No**; when prompted to restart, press **Yes**.

---

## Lab Task 4: Checking Server2 in Server1

1. Switch to Server1, go to **All Servers**, right-click, and select **Add Servers**.
2. In the **Name** field, type **Server2** and press **Find Now**. Then select **Server2** and click on the right arrow to move it to the right column, then press **OK**.
3. You should now see Server2 in the **All Servers** field.

---

## Lab Task 5: Adding Clients to the Domain
Configure the Windows 7 and Windows 10 VMs using the following settings:

- **Windows 7 VM**
  - Name: Client7
  - IP Address: 10.0.0.3
  - Subnet Mask: 255.255.255.0
  - DNS Server: 10.0.0.1

- **Windows 10 VM**
  - Name: Client10
  - IP Address: 10.0.0.4
  - Subnet Mask: 255.255.255.0
  - DNS Server: 10.0.0.1

Each Windows client VM needs to be added to the Domain. The following steps apply to both Windows 7 and Windows 10 VMs.

1. In the Windows 10 client, click on the network, then click on **Network Settings**.
2. Ensure you are under **Ethernet**, then go to **Change adapter options**.
3. On **Ethernet**, right-click and go to **Properties**.
4. In the **Networking** tab, go to **Internet Protocol Version 4 (TCP/IPv4)**, press **Properties** to enter the static IP, subnet mask, and DNS server. When finished, press **OK**.
5. Open the folder, hover, and right-click on **This PC** to click on **Properties**.
6. While in **System**, go to **Change settings**.
7. Click on **Change** to change the computer name to **Client10**. Then select **Domain** and enter **cyber.local**. Click **OK** to enter the Domain.
8. Enter the credentials **cyber\administrator** with the password **(Secure Password)**. After hitting **OK**, you will receive a prompt to restart your computer; press **OK**. Close the windows and press **Restart Now**.

   > **Note:** The following steps are specifically for the Windows 7 client:

9. In the Windows 7 client, click on the network, then click on **Open Network and Sharing Center**.
10. Click on **Local Area Connection** and go to **Properties**.
11. Go to **IPv4**, click on **Properties**, and enter the IP address, subnet mask, and DNS:
    - IP Address: 10.0.0.3
    - Subnet Mask: 255.255.255.0
    - DNS: 10.0.0.1 (alternate: 8.8.8.8)

12. In the Windows 7 client, click **Start** (Windows symbol), right-click **Computer**, and choose **Properties** to access the system.
13. Click **Change Settings**, then click **Change...** In the **Change** field, instead of **Workgroup**, choose **Domain** and type the full name of the Domain: **cyber.local**.
14. When a prompt appears asking for administrative credentials, use the **Administrator** user with the password you previously defined in Server1.
15. Verify that a welcome message appears. Click **OK** to clear the **Computer Name/Domain Changes** windows. After clicking **OK** to restart your client, click **Close**, and then **Restart Now**.

---

## Lab Task 6: Logging into the Domain

1. You can log into a domain user on the login screen by clicking **Switch User** and then **Other User**.
2. Log into your client as **Cyber\Administrator**.
