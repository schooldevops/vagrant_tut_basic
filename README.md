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
