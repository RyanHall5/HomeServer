# Server Setup Command Reference

A running list of commands used during setup and what each one does.

---

## Networking

```bash
ip a
```

Shows all network interfaces and IP addresses.

```bash
hostname -I
```

Shows current IPv4 address(es).

```bash
ip -4 a
```

Shows only IPv4 network information.

---

## SSH

```powershell
ls ~/.ssh
```

Lists local SSH keys.

```powershell
cat ~/.ssh/id_ed25519.pub
```

Displays public SSH key.

```powershell
ssh username@100.x.x.x
```

Connects to server remotely through SSH.

---

## Tailscale

```bash
curl -fsSL https://tailscale.com/install.sh | sh
```

Downloads and installs Tailscale.

```bash
sudo tailscale up
```

Authenticates and connects device to tailnet.

```bash
tailscale ip -4
```

Shows device Tailscale IP.

```bash
tailscale status
```

Displays connected devices and status.

---

## Storage

```bash
lsblk
```

Lists connected drives and partitions.

```bash
sudo blkid
```

Displays filesystem type and UUID information.

```bash
sudo mkdir -p /mnt/storage
```

Creates storage mount folder.

```bash
sudo mount /dev/sdb1 /mnt/storage
```

Mounts drive to Linux filesystem.

```bash
df -h
```

Displays mounted drives and capacity usage.

---

## Permissions

```bash
ls -ld /mnt/storage
```

Shows ownership and permissions of storage folder.

```bash
whoami
```

Shows current logged-in user.

```bash
sudo chown -R username:username /mnt/storage
```

Changes ownership of storage directory.

```bash
chmod -R u+rwX /mnt/storage
```

Adds read/write permissions.

---

## File Transfer

```bash
mkdir -p /mnt/storage/{backups,files,projects,media}
```

Creates organized storage folders.

```powershell
scp "localfile" username@server:/mnt/storage/folder/
```

Uploads files from laptop to server.

```bash
ls -l /mnt/storage/folder
```

Lists files in directory.

```bash
file filename.png
```

Displays file type information.

---

## Samba Network Drive

```bash
sudo apt install samba -y
```

Installs Samba file sharing service.

```bash
sudo nano /etc/samba/smb.conf
```

Edits Samba configuration.

```bash
sudo smbpasswd -a username
```

Creates Samba login credentials.

```bash
sudo systemctl restart smbd
```

Restarts Samba after configuration changes.

Windows access:

```text
\\optiplex\Storage
```

Opens shared drive in File Explorer.
