# How to use a Pi-hole on a Huawei B535 router

## Raspberry Pi setup

1. You will need to have any supported operating system installed on your Raspberry Pi

2. Make all your software is updated by running:
   
   ```shell
      sudo apt update && sudo apt upgrade -y
   ```

3. Install the Pi-hole software onto the Raspberry Pi. Follow the prompts. Note down the details at the end of the installation.
   
   ```shell
   curl -sSL https://install.pi-hole.net | sudo bash
   ```

## Router setup

You can have two ways to use the pi-hole on a network: either by individually configuring every client device to use the pi-hole as the DNS, or by setting up the router to use the pi-hole for its DNS function. 

This guide will cover the second option because then any device that connects to the router will benefit from adblocking without any additional setup.

### Setting up a static IP address

1. Go to your router's configuration page (usually at 192.168.8.1). Note that some internet security suites like Bitdefender might show a warning for this page, but this is the only way to access the router settings.

2. Then go to Advanced -> Router -> DHCP -> IP and MAC Address Binding List

3. Note down the DHCP IP range, because we will need to give the Pi-hole an address outside of this range

4. Click on the plus sign, you will see this menu:
   
   ![static ip](https://github.com/Dafterfly/Pi-hole-info/assets/17124333/acaac3a8-df0b-4248-ba08-414926c319f7)

5. Fill in the IP address that falls outside of the range noted in step 3. 

6. Select your Pi-hole device from the device name dropdown menu, the MAC address will fill in automatically

7. Then click save
   
### Set a manual DNS

1. Scroll back up to Advanced -> Router -> DHCP

2. Open up your browser's developer tools. On Firefox it is with the F12 key.

3. In the Console, type the following and then press Enter:
   
   ```shell
   $('#dhcp_dns').show();
   ```

4. Tick the "Set DNS server manually" that comes up

5. You will see some new options come up
   
   ![dns server](https://github.com/Dafterfly/Pi-hole-info/assets/17124333/8fc78817-18ab-41f2-b194-6b6a7b2ce03a)

6. Fill in only the "Primary DNS server" field with the Static IP address given to the Pi-hole in the MAC Address Binding List

7. Note that you need to make sure on the pi-hole settings page, under Settings -> DNS -> Advanced DNS settings, make sure the following boxes are **unticked**: "Never forward non-FQDN `A` and `AAAA` queries" and "Never forward reverse lookups for private IP ranges".

 ![advanced dns settings](https://github.com/user-attachments/assets/b91e2ee5-2871-44c0-a8fd-3e0b4deb545a)

   The reason for this is because as the below the settings indicate:
   
   > Enabling these two options may increase your privacy, **but may also prevent you from being able to access local hostnames if the Pi-hole is not used as DHCP server.**
   
   As a consequence, if these boxes are ticked, you can't access the pi-hole using the domain name `pi.hole`.

   
### Force the router to only use IPv4 and use only the pi-hole for IPV4 DNS

1. Go to Network -> Mobile Network -> Internet Connection -> Profiles

2. Click on the plus sign

3. Give it a name that you will remember

4. Tick the  '"Set as Default Profile" box

5. Fill in "internet" for the APN

6. For IP Type select "IPv4" from the dropdown menu. Be sure to select the one that has IPv4 only

7. Once again, open up your browser's developer tools. On Firefox it is with the F12 key

8. In the Console, type the following and then press Enter:
   
   ```shell
         $('#apn_list_input_dns_operate').show();
         $('#profile_dns_status_table').show();
         $('#profile_ipv6_dns_status_table').show();
         $('#apn_select_blank').show();
   ```

9. You will see some new options
   
   ![ipv4 apn](https://github.com/Dafterfly/Pi-hole-info/assets/17124333/2dd9612f-abdb-440c-bb3a-92e3e73a2073)

10. Fill in only the "Primary IPv4 DNS server" with the IP address of the Pi-hole

11. Then click save

12. Restart your router
