# V2ray Server Setup Guide

## Setting up a V2ray Server

### Digital Ocean Account Setup

1. **Create a Digital Ocean Account:**
   - Sign up for a Digital Ocean account using a referral link, like this one: [Digital Ocean Referral Link](https://m.do.co/c/648197605dfe) this will give you $200 of credit to be used witihin 2 months.
   - Note: Students can get $200 credit for a year via Github Education.

2. **Add Billing Information:**
   - Add your billing information by linking a credit card to your Digital Ocean account. While other cloud providers can be used, AWS is not recommended due to potential issues.

### Droplet Creation and Configuration

3. **Create a Droplet:**
   - In the top right-hand corner, click "Create" and then select "Droplets."

4. **Configure Server Location:**
   - Choose a server location that's closest to where you'll be in China. For example, if you'll be in the eastern area of China, select San Francisco. You can create multiple servers in different locations if needed.

5. **Select OS and Version:**
   - Choose "Ubuntu" as the OS image and select "Ubuntu 22.04 LTS (x64)" as the version.

6. **Choose Virtual Machine Size:**
   - Opt for "Shared CPU: Basic."

7. **CPU Options:**
   - Select "Premium AMD." If you plan to use it with just a few devices (up to 8), choose the cheapest plan at $5/month.

8. **Authentication Method:**
   - Select "Password" for now, or you can set up SSH authentication separately.

### Initial Server Configuration

9. **Set Hostname:**
   - Change the hostname to something of your choice, for organizational purposes.

10. **Create the Droplet:**
    - Click "Create" and wait for your server to be provisioned.

11. **Note the IP Address:**
    - After the server is created, note down the IP address as you'll need it later.

### Server Software Setup

12. **Access the Server Console:**
    - In the "Droplets" tab, click on your server, and then click "Console." Wait for the console to fully load.

13. **Update Server Packages:**
    - Run the command `apt update && apt upgrade` to update the server with the latest packages. When prompted, type "y" and press Enter to confirm.

14. **Install X-Ray:**
    - Run the command `bash <(curl -Ls https://raw.githubusercontent.com/FranzKafkaYu/x-ui/master/install_en.sh)` (without quotation marks).

15. **X-Ray Configuration:**
    - Follow the prompts for X-Ray installation:
      - Type "y" to continue.
      - Set up your username and password for the x-ui admin panel.
      - Set the port to "54321."
      
16. **Access the Admin Panel:**
    - Type "x-ui" and press Enter.
    - Type "15" and press Enter to enable BBR.

### Web-Based Admin Panel Access

17. **Access Admin Panel in a Web Browser:**
    - Open a web browser and enter your server's IP address followed by the port number (e.g., "http://your_ip_address:54321").

18. **Log in to X-UI Admin Panel:**
    - Use the username and password you set up earlier to log in.

19. **Admin Panel Settings:**
    - Click on "Settings" and confirm the panel restart. Note the new URL for accessing the admin panel.

### Inbound Rules Configuration

20. **Preferred Language Setup:**
    - In your web browser settings, set "Chinese (Simplified)" as the preferred language for adding an inbound.

21. **Add Inbound Rules:**
    - Refresh the admin panel and go to "Inbound" -> "Add inbound."
    - Use the settings for "VLESS + XTLS + uTLS + REALITY."
    - Set the remark to your hostname and port to "443."
    - Toggle to enable "reality."

22. **Add a User:**
    - Click the "+" button next to "Add user" and select "xtls-rprx-vision" as the flow.

23. **Create the Inbound:**
    - Click "Add" at the bottom of the page to create your first inbound.

24. **Update X-Ray:**
    - In the X-UI admin panel, switch to the newest version of X-Ray on the status page and click "Restart X-ray."

25. **Export Links:**
    - You can export links and share them with your users. They just need to paste the link into their V2ray client.

## Setting up a V2ray Client

### V2ray Client Installation and Configuration

1. **Install a V2ray Client:**
   - Download and install a V2ray client, such as Shadowrocket, from the App Store or a trusted source.

2. **Configure V2ray Client:**
   - Open the V2ray client.
   - Locate the settings or configuration options.

3. **Import Configuration:**
   - Import the V2ray configuration by pasting the link provided by your server setup (Step 25 in the server setup section).

4. **Connect:**
   - Connect to the V2ray server by clicking the connect button in the V2ray client.

Please note that specific instructions for the V2ray client may vary based on the client you choose.
