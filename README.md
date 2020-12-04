# Vagrant Tutorial

[from](https://learn.hashicorp.com/tutorials/vagrant/getting-started-index?in=vagrant/getting-started)

## Trouble shooting

- Mac vagrant up 수행했을때 아래 오류 발생시. 

```
There was an error while executing `VBoxManage`, a CLI used by Vagrant
for controlling VirtualBox. The command and stderr is shown below.

Command: ["startvm", "4ec25a51-a29c-48e8-877e-5728dd8a44e6", "--type", "headless"]
```

MAC Preference > 보안 및 개인정보 보호 > 일반 > 'Oracle America Inc' 권한을 허용해주고 재시작하면 동작함. 


## 기본 명령어

### Vagrant 생성하기, 

vm.box 와 함께 생성하는 방법. 

```
vagrant init hashicorp/bionic64
```

### Vagrant 실행하기. 

Vagrant 파일이 존재하는 곳에서 
```
vagrant up
```

### Vagrant 상태보기

```
➜  vagrant_tut vagrant status
Current machine states:

default                   running (virtualbox)

The VM is running. To stop this VM, you can run `vagrant halt` to
shut it down forcefully, or you can run `vagrant suspend` to simply
suspend the virtual machine. In either case, to restart it again,
simply run `vagrant up`.
```

### vagrant ssh 접속하기. 

```
➜  vagrant_tut vagrant ssh
Welcome to Ubuntu 18.04.3 LTS (GNU/Linux 4.15.0-58-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Wed Dec  2 09:22:04 UTC 2020

  System load:  0.77              Processes:           92
  Usage of /:   2.5% of 61.80GB   Users logged in:     0
  Memory usage: 11%               IP address for eth0: 10.0.2.15
  Swap usage:   0%

 * Introducing self-healing high availability clusters in MicroK8s.
   Simple, hardened, Kubernetes for production, from RaspberryPi to DC.

     https://microk8s.io/high-availability

0 packages can be updated.
0 updates are security updates.


vagrant@vagrant:~$ 
```

### vagrant 정지하기. 

```
➜  vagrant_tut vagrant halt
==> default: Attempting graceful shutdown of VM...
```

### vagrant 제거하기

```
➜  vagrant_tut vagrant destroy
    default: Are you sure you want to destroy the 'default' VM? [y/N] y
==> default: Forcing shutdown of VM...
==> default: Destroying VM and associated drives...
```

### vagrant 다시 실행하기

```
vagrant reload
```

### 설치된 리눅스 버젼 확인 

1. ubuntu
```
cat /etc/issue
Ubuntu 18.04.3 LTS \n \l
```

2. centos
```
cat /etc/redhat-release
```

3. general
```
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=18.04
DISTRIB_CODENAME=bionic
DISTRIB_DESCRIPTION="Ubuntu 18.04.3 LTS"
NAME="Ubuntu"
VERSION="18.04.3 LTS (Bionic Beaver)"
ID=ubuntu
ID_LIKE=debian
PRETTY_NAME="Ubuntu 18.04.3 LTS"
VERSION_ID="18.04"
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
```

## Vagrant box

### vagrant box list 확인하기. 

local 에 설치된 vagrant box 목록을 확인할 수 있다. 

```
vagrant box list
bento/ubuntu-16.04  (virtualbox, 202010.24.0)
hashicorp/bionic64  (virtualbox, 1.0.282)
hashicorp/precise64 (virtualbox, 1.1.0)
ubuntu/xenial64     (virtualbox, 20201201.0.0)

```

### vagrant box 추가힉. 

[https://app.vagrantup.com/boxes/search](https://app.vagrantup.com/boxes/search) 혹은 
[http://www.vagrantbox.es/](http://www.vagrantbox.es/) 에서 검색

vagrant box <title> <url>

```
vagrant box add centos7 https://github.com/tommy-muehle/puppet-vagrant-boxes/releases/download/1.1.0/centos-7.0-x86_64.box
```

### vagrant 패키징하기. 

```
vagrant package --output custom-trusty.box
```

### local vagrant box 등록하기

```
vagrant box add Custom-Trusty custom-trusty.box
```

```
➜  vagrant_tut git:(master) ✗ vagrant box list
Custom-Trusty       (virtualbox, 0)
bento/ubuntu-16.04  (virtualbox, 202010.24.0)
centos7             (virtualbox, 0)
hashicorp/bionic64  (virtualbox, 1.0.282)
hashicorp/precise64 (virtualbox, 1.1.0)
ubuntu/xenial64     (virtualbox, 20201201.0.0)
```

### vagrant box 제거하기

```
➜  vagrant_tut git:(master) ✗ vagrant box remove Custom-Trusty
Removing box 'Custom-Trusty' (v0) with provider 'virtualbox'...
```

### vagrant update

```
vagrant box update
```