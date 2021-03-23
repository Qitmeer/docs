---
title: Qitmeer Installation
weight: 1
#pre: "<b>1. </b>"
# chapter: true
---

## [Approach 1: Docker](#approach-1)
For most users, run Qitmeer with a docker is recommended since this would the easiest and fastest way to experience Qitmeer. No worry about the system requisite and no need to wait for compiling build.

### Install docker

#### Windows
1. Download and install package from: https://download.docker.com/win/stable/Docker%20Desktop%20Installer.exe


2. After installation, you need to logout and login again

3. Add current user to docker-users group  
    * open Local Users and Groups  
        search "lusrmgr.msc" in Start Menu and Open it
    * Follow the steps in Figure 1 to add current user to group, replace "Qitmeer" in step 3 with your account 

    ![Figure 1](/images/qitmeer-installation/docker-users.png)

    > Figure 1: Add current user to docker-users group

    * restart or re-login to make the new configuration take effect


#### Mac
Download and install package from: https://download.docker.com/mac/stable/Docker.dmg

#### Ubuntu

```shell
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
sudo apt-get update
sudo apt-get install docker-ce
```

### Run Qitmeer on Docker
```shell
docker pull qitmeer/qitmeerd
docker run -it -p 18130:18130 -p 18131:18131 qitmeer/qitmeerd --notls --rpcuser=test --rpcpass=test
```

## [Approach 2: Build from source](#approach-2)
For developers or people with technical background, we also welcome you to build qitmeer from source

### Setup development environment
Follow [Development Environment](../development-environment)

### Install Qitmeer
From this steps on, all the commands are consistent among all platforms
```shell
git clone https://github.com/Qitmeer/qitmeer ~//github.com/Qitmeer/qitmeer
```
### Run Qitmeer
```shell
cd ~//github.com/Qitmeer/qitmeer
git pull
make
Done building.
  qitmeer version 0.9.2+dev-7478571 (Go version go1.15.5))
Run "./build/bin/qitmeer" to launch.

# once needs cleaning data or problems happened, please uncomment this line to clean data
./build/bin/qitmeer --testnet --notls --rpcuser=test --rpcpass=test
```
