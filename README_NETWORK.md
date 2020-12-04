# Network 설정하기. 

[PROVISION](./README_PROVISION.md) 을 통해서 프로비져닝을 수행했고, vagrant ssh 를 통해 호스트에서 직접 들어가서 웹서버가 정상으로 동작함을 확인할 수 있었다. 

```
curl localhost
```
를 통해서 우리가 만든 index.html 을 확인할 수 있었다. 

## Port Forward 수행하가

단순 프로비져닝을 수행하여 인스턴스를 올려 보았지만, 외부에서는 접근할 수 없다. 

이제는 Port Forward 를 통해서 Web Server 를 외부에서 접근해보자. 

Port forwarding 은 guest machine 에서 host 머신의 port를 통해서 서비스를 제공할 수 있다. 

- guest machine: 이것은 우리가 vagrant up 을 통해서 올라간 서버이다. 
- host machine: 이것은 우리 로컬 시스템이다. 

### Port forward 적용하기. 

이제 호스트 머신에서 포트 4567을 통해서 guest 서버의 웹서버인 80에 접근해보자. 

Vagrantfile 을 아래와 같이 수정해주자. 

```
Vagrant.configure("2") do |config|
  config.vm.box = "hashicorp/bionic64"
  config.vm.provision :shell, path: "bootstrap.sh"
  config.vm.network :forwarded_port, guest: 80, host: 4567
end

```

