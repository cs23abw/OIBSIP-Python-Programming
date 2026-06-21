# Basic Firewall Configuration with UFW

## Project Overview

This task was completed as part of the Oasis Infobyte Cyber Security Internship.

The objective of this task is to configure a basic firewall on an Ubuntu Linux system using UFW, which stands for Uncomplicated Firewall. The firewall was configured to allow SSH traffic and deny HTTP traffic.

This task was completed in an Ubuntu VirtualBox virtual machine.

## Tool Used

* Ubuntu Linux
* UFW (Uncomplicated Firewall)
* Terminal

## What is UFW?

UFW is a simple firewall tool used on Linux systems. A firewall controls network traffic by deciding what should be allowed or blocked.

In simple terms, a firewall works like a security gate:

* Allowed traffic can pass through.
* Denied traffic is blocked.
* Unnecessary open access can be reduced.

## Commands Used

```bash
sudo ufw status verbose
sudo ufw allow ssh
sudo ufw deny http
sudo ufw enable
sudo ufw status verbose
```

## Explanation of the Commands

### Check UFW Status

```bash
sudo ufw status verbose
```

This command checks whether UFW is active or inactive and shows existing firewall rules.

Before configuration, the firewall status was:

```text
Status: inactive
```

This means UFW was installed but not yet enabled.

### Allow SSH

```bash
sudo ufw allow ssh
```

This command allows SSH traffic.

SSH usually uses port `22/tcp`. It is commonly used for secure remote access and administration.

### Deny HTTP

```bash
sudo ufw deny http
```

This command denies HTTP traffic.

HTTP usually uses port `80/tcp`. HTTP is unencrypted, so blocking it can reduce unnecessary exposure if the system is not meant to host a web server.

### Enable UFW

```bash
sudo ufw enable
```

This command turns on the firewall.

After enabling UFW, the firewall became active and started applying the configured rules.

## Firewall Status After Configuration

After configuring UFW, the final firewall status showed:

```text
Status: active

To                         Action      From
--                         ------      ----
22/tcp                     ALLOW IN    Anywhere
80/tcp                     DENY IN     Anywhere
22/tcp (v6)                ALLOW IN    Anywhere (v6)
80/tcp (v6)                DENY IN     Anywhere (v6)
```

## Security Explanation

The firewall was configured to allow SSH and deny HTTP.

Allowing SSH is useful because SSH is used for secure remote administration. However, SSH should still be protected with strong passwords, secure keys, and restricted access where possible.

Denying HTTP blocks unencrypted web traffic on port 80. This is useful when the system is not intended to run a normal web server.

The final configuration also shows IPv6 rules. These were automatically added by UFW, which means the same allow and deny rules were applied for IPv6 traffic.

## Files Included

```text
Basic Firewall Configuration with UFW/
├── ufw_configuration.sh
├── README.md
└── screenshots/
    ├── ufw-version.png
    ├── ufw-before-configuration.png
    └── ufw-status-after-configuration.png
```

## Screenshot Evidence

The screenshots folder contains evidence of:

* UFW version check
* UFW status before configuration
* UFW status after firewall rules were applied

The most important screenshot is:

```text
ufw-status-after-configuration.png
```

This screenshot shows that UFW is active and that SSH is allowed while HTTP is denied.

## What I Learned

Through this task, I learned how to:

* Check whether UFW is installed
* Check the current firewall status
* Allow SSH traffic using UFW
* Deny HTTP traffic using UFW
* Enable the firewall
* Read firewall rules
* Understand the meaning of allowed and denied ports
* Document firewall configuration for a cyber security task

## Conclusion

The UFW firewall was successfully configured on Ubuntu.

SSH traffic was allowed, HTTP traffic was denied, and the firewall was enabled successfully. This task helped me understand how basic firewall rules can improve system security by controlling access to network services.

## Author

Chukwukaima Sam
