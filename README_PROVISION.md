# Provisioning with vagrant

웹서버를 수행하고, html 을 서비스 해보는 작업 프로비젼하기. 

프로비젼은 OS 가 설치되고, 시스템 목적을 달성하기 위해 함께 설치되어야할 도구 및 패키지 등을 설치하는 작업을 이야기한다. 

vagrant 는 `vagrant up`  을 통해서 OS가 설치될때 자동으로 설치되도록 지원하며, 반복적인 작업을 수행할 수 있게 멱등성을 제공한다. 

## HTML 파일 생성하기. 

이제 노출 시킬 웹 페이지를 작성해 보자. 

html 디렉토리를 만들고, 하위에 index.html 파일을 생성한다.

./html/index.html

```
<!DOCTYPE html>
<html>
  <body>
    <h1>Getting started with Vagrant!</h1>
  </body>
</html>

```

## 설치 스크립트 작성하기. 

bootstrap.sh

```
#!/usr/bin/env bash

apt-get update
apt-get install -y apache2
if ! [ -L /var/www ]; then
  rm -rf /var/www
  ln -fs /vagrant /var/www
fi
```

- apt-get update: apt-get 을 업데이트한다. 
- apt-get install -y apache2: apache2 서버를 설치한다. 
- `if ! [ -L /var/www ]; then`: /var/www 가 심볼릭 링크가 아닌경우 새로 링크르 걸어준다. 
  
즉, vagrant는 로컬 파일과, 실제 파일을 공유할 수 있기 때문에 심볼릭 링크를 연결하여 서비스를 수행할 수 있다. 

## Vagrant 설정하기. 

이제는 vagrant 가 수행될때 shell 스크립트가 실행되도록 수정하자. 

Vagrantfile 을 다음과 같이 내용을 수정한다. 

```

Vagrant.configure("2") do |config|
  config.vm.box = "hashicorp/bionic64"
  config.vm.hostname = "apache-web-test"

  config.vm.provision "shell", path: "bootstrap.sh"

end
```

위 내용은 vagrant가 수행되면서 provision 을 수행하라는 의미이다. 

이때 "shell" 을 통해서 즉, shell을 이용하여 path에 존재하는 bootstrap.sh 를 실행하라는 의미가 된다. 

## 프로비젼 반영하기. 

이미 vagrant up 으로 러닝되고 있다면 다음 명령을 통해서 변경사항을 새롭게 릴로딩 하자. 

```
➜  vagrant_tut git:(master) ✗ vagrant reload --provision
==> default: Attempting graceful shutdown of VM...
==> default: Checking if box 'hashicorp/bionic64' version '1.0.282' is up to date...
==> default: Clearing any previously set forwarded ports...
==> default: Clearing any previously set network interfaces...
==> default: Preparing network interfaces based on configuration...
```

## 정상적을 프로지변 되었는지 확인하기. 

```
vagrant ssh

```

```
vagrant@apache-web-test:~$ ls /var/www
bootstrap.sh  html  index.html  README.md  README_PROVISION.md  README_SYCN_LOCAL_GUEST.md  Vagrantfile

vagrant@apache-web-test:~$ cat /var/www/index.html 
<!DOCTYPE html>
<html>
  <body>
    <h1>Getting started with Vagrant!</h1>
  </body>
</html>
vagrant@apache-web-test:~$ 
```

우리가 만든 파일이 존재하고 내용도 동일함을 알 수 있다. 

### 심볼릭 링크 확인하기. 

```
vagrant@apache-web-test:/var$ cd /var

vagrant@apache-web-test:/var$ ls -alt
total 52
drwxr-xr-x 13 root root   4096 Dec  3 00:38 .
lrwxrwxrwx  1 root root      8 Dec  3 00:38 www -> /vagrant
```

위와 같이 심볼릭 링크로 정상 등록되어 있다. 

## Web Server 확인하기. 

이번에는 웹서버가 정상 동작하는지 확인하자. 

```
vagrant@apache-web-test:~$ curl localhost
<!DOCTYPE html>
<html>
  <body>
    <h1>Getting started with Vagrant!</h1>
  </body>
</html>
```

정상적으로 노출 됨을 확인할 수 있다. 



