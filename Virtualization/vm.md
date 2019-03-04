# Virtualization

### Cloud Init 붙여보기

#### 0.1 guestfs

- virtual amchine dis에 접근가능하고 변경할수 있게 해주는 것.
- sudo apt install libguestfs-tools 
- guestfish -a Centos~.qcow2 와 같은 식으로 이미지에 접근가능.

~~~shell
- run

  - guest by adding disks, then mount any disks you need

- list-filesystems

- mount /dev/sda1

- ls /usr/share/licenses/cloud-init* 
  
~~~

* cent os7의 버전을 찾는 =>. 0.7.9로 나옴.



#### 0.2 meta/user data

* metadata
  * 말그대로 서버 meta정보 name, instance id displayname ...
* userdata
  * ec2 userdata에 넣는 것처럼 실제 실행될때 작동되는 script들
* meta 와 user data 는 filesystem(flopy, iso..)의 root에 위치해야된다
* 자체적으로 예를 통해 meta user data를 잘 만들고..



#### 0.3 vm instance 새성

* cloud image를 기반으로 실제 넣어줄 vm image 를 만들어야함.





#### 0.4 qcow2

* Qemu Copy on Write 
* copy on write를 지원하는 이미지. 
* 복사하지 않고 새로운 블록에 데이터를 기록하기 떄문에 스냅샷을 뜰수가 있다. 



#### 0.5 fqdn

* Fully Qualified Domain Name
* namespace게층상 최종 호스트명을 포함하는 도메인명을 뜻함.
* 그냥 풀 도메인 이름 이라고 생각하면댐.



#### 0.9999 ???

* [cidata](https://cloudinit.readthedocs.io/en/0.7.9/topics/datasources/nocloud.html) : 걍 volume lable이름이 cidata여양한다는 뜻.











### Reference

* [meta/user data](https://cloudinit.readthedocs.io/en/latest/topics/datasources.html)
* [tutorial](https://leeyj7141blog.wordpress.com/2017/12/01/libvirt-kvm-환경에서의-cloud-init-간단-사용법/)


