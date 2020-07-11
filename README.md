# (Re)Take control of your backups at home with a Raspberry Pie 4

## Installation guide

1. [Requirements](#1-requirements)
    * [ISP requirements](#isp-requirements)
    * [Hardware requirements](#hardware-requirements)
2. [OS installation](#2-os-installation)
3. [Hardware installation](#3-hardware-installation)
4. [Initial Ubuntu setup](#4-initial-ubuntu-setup)
    * [Step 1: set up appropriate keyboard layout](#step-1-set-up-appropriate-keyboard-layout)
    * [Step 2: set up timezone](#step-2-set-up-timezone)
    * [Step 3: restart your machine to enable changes](#step-3-restart-your-machine-to-enable-changes)
    * [Step 4: allow root login](#step-4-allow-root-login)
    * [Step 5: change username, password and hostname](#step-5-change-username-password-and-hostname)
    * [Step 6: disallow root login](#step-6-disallow-root-login)
5. [Upgrade your system & enable automatic updates](#5-upgrade-your-system--enable-automatic-updates)
6. [Local network access](#6-local-network-access)
    * [Step 1: display the MAC address of your Pie connected network](#step-1-display-the-mac-address-of-your-pie-connected-network)
    * [Step 2: login to your router admin panel](#step-2-login-to-your-router-admin-panel)
    * [Step 3: register a static address](#step-3-register-a-static-address)
    * [Step 4: SSH access](#step-4-ssh-access)
7. [Remote network access](#7-remote-network-access)
    * [Step 1: set up port forwarding](#step-1-set-up-port-forwarding)
8. [Restrict SSH access](#8-restrict-ssh-access)
    * [Step 1: create an SSH key](#step-1-create-an-ssh-key)
    * [Step 2: add your public key to your machine's authorized keys](#step-2-add-your-public-key-to-your-machines-authorized-keys)
    * [Step 3: disallow SSH password authentication](#step-3-disallow-ssh-password-authentication)
    * [Step 4: keep alive SSH connections](#step-4-keep-alive-ssh-connections)
    * [Step 5: Change default SSH port](#step-5-change-default-ssh-port)

9. [Set up machine](#9-set-up-machine)
    * [Step 0: set up variables](#step-0-set-up-variables)
    * [Step 1: Postfix](#step-1-postfix)
    * [Step 2: Firewall](#step-2-firewall)
    * [Step 3: Fail2ban](#step-3-fail2ban)
10. [Configure hard drive](#10-configure-hard-drive)
    * [Step 1: check disk status](#step-1-check-disk-status)
    * [Step 2: create the filesystem](#step-2-create-the-filesystem)
    * [Step 3: create the mount point](#step-3-create-the-mount-point)
    * [Step 4: mount the filesystem](#step-4-mount-the-filesystem)
11. [Create a new backup access](#11-create-a-new-backup-access)
    * [Step 1: ask for username and generate password](#step-1-ask-for-username-and-generate-password)
    * [Step 2: create the user and put it into a jail](#step-2-create-the-user-and-put-it-into-a-jail)
    * [Step 3: enable access from your computer](#step-3-enable-access-from-your-computer)
    * [Step 4: enable access from the machine that will perform backups](#step-4-enable-access-from-the-machine-that-will-perform-backups
)

## 1. Requirements

### ISP requirements

[Back to top ↑](#installation-guide)

Your Internet Service Provider (ISP) must give you a static IP address.

In France, the ISP called "[Free](https://free.fr/assistance/54.html)"
matches this requirement.

### Hardware requirements

[Back to top ↑](#installation-guide)

* 1 × [Raspberry Pie 4 (4 GB RAM)](https://www.kubii.fr/les-cartes-raspberry-pi/2772-nouveau-raspberry-pi-4-modele-b-4gb-kubii-0765756931182.html)
* 1 × [Raspberry Pie 4 case](https://www.kubii.fr/boitiers-et-supports/2681-boitier-officiel-pour-raspberry-pi-4-kubii-3272496298583.html)
* 1 x [Raspberry Pie 4 power supply](https://www.kubii.fr/14-chargeurs-alimentations-raspberry/2678-alimentation-officielle-153w-usb-c-pour-raspberry-pi-4-kubii-3272496300002.html)
* 1 x [SanDisk microSD card 16 Go class 10](https://www.kubii.fr/raspberry-pi-microbit/2587-carte-micro-sd-sandisk-16go-classe10-taux-de-transfert-80mb-kubii-619659161613.html)
* 1 × [Toshiba N300 4 To Hard Drive](https://www.ldlc.com/fiche/PB00259091.html)
* 1 × [Ugreen USB 3.0 external case 50422 for 3,5 inch HDD](https://www.amazon.fr/UGREEN-Bo%C3%AEtier-Externe-Compatible-Alimentation/dp/B076WS2WJ6)
* 1 × [Ugreen ethernet cable Cat 7 10Gbps](https://www.amazon.fr/UGREEN-11260-Ethernet-Nintendo-Consoles/dp/B00QV1F1C4)
* 1 × [Ugreen USB 3.0 SD card reader 30333](https://www.amazon.fr/UGREEN-Lecteur-M%C3%A9moire-CompactFlash-Compatible/dp/B01ANDA8GE/)
(optional if you already have a SD card reader)
* 1 × [Ugreen micro HDMI to HDMI adapter](https://www.amazon.fr/UGREEN-Femelle-Adaptateur-Supporte-Ethernet/dp/B00B2HORKE/)
* 1 × [Ugreen HDMI cable 0,9 m](https://www.amazon.fr/UGREEN-Ethernet-18Gbps-Supporte-Compatible/dp/B07DBYDJQF/)
* 1 × keyboard
* 1 × screen

## 2. OS installation

[Back to top ↑](#installation-guide)

1. Download the [Ubuntu 18.04 64 bits image](https://ubuntu.com/download/raspberry-pi/thank-you?version=18.04.4&architecture=arm64+raspi3)
for Raspberry Pie 4.
2. Put your microSD card in your SD card reader and connect it to your computer.
3. Follow [instructions](https://ubuntu.com/download/raspberry-pi/thank-you)
in order to flash the downloaded image onto the microSD card.
4. Disconnect everything when the process is finished.

## 3. Hardware installation

[Back to top ↑](#installation-guide)

1. Put your microSD card containing the installed OS in your Raspberry Pie.
2. Put your Raspberry Pie into its case.
3. Put your HDD into its USB 3.0 case.
4. Connect your Raspberry Pie to your router with the ehernet cable.
5. Connect your drive to your Raspberry Pie with its USB cable.
6. Connect your keyboard and screen to your Raspberry Pie.
7. Connect the power adaptators of your drive, Rasberry Pie and screen.

Your Ubuntu machine will boot up!

## 4. Initial Ubuntu setup

[Back to top ↑](#installation-guide)

You can login with "ubuntu" as default login and password. You may
experienced login errors if you try to login directly as soon as the
prompt is displayed. This is because some background installations
processes are not completed yet. Wait until SSH keys are displayed on
the screen then press "Enter". You will be prompted to change your
password immediately after login.

*Note: Ubuntu 18.04 for Raspberry Pie 4 is by default using a "qwerty"
keyboard layout which might not be your layout. To prevent loosing access
to your account, I suggest you to set up something universal like
"hellohello" for now, set up appropriate keyboard layout and change
the password later.*

### Step 1: set up appropriate keyboard layout

[Back to top ↑](#installation-guide)

```bash
sudo dpkg-reconfigure keyboard-configuration
```

### Step 2: set up timezone

[Back to top ↑](#installation-guide)

```bash
sudo timedatectl set-timezone Europe/Paris
```

### Step 3: restart your machine to enable changes

[Back to top ↑](#installation-guide)

```bash
sudo reboot
```

### Step 4: allow root login

[Back to top ↑](#installation-guide)

Because you might want something more personal than "ubuntu" as a
username and hostname, you can change them. We will need the
root account for that so we will temporary allow root login:

```bash
sudo passwd root
logout
```

### Step 5: change username, password and hostname

[Back to top ↑](#installation-guide)

Login as root and use these commands to rename your username,
change your password and your hostname to something more meaningful to you:

```bash
# Change username
usermod -l <newUserName> ubuntu

# Rename home directory
usermod -d /home/<newUserName> -m <newUserName>

# Change password
passwd <newUserName>

# Change hostname (must be a domain name pointing to this machine IP address)
hostnamectl set-hostname <newHostname>
```

### Step 6: disallow root login

[Back to top ↑](#installation-guide)

When it's done, you can disallow root login. For security reasons,
you should never leave your root account accessible.

```bash
# Disable root account
passwd -l root

# Reboot to apply changes
reboot
```

## 5. Upgrade your system & enable automatic updates

[Back to top ↑](#installation-guide)

Upgrading the system will ensure that all your softwares are
using latest security fixes.

```bash
sudo apt update && sudo apt dist-upgrade -y
```

Then, we'll enable automatic updates to be sure that all
futures security fixes are installed as soon are they are released:

<!-- markdownlint-disable MD013 -->
```bash
# Make a backup of the config files
sudo cp /etc/apt/apt.conf.d/10periodic /etc/apt/apt.conf.d/.10periodic.backup
sudo cp /etc/apt/apt.conf.d/50unattended-upgrades /etc/apt/apt.conf.d/.50unattended-upgrades.backup

# Download updates when available
sudo sed -i'.tmp' -e 's,APT::Periodic::Download-Upgradeable-Packages "0";,APT::Periodic::Download-Upgradeable-Packages "1";,g' /etc/apt/apt.conf.d/10periodic

# Clean apt cache every week
sudo sed -i'.tmp' -e 's,APT::Periodic::AutocleanInterval "0";,APT::Periodic::AutocleanInterval "7";,g' /etc/apt/apt.conf.d/10periodic

# Enable automatic updates once downloaded
sudo sed -i'.tmp' -e 's,//\s"${distro_id}:${distro_codename}-updates";,        "${distro_id}:${distro_codename}-updates";,g' /etc/apt/apt.conf.d/50unattended-upgrades

# Ask for email
read -r -p 'Enter your email for notifications on update errors: ' email

# Enable email notifications
sudo sed -i'.tmp' -e "s,//Unattended-Upgrade::Mail \"root\";,Unattended-Upgrade::Mail \"${email}\";,g" /etc/apt/apt.conf.d/50unattended-upgrades

# Enable email notifications only on failures
sudo sed -i'.tmp' -e 's,//Unattended-Upgrade::MailOnlyOnError "true";,Unattended-Upgrade::MailOnlyOnError "true";,g' /etc/apt/apt.conf.d/50unattended-upgrades

# Remove unused kernel packages when needed
sudo sed -i'.tmp' -e 's,//Unattended-Upgrade::Remove-Unused-Kernel-Packages "false";,Unattended-Upgrade::Remove-Unused-Kernel-Packages "true";,g' /etc/apt/apt.conf.d/50unattended-upgrades

# Remove unused dependencies when needed
sudo sed -i'.tmp' -e 's,//Unattended-Upgrade::Remove-Unused-Dependencies "false";,Unattended-Upgrade::Remove-Unused-Dependencies "true";,g' /etc/apt/apt.conf.d/50unattended-upgrades

# Reboot when needed
sudo sed -i'.tmp' -e 's,//Unattended-Upgrade::Automatic-Reboot "false";,Unattended-Upgrade::Automatic-Reboot "true";,g' /etc/apt/apt.conf.d/50unattended-upgrades

# Set reboot time to 5 AM
sudo sed -i'.tmp' -e 's,//Unattended-Upgrade::Automatic-Reboot-Time "02:00";,Unattended-Upgrade::Automatic-Reboot-Time "05:00";,g' /etc/apt/apt.conf.d/50unattended-upgrades

# Remove temporary files
sudo rm /etc/apt/apt.conf.d/10periodic.tmp
sudo rm /etc/apt/apt.conf.d/50unattended-upgrades.tmp
```
<!-- markdownlint-enable MD013 -->

## 6. Local network access

[Back to top ↑](#installation-guide)

If you want to access your machine from another computer on your local
network instead of directly with a keyboard and a screen, you'll need
to reserve a static IP address for it. If not, the attributed IP address
inside your network will change each time your router starts up, so it's quite annoying.

### Step 1: display the MAC address of your Pie connected network

[Back to top ↑](#installation-guide)

```bash
ifconfig | grep -i ether
```

### Step 2: login to your router admin panel

[Back to top ↑](#installation-guide)

Login to your router according to your ISP and/or router documentation.

*Note: for the "Free" ISP, the URL of the admin panel is: [https://subscribe.free.fr/login/](https://subscribe.free.fr/login/).*

### Step 3: register a static address

[Back to top ↑](#installation-guide)

Register the static IP address according to your ISP and/or router documentation.

The IP address you choose must not be in the DHCP server range.
You can start with something like "192.168.0.101".

*Note: for the "Free" ISP, once logged in, go under
"Ma Freebox" > "Paramétrer mon routeur Freebox" > "Redirections / Baux DHCP"
and fill the form like bellow.*

![register-static-ip](https://user-images.githubusercontent.com/6952638/76153321-a0767700-60ca-11ea-8816-c548047064e4.png)

### Step 4: SSH access

[Back to top ↑](#installation-guide)

With this, you should now be able to access your Raspberry Pie from
your computer (which must be connected to the same network as your Pie)
through SSH with this command:

```bash
ssh <yourUserName>@<yourIpAddress>
```

## 7. Remote network access

### Step 1: set up port forwarding

[Back to top ↑](#installation-guide)

For now, your router is the target of all requests made to your public
IP address, and it does not do anything with them.

We need to instruct it to redirect the traffic to the Pie so that we can
access it from outside the local network, from the Internet.

According to your ISP/router documentation, redirect the traffic from
port 22.

*Note: for the "Free" ISP, once logged in, go under
"Ma Freebox" > "Paramétrer mon routeur Freebox" > "Redirections / Baux DHCP"
and fill the form like bellow.*

![port-forwarding](https://user-images.githubusercontent.com/6952638/84016511-aefc5500-a97d-11ea-8481-90ef054f9932.png)

## 8. Restrict SSH access

[Back to top ↑](#installation-guide)

The root account is disabled but now, anybody can potentially access
your machine through your user account if they found your password.

Your user account is not root but have some sudo privileges. So if it's
compromised, an attacker can do pretty much everything he want with your
machine, including accessing your datas.

To protect your account from being accessed by another person that you,
we will disable SSH password authentication and only let your authorized
computers to login with your user account (note that this will not
disable password authentication direcly with a keyboard and a screen connected).

On each computer you want to access your Raspberry Pie with, follow these steps:

### Step 1: create an SSH key

[Back to top ↑](#installation-guide)

If you don't have an SSH key (look for "`~/.ssh/id_rsa`" and
"`~/.ssh/id_rsa.pub`" files), use this command to generate one:

```bash
ssh-keygen -t rsa -b 4096 -N '' -f ~/.ssh/id_rsa
```

### Step 2: add your public key to your machine's authorized keys

[Back to top ↑](#installation-guide)

From your computer, run:

<!-- markdownlint-disable MD013 -->
```bash
ssh <yourUserName>@<yourIpAddress> "echo '$(cat ~/.ssh/id_rsa.pub)' | tee -a ~/.ssh/authorized_keys > /dev/null && chmod 400 ~/.ssh/id_rsa*"
```
<!-- markdownlint-enable -->

If you try to reconnect to your machine through SSH, you should now be
able to login without being asked for a password. SSH will automatically
log you if your local SSH key matches one indicated in the remote
"~/.ssh/authorized_keys" file.

### Step 3: disallow SSH password authentication

[Back to top ↑](#installation-guide)

Now that you have an passwordless SSH access to your Raspberry Pie,
we will disallow password authentication. This will prevent all non
authorized computers from being able to access it through SSH.

I recommend you to backup your "~/.ssh/id_rsa" and "~/.ssh/id_rsa.pub"
files in a safe place, for example in a password manager app protected
by a master password.

This will prevent you from loosing access to your Pie if your only
authorized computer dies (in that case, you only have to copy these
files in your next computer to allow connections from it).

To disable SSH password authentication, connect to your Pie and run:

<!-- markdownlint-disable MD013 -->
```bash
# Update the config and save the original in a "/etc/ssh/sshd_config.backup" file
sudo sed -i'.backup' -e 's/PasswordAuthentication yes/PasswordAuthentication no/g' /etc/ssh/sshd_config

# Restart SSH
sudo service ssh restart
```
<!-- markdownlint-enable -->

### Step 4: keep alive SSH connections

[Back to top ↑](#installation-guide)

This will prevent SSH connections to disconnect prematurely.

```bash
# Keep alive client connections
echo "
ClientAliveInterval 120
ClientAliveCountMax 3" | sudo tee -a /etc/ssh/sshd_config > /dev/null

# Restart SSH
sudo service ssh restart
```

### Step 5: Change default SSH port

[Back to top ↑](#installation-guide)

If the default SSH port is available, this will make an eventual attackers task harder.

```bash
sudo sed -i'.backup' -e 's/#Port 22/Port 3022/g' /etc/ssh/sshd_config

# Restart SSH
sudo service ssh restart
```

## 9. Set up machine

### Step 0: set up variables

[Back to top ↑](#installation-guide)

<!-- markdownlint-disable MD013 -->
```bash
# Ask email if not already set
if [[ -z "${email}" ]]; then
    read -r -p "Enter your email (needed to set up email monitoring): " email
fi

# Ask hostname if not already set
if [[ -z "${hostname}" ]]; then
    read -r -p "Enter your hostname (it must be a domain name pointing to this machine IP address): " hostname
fi

# Ask SMTP hostname if not already set
if [[ -z "${smtphostname}" ]]; then
    read -r -p "Enter your remote SMTP server hostname: " smtphostname
fi

# Ask SMTP port if not already set
if [[ -z "${smtpport}" ]]; then
    read -r -p "Enter your remote SMTP server port: " smtpport
fi

# Ask SMTP username if not already set
if [[ -z "${smtpusername}" ]]; then
    read -r -p "Enter your remote SMTP server username: " smtpusername
fi

# Ask SMTP username if not already set
if [[ -z "${smtppassword}" ]]; then
    read -r -p "Enter your SMTP password: " smtppassword
fi
```
<!-- markdownlint enable -->

### Step 1: Postfix

[Back to top ↑](#installation-guide)

We've set up email notifications on updates errors but
we need an SMTP server in order to actually be able to send emails.

<!-- markdownlint-disable MD013 -->
```bash
# Install
sudo DEBIAN_FRONTEND=noninteractive apt install -y postfix mailutils

# Make a backup of the config files
sudo cp /etc/postfix/main.cf /etc/postfix/.main.cf.backup
sudo cp /etc/aliases /etc/.aliases.backup

# Update main config file
echo "smtpd_relay_restrictions = permit_mynetworks permit_sasl_authenticated defer_unauth_destination
myhostname = ${hostname}
relayhost = [${smtphostname}]:${smtpport}
alias_maps = hash:/etc/aliases
alias_database = hash:/etc/aliases
mailbox_size_limit = 0
recipient_delimiter = +
inet_interfaces = all
inet_protocols = ipv4
smtp_sasl_auth_enable = yes
smtp_sasl_security_options = noanonymous
smtp_sasl_password_maps = hash:/etc/postfix/sasl_passwd
smtp_use_tls = yes
smtp_tls_CAfile = /etc/ssl/certs/ca-certificates.crt
sender_canonical_classes = envelope_sender, header_sender
sender_canonical_maps =  regexp:/etc/postfix/sender_canonical_maps
smtp_header_checks = regexp:/etc/postfix/header_check" | sudo tee -a /etc/postfix/main.cf > /dev/null

# Save SMTP credentials
echo "[${smtphostname}]:${smtpport} ${smtpusername}:${smtppassword}" | sudo tee /etc/postfix/sasl_passwd > /dev/null
sudo postmap /etc/postfix/sasl_passwd
sudo chown root:root /etc/postfix/sasl_passwd /etc/postfix/sasl_passwd.db
sudo chmod 0600 /etc/postfix/sasl_passwd /etc/postfix/sasl_passwd.db

# Remap sender address
echo "/.+/    ${smtpusername}" | sudo tee /etc/postfix/sender_canonical_maps > /dev/null
echo "/From:.*/ REPLACE From: ${smtpusername}" | sudo tee /etc/postfix/header_check > /dev/null
sudo postmap /etc/postfix/sender_canonical_maps
sudo postmap /etc/postfix/header_check

# Forwarding System Mail to your email address
echo "root:     ${email}" | sudo tee -a /etc/aliases > /dev/null

# Enable aliases
sudo newaliases

# Restart Postfix
sudo service postfix restart
```
<!-- markdownlint-enable -->

### Step 2: Firewall

[Back to top ↑](#installation-guide)

We will enable Ubuntu firewall in order to prevent remote access to our machine.
We will only allow SSH (for remote SSH access) and Postfix
(for emails sent to the postmaster address).
**Careful, you need to allow SSH before enabling the
firewall, if not, you may lose access to your machine.**

```bash
# Add rules and activate firewall
sudo ufw allow 3022
echo 'y' | sudo ufw enable
```

### Step 3: Fail2ban

[Back to top ↑](#installation-guide)

Preventing remote access from others sotwares than SSH and Postfix in not
enough. We are still vulnerable to brute-force attacks through these services.
We will use Fail2ban to protect us.

```bash
# Install
sudo apt install -y fail2ban

# Add default configuration
echo "[DEFAULT]
findtime = 3600
bantime = 86400
destemail = ${email}
action = %(action_mwl)s" | sudo tee /etc/fail2ban/jail.local > /dev/null

echo "
[sshd]
enabled = true
port = ssh
filter = sshd
logpath = /var/log/auth.log
maxretry = 3" | sudo tee -a /etc/fail2ban/jail.local > /dev/null

# Restart Fail2ban
sudo service fail2ban restart
```

## 10. Configure hard drive

### Step 1: check disk status

[Back to top ↑](#installation-guide)

Check available disks with:

```bash
lsblk -o NAME,SIZE,FSTYPE,TYPE,MOUNTPOINT
```

You should see this:

```text
NAME         SIZE FSTYPE TYPE MOUNTPOINT
sda          3.7T        disk
mmcblk0     14.9G        disk
├─mmcblk0p1  256M vfat   part /boot/firmware
└─mmcblk0p2 14.6G ext4   part /
```

### Step 2: create the filesystem

[Back to top ↑](#installation-guide)

```bash
sudo mkfs.ext4 -F /dev/sda
```

### Step 3: create the mount point

[Back to top ↑](#installation-guide)

```bash
sudo mkdir /home/jails
```

### Step 4: mount the filesystem

[Back to top ↑](#installation-guide)

```bash
# Mount the disk now
sudo mount /dev/sda /home/jails

# Make the mount permanent after reboot
echo "/dev/sda /home/jails ext4 defaults 0 1" | sudo tee -a /etc/fstab > /dev/null
```

## 11. Create a new backup access

### Step 1: ask for username and generate password

[Back to top ↑](#installation-guide)

```bash
# Ask for username
read -r -p 'Enter the new username: ' newusername

# Generate a new password
newpassword=$(openssl rand -hex 15)
```

### Step 2: create the user and put it into a jail

[Back to top ↑](#installation-guide)

<!-- markdownlint-disable MD013 -->
```bash
username=${newusername} password=${newpassword} use_basic_commands=n bash -c "$(wget --no-cache -O- https://raw.githubusercontent.com/RomainFallet/chroot-jail/master/create.sh)"
```
<!-- markdownlint-enable -->

### Step 3: enable access from your computer

[Back to top ↑](#installation-guide)

```bash
# Create SSH folder in the user home
sudo mkdir -p "/home/${newusername}/.ssh"

# Set up permissions
sudo chmod 700 "/home/${newusername}/.ssh"

# Copy the authorized_keys file to enable passwordless SSH connections
sudo cp ~/.ssh/authorized_keys "/home/${newusername}/.ssh/authorized_keys"

# Set up permissions
sudo chmod 644 "/home/${newusername}/.ssh/authorized_keys"

# Give ownership to the user
sudo chown -R "${newusername}:${newusername}" "/home/${newusername}/.ssh"
```

**Note: you actually don't need to know the password because we disabled SSH
password authentication and didn't give sudo privileges to this user.**

### Step 4: enable access from the machine that will perform backups

[Back to top ↑](#installation-guide)

Login to the user of the machine that will  perform backups, then use:

<!-- markdownlint-disable MD013 -->
```bash
# Ensure SSH keys exists
ssh-keygen -t rsa -b 4096 -N '' -f ~/.ssh/id_rsa

# Ensure SSH keys permissions are OK
chmod 400 ~/.ssh/id_rsa*
```
<!-- markdownlint-enable -->

Then, copy the content of the `~/.ssh/id_rsa.pub` file
in the `~/.ssh/authorized_keys` file of the user
you've just created on the backup machine.

You will be able to login without password like this:

```bash
ssh <newusername>@<backupHostname>
```
