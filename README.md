# Personal Linux Server - Private Cloud + Secure Remote Access

Self-Hosted Linux server providing private cloud storage through NextCloud, with secure remote access via TailScale VPN meshes. Built for two primary purposes: Initially, to learn networking, Linux administration, ssh, and self-hosted infrastructure development. Secondly, to serve as a private, free, large storage file sharing and backup system for myself, family, and friends.

<br>

---

<br>

## Why does this project exist?

### Problems addressed by project:

1. Like me, you may find yourself getting these notifications: "there is not enough iCloud storage available", "Storage is full. You can't back up photos or videos, and Gmail and Drive are affected", or any kind of full storage notification. I don't want to delete old photos/videos since they hold sentimental values. So it feels like my only choice is to upgrade my storage plan, but what if I don't want to upgrade?

2. I have an iphone, my mother has an android, and often, when she sends me videos from her phone via text, the quality is just terrible. The only way we have found to share media reliably without corrupting quality, is via shared google photos, which takes up a lot of storage.

<br>

### How this project solves these problems:

1. By making a one time purchase of a large physical storage device, you have access to much more storage space than the allocated amounts from apple, google, etc. Google's default storage amounts is a mere 15GB, whereas you can find a new or used 1TB+ external hard drive for pretty cheap.

2. Large external storage drives provide an abundance of space for backing up phones, laptops, desktops, projects, etc. This can be especially helpful if you are in a field like me (Engineering Student), and often find yourself with software, applications, and projects that take up a large amount of storage.

3. Nextcloud's free filesharing system removes the quality deprication from sharing media between operating systems via messages, since it is a dropbox style software that doesn't depend on the operating system of users. Your storage in Nextcloud is tied directly to your physical drive, Nextcloud is merely a way to access it.

<br>

---

<br>

## Architecture (Needs Improvements)

The currently architecture of the project flows like this:

#### Admin Flow

```text
My personal device
        ↓
tailscale VPN mesh
        ↓
SSH
        ↓
Google Auth + Password Protected
        ↓
Server
```

#### User Flow

```text
User personal device
        ↓
Cloudflare tunnel via browser
        ↓
Server
        ↓
Docker Network
        ↓
Nextcloud Container
        ↓
Database
```

<br>

---

<br>

## What technologies were used?

### Hardware:

1. Dell Optiplex 3060 micro (hosting linux server)

2. 14TB Western Digital External Hard Drive (a storage device this large is not necessary, I just had one spare)

3. 8GB+ Portable USB Drive (Installing Ubuntu on server)

4. Simple USB-A Keyboard + Mouse (For setting up server before ssh is configured)

5. HDMI Cord + Screen (For setting up server before ssh is configured)

6. Ethernet Cord (Internet connection for server)

### Software:

1. Rufus (Formatting boot drive)

2. Ubuntu (OS running on the server)

3. OpenSSH (allows remote access to server through ssh)

4. Tailscale (creates vpn meshes to ensure secure ssh connection)

5. NextCloud (filesystem)

6. Cloudflare (secure connection)

7. Docker (container system)

8. google-authenticator (optional server security)

<br>

---

<br>

## Challenges / Debugging

### Remote Access Configuration (resolved):

Initially I had the server setup with tailscale connecting users to te server via their private vpn meshes, but this wasn't practical for non-technical users, and required a lot of overhead for adding new users. To resolve this issue, I purchased a cheap domain from Cloudflare for 4$/yr so that I could setup a Cloudflare tunnel to the server to ensure secure and easy access for non-technical users. Now, users are able to just type in the given url to their browsers, enter their nextcloud credentials, and they are good to go. In the future I'll be looking more at HTTPS proxies, Nginx, and DuckDNS to try and host this service for free without requiring tailscale installation from users.

<br>

### Ubuntu installation via bootdrive (resolved):

For a while I was having trouble removing windows from the Optiplex and installing Ubuntu via the boot drive. I would get the installer to run full, and it would say the installation was complete, but upon restart I was hit with a "not bootable device" error. Ultimately this problem was resolved by me moving the USB bootdrive to a port in the back of the Optiplex, rather than the front. From what I understand, this error occurred because front ports can be unreliable for OS installation due to them being connected to the motherboard via internal cables, whereas back ports are wired directly to the motherboard.

<br>

### Google Authenticator ssh Lockout (resolved):

While installing and setting up google authenticator to my server, I accidentally broke ssh entirely and wasn't able to connect to the server from my laptop. I had to return to the headless served with KBM + a monitor to log in to the server physically. I fixed ssh by commenting out my changes in the sshd and sshd_config files. I stayed physically connected to the server, debugging my password + security code login until it was reliably working. The main issue was that KbdInteractiveAuthentication was incorrectly set to 'No' in the sshd_config file.

<br>

---

<br>

## Potential Future Improvements

### Company/Business section:

Currently, the project is setup in 4 primary partitions, a shared section for family storage, friend storage, guest/temporary activity, and my personal storage. My primary storage takes up the vast majority of the drive since it is 14TB. My family also owns/operates a small business, and we are in the process of trying to grow that business through outreach. I am going to make a 5th partition of the drive for business related files. Images of products, events, CAD files, documentation, filings, contact lists, anything of that nature so we all have access to everything.

<br>

### HTTPS proxy in place of cloudflare:

As mentioned in the challenges section, currently to use the project, you have to either download and setup both tailscale and the nextcloud app, or pay for a domain to get a cloudflare tunnel working. I would like to setup HTTPS proxies to securely open my server to the internet so that my users don't have to download tailscail for secure vpn connections and anyone replicating the project doesn't have to pay recurring fees.
