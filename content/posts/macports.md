+++
authors = ["pixrl"]
title = "Simple guide to Macports"
date = "2024-06-03"
description = "Simple guide to Macports"
tags = [
    "macos",
    "macports",
]
categories = [
    "macos",
]
series = ["administration"]
+++
Macports [per official documentation](https://www.macports.org/) is "an open-source community initiative to design an easy-to-use system for compiling, installing, and upgrading either command-line, X11 or Aqua based open-source software on the Mac operating system".

This simple guide demonstrates the most common commands for MacPorts. 

Refer to official [MacPorts Guide](https://guide.macports.org/#installing.macports) to install MacPorts.

#### Search for ports
```
port search [--name] [--regex] '<searchtext>'
```
This command searches both the name and description of ports.

You can also use wildcards to limit searches, e.g. ‘openjdk*’.
#### Get information about a port
```
port info <portname>
```

#### List installed ports
For a list of the ports explicitly installed
```
port echo requested
```
For a list of everything installed by MacPorts
```
port installed
```
## Install/Uninstall Ports
#### Install a port
```
sudo port install <portname>
```
#### Cleaning up after failed install
The `clean` deletes intermediate files created by MacPorts while installing a port. A **port clean** is often necessary when builds fail and should be the first thing to try after a failed installation attempt.
```
sudo port clean <portname>
```

#### Uninstall a port
The `uninstall` action will remove an installed port. To remove unused dependencies run `sudo port uninstall leaves`.
```
sudo port uninstall <portname>
```
## Updates
#### Selfupdate command
The selfupdate update the local ports tree with the global MacPorts ports repository so you will have the latest versions of software packages available.
```
sudo port selfupdate
```
#### Show available updates
```
sudo port outdated
```
#### Update outdated ports
```
sudo port upgrade outdated
```
#### Update a specific port
```
sudo port upgrade <portname>
```
## Cleanup/Maintenance
#### List inactive ports
Upgrade does not uninstall the old version of a port. Instead, it deactivates it, i.e., it stashes the files belonging to the older version away in a tarball. This allows you to go back to the older version if there happens to be a problem with the updated one. Use `port installed inactive` to get a list of inactive ports you likely no longer need.
```
sudo port installed inactive
```

#### Uninstall all inactive ports
Periodically you should uninstall old versions.
```
sudo port uninstall inactive
```
#### Uninstall no-longer needed dependencies (leaves)
Uninstalling a port will not uninstall ports that have been automatically installed as dependencies of the uninstalled port and are otherwise unused. You can trigger this behavior by passing the `--follow-dependencies` flag. Ports that were manually installed (i.e., are marked as “requested”) or have other dependents will not be removed. You can manually uninstall the unneeded ports later using the leaves pseudo-port, e.g., using `sudo port uninstall leaves`.
```
sudo port uninstall leaves
```