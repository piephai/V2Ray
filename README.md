# V2ray Server Setup Guide

I tried to install V2Ray on several cloud hosting platforms, including AWS (including Lightsail) and Digital Ocean. However, none of the configurations I experimented with could reliably penetrate China's Great Firewall on AWS servers. Vultr rejected my payment card, so I had to look for alternatives. I chose Digital Ocean. Digital Ocean has been running smoothly for several weeks, with excellent reliability and minimal speed loss.

Using this system has been economical, as each server only costs $5 a month in China. Although it has the potential for commercial use, my main goal is to provide this information to travelers to China so they can save $30/month on services like Astrill that often require switching between servers. Both Astrill and V2Ray worked in my experience, but I found the V2Ray setup to be more reliable.

However, there are some drawbacks compared to other VPNs like Astrill, such as the lack of URL-specific bypasses. This may not be a big issue for me while traveling in China, but it may be a problem if you plan to live here for a long time.

If you want to avoid VPNs altogether, the easiest way is to use a SIM card from Hong Kong (if you're flying in from there) or roam with a SIM card from your home country. For example, if you have a SIM card from Malaysia, you can use that SIM card to roam in China while getting 2GB of data per day for only 99RM ($21 US) per month. This may be cheaper than getting a SIM card in China. However, without a local Chinese phone number, you won't be able to use some local services such as ordering takeout and buying tickets via WeChat.


## Setting up a V2ray Server

### Digital Ocean Account Setup

1. **Create a Digital Ocean Account:**
   - Sign up for a Digital Ocean account using a referral link, like this one: [Digital Ocean Referral Link](https://m.do.co/c/648197605dfe) this will give you $200 of credit to be used within 2 months.
   - Note: Students can get a $200 credit that is valid for a year via GitHub Education.

2. **Add Billing Information:**
   - Add your billing information by linking a credit card to your Digital Ocean account. While other cloud providers can be used, AWS is not recommended due to potential issues.

### Droplet Creation and Configuration

3. **Create a Droplet:**
   - In the top right-hand corner, click "Create" and then select "Droplets."

4. **Configure Server Location:**
   - Choose a server location that's closest to where you'll be in China. For example, if you're in the eastern area of China, select San Francisco. You can create multiple servers in different locations if needed.

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
      ![Pasted Graphic 1](https://github.com/piephai/V2Ray/assets/65212311/5d1eca9e-6393-44f8-8aed-424d6eaace60)
      <img width="1002" alt="Pasted Graphic 2" src="https://github.com/piephai/V2Ray/assets/65212311/fbfee5ac-c3ce-402d-a56b-072b346a6ee1">

13. **Update Server Packages:**
    - Run the command `export DEBIAN_FRONTEND=noninteractive && apt update -y && apt upgrade -y` to update the server with the latest packages.

14. **Install X-Ray:**
    - Run the command `bash <(curl -Ls https://raw.githubusercontent.com/FranzKafkaYu/x-ui/master/install_en.sh)`.

15. **X-Ray Configuration:**
    - Follow the prompts for X-Ray installation:
      - Type "y" to continue.
      - Set up your username and password for the x-ui admin panel.
      - Set the port to "54321."
      
16. **Enable BBR:**
    - Type "x-ui" and press Enter.
    - Type "15" and press Enter to enable BBR.

### Web-Based Admin Panel Access

17. **Access Admin Panel in a Web Browser:**
    - Open a web browser and enter your server's IP address followed by the port number (e.g., "http://your_ip_address:54321").
      <img width="1503" alt="Pasted Graphic 7" src="https://github.com/piephai/V2Ray/assets/65212311/d49c8b14-8af4-42b4-bc3a-fdfa852879df">

18. **Log in to X-UI Admin Panel:**
    - Use the username and password you set up in step 15 to log in.
      <img width="901" alt="Pasted Graphic 10" src="https://github.com/piephai/V2Ray/assets/65212311/dd6bab36-5a44-4ee3-874a-69d0dffcddc7">

19. **Admin Panel Settings:**
    - Click on "Settings" and confirm the panel restart. Note the new URL for accessing the admin panel.
      <img width="1710" alt="Pasted Graphic 11" src="https://github.com/piephai/V2Ray/assets/65212311/3154ddbe-6ca8-43a0-8589-9358b804a90e">
      ![Pasted Graphic 12](https://github.com/piephai/V2Ray/assets/65212311/e1b672ac-c4a3-4a20-a64e-a300fd5cad88)


### Inbound Rules Configuration

20. **Preferred Language Setup:**
    - In your web browser settings, set "Chinese (Simplified)" as the preferred language for adding an inbound. Panel is a little buggy and you won't be able to add inbounds without doing this first.
      ![Pasted Graphic 14](https://github.com/piephai/V2Ray/assets/65212311/dd60e835-4281-426b-9143-5e274d180ee2)
      ![Pasted Graphic 16](https://github.com/piephai/V2Ray/assets/65212311/a3cb3267-11d7-4d0a-a7f2-7105db37a2d0)
      <img width="752" alt="Pasted Graphic 17" src="https://github.com/piephai/V2Ray/assets/65212311/8e413279-a59e-44e5-857e-d9c5fa218562">

21. **Add Inbound Rules:**
    - Refresh the admin panel and go to "Inbound" -> "Add inbound."
    - Use the settings for "VLESS + XTLS + uTLS + REALITY."
    - Set the remark to your hostname (Step 8) and port to "443." 
    - Toggle to enable "reality."

*Note: Don’t worry if your information below the “reality” row is different to the screenshot as those are automatically populated.*

![Pasted Graphic 21](https://github.com/piephai/V2Ray/assets/65212311/dd39e6c4-6f0a-4e45-a371-3010f4bfa189)

22. **Add a User:**
    - Click the "+" button next to "Add user" and select "xtls-rprx-vision" as the flow.
      ![Pasted Graphic 22](https://github.com/piephai/V2Ray/assets/65212311/bab08429-5cdc-41e4-b3a3-b2a022290228)

23. **Create the Inbound:**
    - Click "Add" at the bottom of the page to create your first inbound.
    <img width="1486" alt="Pasted Graphic 23" src="https://github.com/piephai/V2Ray/assets/65212311/fe644585-fc9f-4bc3-8454-85f2651ae9da">

24. **Update X-Ray:**
    - In the X-UI admin panel, switch to the newest version of X-Ray on the status page and click "Restart X-ray."
   ![Pasted Graphic 24](https://github.com/piephai/V2Ray/assets/65212311/58da2fee-8f1b-4fcd-b7f9-3ee445ba426a)

25. **Export Links:**
    - You can export links and share them with your users. They just need to paste the link into their V2ray client.
    ![Pasted Graphic 25](https://github.com/piephai/V2Ray/assets/65212311/eef2ebe3-8ce0-4d49-86ad-08a7f312b04a)


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

*Please note that specific instructions for the V2ray client may vary based on the client you choose.*
