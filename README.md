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

### Step 2: Configure the OpenVPN Server with the Wizard
1. Choose **Local User Access** for user authentication, or select a different method if you have an external authentication server.
2. Click **Next** to proceed.

### Step 3: Set Up the Certificate Authority (CA)
1. Choose **Create a new Certificate Authority** if you don’t have an existing CA.
2. Enter a **Descriptive Name** (e.g., `OpenVPN-CA`).
3. Fill in the required fields, such as **Country Code**, **State**, **City**, **Organization**, etc.
4. Click **Create new Certificate Authority**.

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

### Step 6: Configure Cryptographic Settings
1. **TLS Authentication**: Enable this for additional security.
   - pfSense will generate the TLS key for authentication.
2. **Peer Certificate Authority**: Select the CA created in Step 3.
3. **Server Certificate**: Choose the server certificate created in Step 4.
4. **DH Parameter Length**: Set to **2048-bit** for a balance of security and performance.
5. **Encryption Algorithm**: Select **AES-256-CBC**.
6. **Auth Digest Algorithm**: Choose **SHA256**.
7. **Hardware Crypto**: Select **No Hardware Crypto Acceleration** unless you have specific hardware support, such as AES-NI.

### Step 7: Configure Tunnel Settings
1. **IPv4 Tunnel Network**: Specify an unused subnet, such as `10.0.8.0/24`, for VPN clients.
2. **IPv6 Tunnel Network**: Leave blank unless you plan to use IPv6.
3. **Redirect IPv4 Gateway**: Check this if you want all client traffic routed through the VPN.
4. **Local Network**: Enter the local network(s) accessible to VPN clients, e.g., `192.168.1.0/24`.
5. **Concurrent Connections**: Set a limit if required.
6. **Compression**: Set to **No Preference** or **LZO Compression** if needed.

### Step 8: Configure Client Settings
1. **DNS Default Domain**: Enter an internal domain if applicable.
2. **DNS Servers**: Specify DNS servers for the VPN clients if desired.
3. **Save** to apply these settings.

### Step 9: Create OpenVPN Users
1. Go to **System > User Manager** in the pfSense menu.
2. Click **Add** to create a new user.
3. Set a **Username** and **Password**.
4. In the **Certificates** section, click **Add New Certificate** to generate a certificate for the user.
5. Save the user configuration.

### Step 10: Export the VPN Client Configuration
1. Navigate to **VPN > OpenVPN > Client Export**.
2. Under **Client Export Package**, locate your VPN configuration.
3. **Download the installer** or configuration files needed for your device.
   - If using OpenVPN Connect, download the **.ovpn file** for importing.

---

### Next Steps
Once the configuration files are downloaded, you can proceed to set up the OpenVPN client on your device to test the VPN connection.

---

## Additional Resources
- [pfSense Documentation](https://docs.netgate.com/pfsense/en/latest/)
- [OpenVPN Documentation](https://openvpn.net/vpn-server-resources/documentation/)

---

Feel free to open an issue if you encounter any problems during setup. 

---

**Disclaimer**: This guide assumes basic networking knowledge and administrative rights to pfSense. Use caution when making firewall and VPN configurations, as incorrect settings may impact network security and accessibility.
