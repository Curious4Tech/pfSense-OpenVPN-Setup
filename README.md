# pfSense-OpenVPN-Setup
Step-by-step guide to configuring OpenVPN on pfSense using the built-in wizard. This setup allows secure, encrypted remote access to your network. Includes certificate setup, server configuration, tunnel settings, and client export instructions for a quick, efficient VPN deployment.


# OpenVPN Setup on pfSense Using Wizard

This guide provides a step-by-step setup for configuring OpenVPN on pfSense using the built-in wizard. OpenVPN allows secure, remote access to your network through an encrypted tunnel. 

## Prerequisites

- **pfSense** installed and accessible.
- **Admin access** to the pfSense firewall.
- A basic understanding of network configuration is recommended.

---

## Steps to Set Up OpenVPN on pfSense

### Step 1: Access the OpenVPN Wizard
1. Log in to the **pfSense** web interface.
2. Navigate to **VPN > OpenVPN**.
3. Click on the **Wizards** tab to start the OpenVPN setup wizard.

![image](https://github.com/user-attachments/assets/3ff74265-c96e-4176-9d87-13c9f6eb7d90)


### Step 2: Configure the OpenVPN Server with the Wizard
1. Choose **Local User Access** for user authentication, or select a different method if you have an external authentication server.
2. Click **Next** to proceed.


![image](https://github.com/user-attachments/assets/842ba941-145c-4f3f-a691-a100025de913)



### Step 3: Set Up the Certificate Authority (CA)
1. Choose **Create a new Certificate Authority** if you don’t have an existing CA.


![image](https://github.com/user-attachments/assets/39744777-6cea-4a55-acff-93de4e3f58c9)
   

3. Enter a **Descriptive Name** (e.g., `OpenVPN-CA`).
4. Fill in the required fields, such as **Country Code**, **State**, **City**, **Organization**, etc.
5. Click **Add new CA**.


![image](https://github.com/user-attachments/assets/fd9ab6c6-e704-4c9b-ae7c-4925b9739c7f)


### Step 4: Create the Server Certificate
1. Choose **Create an internal Certificate** for the OpenVPN server.
2. Provide a **Descriptive Name** (e.g., `OpenVPN-Server`).
3. Complete the necessary fields, similar to those in the CA setup.
4. Click **Create new Certificate**.

### Step 5: Configure the OpenVPN Server
1. **Description**: Enter a name for your VPN server (e.g., `OpenVPN`).
2. **Protocol**: Select **UDP** for better performance, or **TCP** if UDP is blocked on your network.
3. **Device Mode**: Set to **tun** (tunnel mode).
4. **Interface**: Choose the **WAN** interface.
5. **Local Port**: Use **1194** or specify another port if necessary.



![image](https://github.com/user-attachments/assets/b29c3e22-7d0f-47bd-a5fb-c26332229ce5)



### Step 6: Configure Cryptographic Settings
1. **TLS Authentication**: Enable this for additional security.
   - pfSense will generate the TLS key for authentication.
2. **Peer Certificate Authority**: Select the CA created in Step 3.
3. **Server Certificate**: Choose the server certificate created in Step 4.
4. **DH Parameter Length**: Set to **2048-bit** for a balance of security and performance.
5. **Encryption Algorithm**: Select **AES-256-CBC**.
6. **Auth Digest Algorithm**: Choose **SHA256**.
7. **Hardware Crypto**: Select **No Hardware Crypto Acceleration** unless you have specific hardware support, such as AES-NI.



![image](https://github.com/user-attachments/assets/9acfc5d6-2d02-4568-b050-ff73b04082ac)



### Step 7: Configure Tunnel Settings
1. **IPv4 Tunnel Network**: Specify an unused subnet, such as `10.0.8.0/24`, for VPN clients.
2. **IPv6 Tunnel Network**: Leave blank unless you plan to use IPv6.
3. **Redirect IPv4 Gateway**: Check this if you want all client traffic routed through the VPN.
4. **Local Network**: Enter the local network(s) accessible to VPN clients, e.g., `192.168.1.0/24`.
5. **Concurrent Connections**: Set a limit if required.
6. **Compression**: Set to **No Preference** or **LZO Compression** if needed.



 ![image](https://github.com/user-attachments/assets/edbd2efb-f72f-4850-91e6-99347b189785)
 

### Step 8: Configure Client Settings
1. **DNS Default Domain**: Enter an internal domain if applicable.
2. **DNS Servers**: Specify DNS servers for the VPN clients if desired.
3. **Next** to continue the configuration settings.


   
  ![image](https://github.com/user-attachments/assets/973dce9e-7d55-4f8c-8aa2-5b08c610b7c9)



4. Check **Firewall rule** and **OpenVPN rule**, and then click on **Next**



 ![image](https://github.com/user-attachments/assets/4d69d1a5-8c00-4203-8338-a3a53ac67b39)

   
5. Click on **Finish** to save the configurataion


 ![image](https://github.com/user-attachments/assets/dbea298c-dda3-4b06-b6d7-2f5bf198abbc)


### Step 9: Create OpenVPN Users
1. Go to **System > User Manager** in the pfSense menu.


 ![image](https://github.com/user-attachments/assets/c290d005-7de1-4110-b57b-b263e7df369f)


3. Click **Add** to create a new user.


 ![image](https://github.com/user-attachments/assets/4d6f25dc-efbe-4f29-a1f7-1732849c0f30)

4. Set a **Username** and **Password**.

   
 ![image](https://github.com/user-attachments/assets/feb627cc-6f89-431c-93d3-4d1c24592da5)


6. In the **Certificates** section, click **Add New Certificate** to generate a certificate for the user.


 ![image](https://github.com/user-attachments/assets/1904d4ed-0530-49e7-9179-6e0562b02399)


8. Save the user configuration.

### Step 10 : Assign Permissions:

1. Go to **System > User Manager**.
2. Select the user, then under **Effective Privileges**, click **Add**.
3. Assign the above-listed permissions as needed.
4. Save the settings.



 ![image](https://github.com/user-attachments/assets/6bad50fa-84ed-4b0e-a885-2fe8fc054c6e)


---

### Next Steps
Once the esrver configuration is setup , you can proceed to set up the OpenVPN client VPN connection.

---

## Additional Resources
- [pfSense Documentation](https://docs.netgate.com/pfsense/en/latest/)
- [OpenVPN Documentation](https://openvpn.net/as-docs/general.html))

---

Feel free to open an issue if you encounter any problems during setup. 

---

**Disclaimer**: This guide assumes basic networking knowledge and administrative rights to pfSense. Use caution when making firewall and VPN configurations, as incorrect settings may impact network security and accessibility.
