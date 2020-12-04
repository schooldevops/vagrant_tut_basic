# Synchronize Local and Guest Files

Vagrant 는 자동적으로 파일들을 공유한다. 

로컬 파일을 guest machine 과 싱크 맺음 

파일을 로컬에서 에디트하고, virtual 개발 환경에서 이를 이용할 수 있다. 

기본적으로 Vagrant 는 프로젝트 디렉토리(Vagrantfile 이 있는 디렉토리) /vagrant 디렉토리를 guest machine 에서 접근가능

```
vagrant ssh 

vagrant@tomcat-test:/usr/local$ ls /vagrant
provision-tomcat.sh  README.md  README_PROVISION.md  README_SYCN_LOCAL_GUEST.md  Vagrantfile
<-- 로컬 파일이 보인다. 
```

```
// hello라는 파일을 생성한다. 
vagrant@tomcat-test:/usr/local$ touch /vagrant/hello

// 로컬 파일을 조회하면 다음과 같이 hello 파일이 보인다.
vagrant@tomcat-test:/usr/local$ ls /vagrant
hello  provision-tomcat.sh  README.md  README_PROVISION.md  README_SYCN_LOCAL_GUEST.md  Vagrantfile
```