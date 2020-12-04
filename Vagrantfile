# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "hashicorp/bionic64"
  config.vm.hostname = "apache-web-test"

  config.vm.provision "shell", path: "bootstrap.sh"
  config.vm.network :forwarded_port, guest: 80, host: 4567

end

## host 머신에서 테스트하기.

이제 우리 로컬 시스템에서 다음과 같이 호출해보자. 

```
➜  vagrant_tut git:(master) ✗ curl localhost:4567
<!DOCTYPE html>
<html>
  <body>
    <h1>Getting started with Vagrant!</h1>
  </body>
</html>
```

정상적으로 웹 서버의 응답을 받았다. 
