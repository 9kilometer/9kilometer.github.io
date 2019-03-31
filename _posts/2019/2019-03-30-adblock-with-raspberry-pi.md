---
title: "라즈베리파이로 광고 차단기 만들기"
# excerpt: ""
# header: 
#     overlay_image: /assets/resources/post_header.jpg
last_modified_at: 2019-03-30T00:00:00
category: dev
toc: true
tag: 
    - raspberry pi
    - pihole
    - PYTHON
---

 언젠가 쓸 일이 있지 않을까 하고 구해뒀던 라즈베리 파이를 묵혀둔 지 몇 년째, 정말로 고물이 되어버리기 전에(...) 뭐라도 만들까 하고 찾던 중 광고차단기로 활용할 수 있다는 글을 보고 시도해봤다. 컴퓨터로는 이미 웹 브라우저에 광고 차단 플러그인을 받아 쓰고 있었지만, 이걸 쓰면 디바이스 상관 없이 광고를 차단시킬 수 있다는 점이 끌렸다. (폰으로 인터넷 볼 때 옆으로 좀만 슬라이드해도 광고 페이지로 넘어가는 광고같은 것들이 너무 짜증나기도 했고...-_-)  

 일단 가지고 있는 장비는,
 - raspberry pi 2 model B
 - SD카드(+리더기), 랜선, 케이블, 와이파이 동글 등
 - 브레드보드와 입출력 키트

브레드보드와 입출력 키트로는 전원 스위치를 만들 예정이고, 이 글에선 광고차단기 적용까지의 과정만 적었다.

---

## OS 설치
 일단 SD카드를 준비하자. 가벼운 OS로 설치할거면 최소 4GB면 된다고 하는데, 그냥 가지고 있던 16GB짜리를 썼다.
 개인 PC에 SD카드를 연결하고 [여기](https://www.raspberrypi.org/downloads/raspbian/)서 라즈비안 이미지를 다운받자.  

<figure style="width:90%">
    <img src="/assets/images/2019/adblock-with-raspberry-pi/os_image.png">
</figure>  

어차피 헤드리스로 돌릴거니 가볍게 Raspbian Stretch Lite 이미지를 다운 받았다.  
(zip 파일로 받으려다가 너무 느려서 멈추고 토렌트로 받았다... 토렌트 프로그램 있다면 토렌트를 쓰는 걸 추천...)  

이제 이미지 작성 도구로 다운받은 이미지를 SD카드에 굽자.  
Etcher라는 프로그램을 사용했다. [다운로드](https://www.balena.io/etcher/)

<figure>
    <img src="/assets/images/2019/adblock-with-raspberry-pi/image11.gif">
</figure>

크로스플랫폼이라 윈도우던 맥이던 상관 없이 쓸 수 있다. 다운받은 이미지를 압축 풀어둘 필요도 없고, 사전에 SD카드를 따로 포맷할 필요도 없다. 이미지와 SD카드를 선택하고 Flash 버튼을 누르면 끝! 써보니 이동식 저장장치가 아니면 드라이브 목록에도 안 떠서 실수로 C드라이브를 날려먹는다던지 하는 일이 생길 가능성도 없다.  

작업 완료 후 SD카드를 라즈베리 파이에 꽂고 전원을 켜자.  

---
## Pi-hole 설치
Pi-hole은 오픈 소스 프로젝트로, DNS 서버를 직접 구축하고 차단 필터를 적용해 네트워크의 모든 장치에 대한 광고를 차단한다.  
공식 깃허브는 [이쪽](https://github.com/pi-hole/pi-hole)  

 라즈베리파이를 부팅 후 로그인한다. 기본 username은 `pi`, 비밀번호는 `raspberry`다.  
로그인 후 하단의 커맨드로 Pi-hole을 설치한다.  
```
curl -sSL https://install.pi-hole.net | bash 
```  
설치 과정에 여러 선택지가 나오는데, 전부 권장사항을 선택했다. 어차피 나중에 바꿀 수 있으니 깊게 생각할 필요 없을 듯.  
선택지에 뭐가 있는 지 더 알고싶다면 [이 블로그](http://blog.naver.com/PostView.nhn?blogId=seoulworkshop&logNo=221420966250)에 정리가 잘 되어있으니 참고.  

 설치가 끝나고 뜨는 창에 현재 ip와 관리페이지 주소 및 관리페이지 비밀번호가 뜬다. **비밀번호는 반드시 기록해두자!!**  

같은 네트워크를 쓰는 개인 PC에서 관리페이지로 접속하고 로그인하면 다음과 같은 화면을 볼 수 있다.  

<figure>
    <img src="/assets/images/2019/adblock-with-raspberry-pi/pretty-stats.png">
</figure>

---
## 차단필터 추가하기
Pi-hole 관리자 페이지에서 `Settings -> Blocklist` 에서 차단 리스트를 추가할 수 있다.  
설치할 때 권장 사항을 선택했다면 이미 몇 개의 차단 리스트가 들어가 있을 것이다.  

<figure>
    <img src="/assets/images/2019/adblock-with-raspberry-pi/blocklist_1.png">
</figure>  

여기에 [어떤 분](https://www.clien.net/service/board/lecture/10895199)께서 공개한 국내 차단 리스트를 추가하자.  
`https://godpeople.or.kr/hosts.txt` 이 주소를 차단 리스트에 추가하고 저장&업데이트 한다. 리스트가 많아서 그런지 새로 리스트 추가 후 업데이트에 시간이 좀 걸린다. 업데이트가 끝날 때까지 가만 냅두자.  

<figure>
    <img src="/assets/images/2019/adblock-with-raspberry-pi/blocklist_2.png">
    <figcaption>업데이트 성공!</figcaption>
</figure>  

이 메뉴에선 여러 도메인이 적힌 **파일 경로**만 추가 가능하고, 도메인 하나씩 개별적으로 차단 필터에 추가하는 건 `Blacklist` 메뉴에서 한다.  
정확히 해당 주소에 해당하는 것만 차단할 건지(exact), 와일드카드(wildcard)나 정규식(regex)에 맞는 도메인을 전부 차단할 건지 골라 추가해주면 된다.  

<figure>
    <img src="/assets/images/2019/adblock-with-raspberry-pi/blacklist.png">
</figure>  

---
## 공유기 설정 변경
DNS 서버를 만들었으니 공유기에서 이걸 DNS 서버로 지정해야 한다. 그리고 내 경우 라즈베리 파이에 고정 IP를 할당하는 것도 공유기 설정에서 했다. 각자의 공유기 설정 페이지에 접속하자. 나는 iptime 공유기를 쓰므로 `192.168.0.1`로 접속한다.  

인터넷 연결 설정에서 '수동으로 공유기의 DNS 서버 설정' 체크 후 라즈베리 파이 서버 IP를 기본 DNS 서버에 적는다.  
그리고 보조 DNS 서버는 비워놔야 제대로 차단이 되더라.  

<figure>
    <img src="/assets/images/2019/adblock-with-raspberry-pi/router_config_1.png">
</figure>  

수동 IP 할당은 여기서  

<figure>
    <img src="/assets/images/2019/adblock-with-raspberry-pi/router_config_2.png">
</figure>  

---
## 테스트
설정 완료하면 테스트할 기기에서 네트워크 연결을 끊고 재연결한 후 아래 사이트에 접속해본다.  
다음과 같은 화면이 뜨면 성공  

[https://blockads.fivefilters.org/?pihole](https://blockads.fivefilters.org/?pihole)

<figure>
    <img src="/assets/images/2019/adblock-with-raspberry-pi/success.png">
</figure>

[https://ads-blocker.com/testing/](https://ads-blocker.com/testing/)

<figure style="width:50%" class="align-center">
    <img src="/assets/images/2019/adblock-with-raspberry-pi/test1.jpg">
</figure>

**끝!**
{: style="text-align: center; font-size: 30px;"}

---
## 그 외 추가 작업
1) 이 작업이 유의미한 효과가 있는 진 모르겠는데, `Settings -> DNS`의 upstream DNS의 커스텀 필드에 국내 dns 서버를 추가해놨다.  

<figure>
    <img src="/assets/images/2019/adblock-with-raspberry-pi/upstream_dns.png">
    <figcaption>custom 1,2에 KT DNS 주소. ip 뒤에 #53은 설정 저장하니까 자동으로 붙는데 뭔지 모르겠다. </figcaption>
</figure>

2) 공유기 설정에서 DNS를 라즈베리 파이 서버 하나만 적어뒀기 때문에 라즈베리 파이를 끄면 인터넷 연결이 안될 것이다. 하지만 라즈베리 파이를 24시간 내내 틀어둘 게 아닌데다가 PC에선 애드블럭 플러그인을 쓰고 있어 굳이 여기서 만든 DNS 서버를 쓸 필요가 없다고 느껴서, 집에서 쓰는 기기들의 DNS 설정을 바꿔놨다. PC에선 라즈베리 파이 서버를 아예 안 쓰고, 폰에선 보조 DNS를 추가한 것이다. 이렇게 해두니 폰으로 볼 때 라즈베리 파이가 꺼져있어도 인터넷 연결이 잘 된다(당연히 광고 차단은 안 된다).  

윈10 기준 : 제어판 - 네트워크 및 인터넷 - 네트워크 및 공유센터 - 어댑터 설정 변경  

<figure>
    <img src="/assets/images/2019/adblock-with-raspberry-pi/a1.png">
    <figcaption>사용한 DNS 서버는 KT 기본/보조 DNS 서버</figcaption>
</figure>


안드로이드 :  와이파이 현재 네트워크 선택 - 고급 

<figure style="width:50%" class="align-center">
    <img src="/assets/images/2019/adblock-with-raspberry-pi/android.jpg">
    <figcaption>DNS 1: 라즈베리 파이 DNS / DNS 2: KT DNS</figcaption>
</figure>

3) 검색해보면 유투브 광고 차단용 도메인 리스트가 있길래 적용해봤는데, 거의 안 걸러진다. 광고마다 주소가 전부 다르고 규칙성도 없어서 정규식으로 필터 걸지도 못함. 한 번 시도해봤는데 광고만 재생 안되는 게 아니라 영상 자체가 재생이 안 되더라...  

---
## 참조
https://blog.xcoda.net/82  
https://opensource.com/article/18/2/block-ads-raspberry-pi  
https://www.balena.io/blog/deploy-network-wide-ad-blocking-with-pi-hole-and-a-raspberry-pi/?utm_source=efp&utm_medium=etcher&utm_campaign=balena-pihole&utm_content=v2  
