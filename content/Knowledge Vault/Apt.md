---
created: 2025-10-27T15:39
updated: 2025-10-27T15:40
title: "Linux Packages Manager: apt vs apt-get"
tags:
  - SoftwareHacks
---
# Apt vs Apt-Get

The difference between *apt* and *apt-get* is not just that *apt* is a newer version of *apt-get*. The *apt* command was designed as a more user-friendly alternative to *apt-get*, combining the functionality of multiple package management tools for user convenience.

---

# Update package database

Update package database brings newer packages available.

```cmd
sudo apt update
```

---
# Upgrade installed packages

Once you have updated the package database, you can now upgrade the installed packages. 

```cmd
//To perform a normal upgrade
sudo apt upgrade

//To perform a full upgrade
sudo apt full-upgrade

//All in one
sudo apt update && sudo apt upgrade -y
```

**Full-upgrade works the same as upgrade except that if system upgrade needs the removal of a package already installed on the system, it will do that.**

---
# Install new packages

```cmd
sudo apt install <package name>
```

**Auto-completion** is available!!

### For multiple packages

```cmd
sudo apt install <package_1> <package_2> <package_3>
```

### Reinstall??

Apt will auto upgrade the installed package.

### Install packages without upgrading

```cmd
sudo apt install <package_name> --no-upgrade
```

### Only upgrade packages, not install it

```cmd
sudo apt install <package_name> --only-upgrade
```

### Specific version

```cmd
sudo apt install <package_name>=<version_number>
```

---
# Remove packages

```cmd
sudo apt remove <package_name>
```

### Another way: purge

```cmd
sudo apt purge <package_name>
```

### What's difference?

`apt remove`: just remove the binaries of a package. It leaves residue configuration files.
`apt purge`: removes everything related to a package including the configuration files.

---
# Search for packages

```cmd
//search
apt search <search term>

// Show content
apt show <package_name>

// list installed packages
apt list --installed

// list upgradable packages
apt list --upgradable

//list all the packages available for your system
apt list --all-version
```

---
# Clean your system

```cmd
sudo apt autoremove
```

This command removes libs and packages that were installed automatically to satisfy the dependencies of an installed package.