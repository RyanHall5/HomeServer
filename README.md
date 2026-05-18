# Personal Linux Server - Private Cloud + Secure Remote Access

Self-Hosted Linux server providing private cloud storage through NextCloud, with secure remote access via TailScale VPN meshes. Built for two primary purposes: Initially, to learn networking, Linux administration, ssh, and self-hosted infrastructure development. Secondly, to serve as a private, free, large storage file sharing and backup system for myself, family, and friends. 

Why Does this project exist?

Problems this project addresses: 
1. Like me, you may find yourself getting these notifications: "there is not enough iCloud storage available",  "Storage is full. You can't back up photos or videos, and Gmail and Drive are affected", or any kind of full storage notification. I don't want to delete old photos/videos since they hold sentimental values. So it feels like my only choice is to upgrade my storage plan for some annual fee.
3. I have an iphone, my mother has an android, and often, when she sends me videos from her phone via text, the quality is just terrible. The only way we have found to share media reliably without corrupting quality, is via shared google photos, which takes up a lot of storage.

How this project solves those problems:
1. By making a one time purchase of a large physical storage device, you have access to much more storage space than the allocated amounts from apple, google, etc without any of the recurring fees. Google's default storage amounts is a mere 15GB, whereas you can find a new or used 1TB+ external hard drive for pretty cheap.
2. Large external storage drives provide an abundance of space for backing up phones, laptops, desktops, projects, etc. This can be especially helpful if you are in a field like me (Engineering Student), and often find yourself with software, applications, and projects that take up a large amount of storage. 
3. Nextcloud's free filesharing system removes the quality deprication from sharing media between operating systems via messages, since it is a dropbox style software that doesn't depend on the operating system of users. Your storage in Nextcloud is tied directly to your physical drive, Nextcloud is merely a way to access it.

What technologies were used?

Hardware:
1. Dell Optiplex 3060 micro (hosting linux server)
2. 14TB Western Digital External Hard Drive (a storage device this large is not necessary, I just had one spare)
3. 8GB+ Portable USB Drive (Installing Ubuntu on server)
4. Simple USB-A Keyboard + Mouse (For setting up server before ssh is configured)
5. HDMI Cord + Screen (For setting up server before ssh is configured)
6. Ethernet Cord (Internet connection for server)

Software:
1. Rufus (Formatting boot drive)
2. Ubuntu (OS running on the server)
3. OpenSSH (allows remote access to server through ssh)
4. Tailscale (creates vpn meshes to ensure secure ssh connection)
5. NextCloud (filesystem)
6. Docker (container system)
7. google-authenticator (optional server security)

Challenges / Debugging

Remote Access Configuration (Current):
I tried to setup remote access to be more friendly to non-technical people such as my family members by using Cloudflare tunneling but couldn't find a way to it without paying a recurring fee for a domain, which would defeat the purpose of the project so I decided to the connection method as installing tailscale. In the future I'll be looking more at HTTPS proxies, Nginx, and DuckDNS to try and host this service without requiring tailscale installation from users. 

Ubuntu installation via bootdrive (resolved):
For a while I was having trouble removing windows from the Optiplex and installing Ubuntu via the boot drive. I would get the installer to run full, and it would say the installation was complete, but upon restart I was hit with a "not bootable device" error. Ultimately this problem was resolved by me moving the USB bootdrive to a port in the back of the Optiplex, rather than the front. From what I understand, this error occurred because front ports can be unreliable for OS installation due to them being connected to the motherboard via internal cables, whereas back ports are wired directly to the motherboard. 

Google Authenticator ssh Lockout (resolved):
While installing and setting up google authenticator to my server, I accidentally broke ssh entirely and wasn't able to connect to the server from my laptop. I had to return to the headless served with KBM + a monitor to log in to the server physically. I fixed ssh by commenting out my changes in the sshd and sshd_config files. I stayed physically connected to the server, debugging my password + security code login until it was reliably working. The main issue was that KbdInteractiveAuthentication was incorrectly set to 'No' in the sshd_config file. 







