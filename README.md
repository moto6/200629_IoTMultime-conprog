# 200629_IoTMultime-conprog
  - 처음 셋팅하는거 : 라즈베리파이 유선연결 
  - win32diskimager 로 이미지 구움.. : 
    > 목차
    # 사물인터넷 멀티미디어 제어 프로그래밍
    ## 1.사운드 제어 프로그래밍
    * 리눅스 사운드 시스템 개요
    * ALSA를 이용한 오디오 프로그래밍
    * 오디오 볼륨 제어 프로그래밍
    * WAV 파일 출력 프로그래밍
    * 파이썬 pigame 모듈을 활용한 MP3 Player 만들기
    ## 2.이미지 제어 프로그래밍
    * 리눅스 멀티미디어 시스템 개요
    * 프레임 버퍼를 이용한 그래픽 프로그래밍
    * BMP 파일 출력 프로그래밍
    ## 3.카메라와 동영상 제어 프로그래밍 
    * V4L2를 이용한 카메라 제어 프로그래밍 
    * 파이썬 picamera 모듈을 활용한 사진찍기
    * V4L2와 프레임버퍼를 활용한 동영상 촬영 프로그래밍
    * 파이썬 picamera 모듈을 활용한 동영상 촬영 프로그래밍
    ## 4.라즈베리파이 멀티미디어 오픈 SW 활용 
    * 웹 모션 캡처 감시카메라 유틸리티 사용 실습
    * 파이썬으로 구현한 웹 스트리밍 감시카메라 사용 실습
    * 오픈 소스 웹 스트리밍 감시카메라 사용 실습

  > day1 1교시 : 하드웨어셋팅, 환경셋업  
  - 라즈베리파이 설명 : AP칩/SOC : AP랑 SOC의 차이
    - AP : 어플리케이션 프로세서 - 
    - SOC : 시스템 온 칩 - 
    - MCU : 단어로 정의 XX 뉘양스로 해석
    - BCM2837, 등등 버전은 다르다.
    - AP속에는 프로세서, 메모리, 
      - ROM : AP속에 들어가있다. = 리드 온니메모리
      - 메인메모리??
      - RW : 메모리
    - SD카드에는 부트파티션이 보인다, 나머지가 안보이는 이유는 파일시스템이 ext4라서 안보임.
    - HDD랑 SSD는 파일시스템이랑 다른게 뭐임, SD카드 
    - 파일 : 파일시스템은 스토리지 위에 올라간다 스토리지는 하드 SSD sd카드일수도 있고
  - ROM이 내부에 들어가 있다???!?!?!?
  - RAM은 1기가가 들어가 있다
  - 파워가 들어오면 동작하는 소프트웨어 롬에서 램을 가져온다
  - 부팅이 되기 위해서 sd 카드에서 
  - 커널 : OS의 핵심 소프트웨어
  - 커널의 코드가 램쪽에 배치되서 복사되서 돌아간다. 부트코드를 어떻게 만들었나 싶었는데, 램에서 커널이 돌면서 OS가 돌기 시작한다
  - 커널은 어플리케이션을 돌릴 준비 : 하드웨어를 가상화시켜버림
  - 디스크 리눅스커널 라즈비안os는 리눅스 OS이다. 
  - 파일시스템 산하에
    - ROOTFS 
      - BIN/....등등등
    - 램에서는 INIT....
    - 멀티미디어 과정이기에 커널을 이해해주셔야되요
    - 멀티미디어는 커널과 직접적인 관계 왜요???
  - 라즈베리파이 부트캠프
    - 라즈베리파이 이미지 설치 및 다운로드
    - ssh 설정
    - 이더넷 연결
    - sd카드(굽기), 리더기, 전원 연결
    - 부팅후 라즈베리파이 찾기
  - raspberrypi.mshome.net
  > 2교시
  - ls
  - cd : Do <tab>
  - pwd : 경로표시됨 -> 루트가따가 패스워드로 따라감
  - mkdir : 
  - 부팅 시퀀스
    - CPU가 롬에 들어있는 프로그램을 돌려여... (바이오스 = 부트로더)
    - 파워가 켜지면 무적권 읽어서 커널을 램으로 올려
    - 커널 램으로 다 올린다음에 하나의 프로세스 실행 그게 init() 프로세서
  - 데몬 , 윈도우 기준에서 서버, smaba데몬
  - ps : 프로세스 스테이터스
    - 프로세스 제어를 잘 해야된다!! ps 커맨드 
    - ps -e -f == ps -ef
    - 위 명령어에서 [] <== 대괄호는 커널
    - 커널은 파일시스템에 없어요 그래서 파일시스템으로 표현 X
    - 표준출력 기호
        ```
        ps -ef > ps_list
        more ps_list
        less ps_list
        ```
    - ls -l 퍼미션 rwx 등등등 읽어볼수 있음
  - 메뉴얼 보기
    ```
    man ls
    ```
  - 정규표현식 : 파일에서 검색 
    ```
    grep smbd ps_list
    ```
    ```
    pi@raspberrypi:~ $ grep smbd ps_list
    root      2347     1  0 11:01 ?        00:00:00 /usr/sbin/smbd
    root      2348  2347  0 11:01 ?        00:00:00 /usr/sbin/smbd
    root      2349  2347  0 11:01 ?        00:00:00 /usr/sbin/smbd
    root      2353  2347  0 11:01 ?        00:00:00 /usr/sbin/smbd
    pi        2689  2347  0 11:20 ?        00:00:00 /usr/sbin/smbd

    ```
  - 위에서 파일만들고, 표준입출력 리다이렉션 하고 어쩌고 귀찮잖아요??   =>> 리눅스에서 파이프 | 못쓰면 바보   
    ```
    pi@raspberrypi:~ $ ps -ef | grep smbd
    root      2347     1  0 11:01 ?        00:00:00 /usr/sbin/smbd
    root      2348  2347  0 11:01 ?        00:00:00 /usr/sbin/smbd
    root      2349  2347  0 11:01 ?        00:00:00 /usr/sbin/smbd
    root      2353  2347  0 11:01 ?        00:00:00 /usr/sbin/smbd
    root      2689  2347  0 11:20 ?        00:00:00 /usr/sbin/smbd
    pi        2752  2602  0 11:26 pts/1    00:00:00 grep --color=auto smbd

    ```
  - SMABA 쌈바! : 라즈베리파이 파일시스템 EXT4 윈도우즈는 NTFS 
    - 상호간에 보고 주고받기 불가능, 이걸 가능하게 해주는게 바로 쌈바!
    - 쌈바 클라이언트 윈도우 
  - x86 ARM 다르다, 실행이 안된다, 리눅스 OS용은 동일(데비안) 하지만 ARM프로세서용으로 빌드된것만 쓸수 있다.
  - 크로스 컴파일러같은거 설치해서 빌드해야됨.. 
    - 라즈비안 뛰어난 이유는 자체 빌드도 가능하고, 
    - 전세계에서 가장 유명한 ARM 리눅스 머신이라 지원이 많이 됨
    - 임베디드 리눅스 귀찮고 어려운게 개발환경 셋업, 진짜 해결을 잘 해준게 바로 라즈베리파이임.
    - 웹캠 오픈소스 있어요 여기서 빌드 하시면 됩니다!! 가장 강려크함
    - 대기업에서 라즈베리파이 많이쓴다. 라즈베리파이급 만들고싶을때 프로토타이핑용으로 만들어 여기서 테스트 해보고 되는거 확인하면 그때야 진짜로 프로덕트 개발 POC 용도로 아주좋아요!! 
    - 라즈베리파이4 AI 까지 겨냥
  - AI도 임베디드 시스템, OS에 유틸리티 기본 다 탑재 파이썬도 쓸 수 있다 다 설치 가능하다 머신러닝 딥러닝 라이브러리 실제로 돌릴수 있다 (트레이닝은 XX)
  - 트레이닝 끝난 모델을 여기서 돌릴수 있단다. 
  - 리눅스를 잘 돌릴줄 알아야 아이디어를 어떻게 엮을건지 각이 보인다.
  - 멀티미디어 경험하는 프로그램을 만들어와서 돌릴꺼지만 결국 활용을 하는 측면을 생각, 결론은 리눅스 시스템을 이해를 잘 해야 한다.
  - 트레이닝 관점에서 교욱을 임베디드 쪽에서 컨버전 !!! 

> Day1 - 3교시 : 라즈베리파이 사운드장치 출력 only 
  - 레코딩을 하고싶다면 USB로 꼽고 들으면 작동 유선이어폰 가져온거 한번 써봐용!! 
  - 모든 하드웨어 컨트롤은 커널에서 한다!! (커널은 모든 하드웨어를 추상화 해주는거거든)
  - 카메라 모듈은 기본 탑재되어있지 않고, CSI 로 연결해서 컨트롤러만 장착되어 있음.
  - 미디어 디바이스 드라이버를 잡어줘야되요, 부팅되면 기본 살려놔써염
  - 커널쪽에서 디바이스 드라이버를 올리는 작업부터 할꺼야!!
  - snd 라는 모듈 적재되어있는 확인
    ```
    pi@raspberrypi:~/iot-mm $ lsmod | grep snd
    snd_bcm2835            32768  2
    snd_pcm                98304  1 snd_bcm2835
    snd_timer              32768  1 snd_pcm
    snd                    69632  7 snd_timer,snd_bcm2835,snd_pcm
    ```
  - 터미널 장치 두개가 있는거야, 리눅스는 파일에 이름을 부여한다. 파일의 이름이 뭐냐 tty
    - 명령어 tty
    ```
    /dev/pts/1
    ```
  - 모든 장치는 파일로 맵핑되어있다!!
    - ps -ef /dev/
  - DD 가 돌고있다는 말은 장치파일이 만들어져있다. DEV아래에 사운드 
  - 내부적으로는 다르지만 사용자관점에서는 파일으로 동일하게 보임, 그래서 다르게 처리를 위해서 항상 /dev/snd 디렉토리에 위치해야함
    ```
    pi@raspberrypi:~/iot-mm $ ls -l /dev/snd/
    total 0
    drwxr-xr-x  2 root root       60 Jun 29 10:53 by-path
    crw-rw----+ 1 root audio 116,  0 Jun 29 10:53 controlC0
    crw-rw----+ 1 root audio 116, 16 Jun 29 10:53 pcmC0D0p
    crw-rw----+ 1 root audio 116, 17 Jun 29 10:53 pcmC0D1p
    crw-rw----+ 1 root audio 116,  1 Jun 29 10:53 seq
    crw-rw----+ 1 root audio 116, 33 Jun 29 10:53 timer
    ```
  - 파일의 종류
    - c : 캐릭터 장치 : 바이트 단위 입출력
    - b : 블럭장치 : 블럭단위 입출력
    - d : 디렉토리
    - 찍 : 그냥파일
  - insmod : 단일모듈만 적재
  - modprob : 모듈의 의존성까지 모두 함꺼번에 적재
  - 이외에 lsmod, rmmod
  - 커널에 DD탑재는 APP영역이 아니기 때문에 Super 권한필요
  - 윈도우와 리눅스의 가장 큰 차이
    - 멀티유저사용자 : 퍼미션 제한 /등등...->> 나는 홈 아래에서만 만들수 있음
    - GUI상태에서는 슈퍼유저 불가능..
    - @@.exe 같은거 라즈베리파이에서 직접 실행 안된다.
      - 라즈베리용 빌드된 파일이 있다면 그걸
      - 오픈소스가 있다면 라즈베리용으로 다시 빌드
      - 업무용으로 뭔갈 하고싶다면 빌드시스템을 구축
    - 내일 웹캠 다운받아서 빌드시스템 구축해서 돌릴꺼야
    - 빌드시스템 어떻게 고쳐야할껀지? 응용할수 있을려면 빌드시스템을 알아야하는데, 빌드시스템 지대로 공부하는경우가 없음 ㅎㅎ...
    - 리눅스 커널과 디바이스 드라이버 강의 배워야함 , 리눅스를 잘 활용할 수 있는 과정을 추가해야함!!!
      - @@@@@@@@빌드시스템 뭡니까??
      - 빌드시스템 : gcc, make, cmake
    - 미디어쪽은 커널 디바이스드라이버 작동해야되고 파일이 만들어저야한다.
    - 라즈베리파이재단에서 미디어 유틸등등 많다!
    - ALSA : 리눅스 커널중 사운드장치 제어할때의 라이브러리, 알사 라이브러리로 만들어진 어플리케이션 
    - amixer 명령어실행, which amixer -> 위치가 리턴됨
    ```
    ls /usr/bin/am*
    ```
    - alsamixer
    - omxplayer : 강남스타일 재생해봄 , 단 시스템 볼륨과 무관하게 동작하는 어플리케이션 제작 !
      - +,-키를 이용해서 볼륨 조절
    - 유틸리티 중에서 포맷이 호환이 안되는 경우가 있음...

> day1 점심이후 
- 오디오 돌려봐 맨땅 ㄴㄴ, 알플레이어, 오앰엑스 플레이어를 사용해서 어플리케이션 작성
- 맨땅코딩 절대 ㄴㄴ...
```
mplayer http://radio.linnrecords.com:8000/stream
```
- 이런 mplay 등의 기존 app을 활용해서 어떻게 만들 수 있는지 고민해보렴..
- alsa를 사용하기전에 이전에 gcc 랑 c언어 컴파일 기본
- ps -ef | grep rplayer
- mplayer 에서 래핑하는 어플  기본 만들어봄
  - pi@raspberrypi:~/iot-mm $ cat test.c
```c
#include <stdio.h>
#include <stdlib.h>
int main(int argc, char *argv[]) {

        int num=1;
        printf("hellow orld!\n");

        if(argc != 2) {
                printf("useage : %s 1(1:jazz, 2:radio, 3:class) \n",argv[0]);
                exit(1);
        }
        num = atoi(argv[1]);// asci to integear
        switch(num) {
                case 1:
                        system("mplayer http://radio.linnrecords.com:8000/stream");
                        break;

                case 2:
                        system("mplayer http://radio.linnrecords.com:8003/stream");
                        break;

                case 3:
                        system("mplayer http://radio.linnrecords.com:8004/stream");
                        break;

                case 4:
                        system("mplayer http://radio.linnrecords.com:8000/stream");
                        break;

                default:
                        printf("invalid");
                        break;

        }
        return 0;
}

```
- 강남스타일(오프라인재생)과 네트워크 라디오 재생시 : 자동 믹싱된다
- 명령어 : ps -ef | grep mplay
```
pi@raspberrypi:~ $ ps -ef | grep mplay
pi        1451  1376  5 14:55 pts/1    00:00:08 mplayer kangnam.mp3
pi        1485  1484  0 14:57 pts/0    00:00:00 sh -c mplayer http://radio.linnrecords.com:8003/stream
pi        1486  1485  8 14:57 pts/0    00:00:02 mplayer http://radio.linnrecords.com:8003/stream
pi        1487  1486  0 14:57 pts/0    00:00:00 mplayer http://radio.linnrecords.com:8003/stream
pi        1515  1490  0 14:58 pts/2    00:00:00 grep --color=auto mplay

```
- 위 ps 명령어로 확인해보면 mplayer가 자동적으로 서브프로세스 자동적으로 프로세스를 돌린다.
- 엠플레이어 자체를 만들려고 하지 마세요 제발!
- 엠플레이어를 가져다가 우리의 상위 레이어 어플을 어떻게 더 잘만들지를 고민하는게 !!!
- 체크포인트 : 여러개 띄었을때 양쪽이 어떻게 도는지, 엠플레이어 이런코드... 이미 뭔가 떠있었어, 사용자가 더 추가할려고 할때
   - 사용자에게 물어보던가, 혹은 이전의 작업을 죽이던가..
   - 커맨드를 많이 아는게 힘이다!! 
- pkill명령어 -> man pkill
  - 메뉴얼을 봐도 모르겠다? 구글신에게 검색
  - pgrep @@@, pkill @@@ 
- 결론, 리눅스 커맨드 , 리눅스 프로세스 만들어라....
- 차일드프로세스 만드는거 좋다 fork를 쓰는거 시스템프로그래밍, 커널함수....  시스템프로그래밍 하는거 만들기 병렬처리 코드->> 서버 클라이언트 프로그래밍 만들수 있어요 반드시 시스템프로그래밍 만들어
- c언어에서 "system()" 함수를 쓰셔야 합니다.
- 직접 프로세스 스레드 돌리고 공부해야되지만, system() 가져다 쓴다. 
  - 라즈베리파이는 왜 이런거 안써도 만들수 있나요!!
    - mplayer 이런것들을 라즈베리파이라는 보드에 맞게 빌드하고 포팅해놓은것이라서
    - 다른 보드에서 이런짓을 잘 해내려면 "리눅스 시스템 프로그래밍" 을 공부해야된다. 근데요즘 이런강좌가 없잖아?>>
  - 리눅스 커널 강의 -> @@@@@@
    - 
    - 빌드시스템, 
  - 디바이스 디펜던시 포팅 어렵다!!! 일반 임베디드 개발
  - 실제 
- 유저 권한에 대하여
  - su : 스위치 유저
  - sudo su : 
  - su - root : 루트로 변경, 루트암호 필요
  - su - kim : f
  - sudo -i ->> 수퍼유저로 변환하는 기능
    - 제품으로 릴리즈 할때는 기능 막아야함
  - whoami ->> root : 내가 누구인지 알려주는 명령어

> 정리 : 
  - soc, sd카드, 프로그램은 항상 램에서 실행된다. 
  - cli환경에서는 R
  - mplayer 처럼 언제 어디서나 쓸수 있게 하는법
    - sudo cp rplayer /usr/bin : 복사하면됨! 슈퍼유저권한 필요함!!
    - 위처럼 명령어를 쓰면 모든 사용자가어디서나 알플레이어
  - 3단계 : 하드웨어, 커널, APP
    - 컨트롤러 
  - 커널의 기능 : 하드웨어 제거, 태스크 매니지먼트, 메모리 매니지먼트, 파일시스템 메니지먼트
- mplayer 같은걸 만들기 위해서는?? : 라이브러리를 사용
  - c/c++로 만들고, C라이브러리는  
  - DD를 직접 제어하기 힘드니까 쉽게 컨트롤 하기 위해서 제공하는게 바로 ALSA
  - 오디오 모듈 제조사에서 ALSA를 만드는데, 이런회사에서 모듈을 움직이게 하는 디바이스 드라이버는 각각 다른거 만들면 빡치니까 ALSA
  - 오디오는 매우 복잡하니 래핑해주는 라이브러리가 바로 ALSA
  - APP 단에서 ALSA를 불러주는 껍데기가 있다 : C언어의 ALSA가 있고, 파이썬의 ALSA가 있다.
  - 리눅스의 로우레벨에서는 디바이스를 어플리케이션에서 접근할때 항상 파일처럼 접근, 알사파일을 열어라!! 출력데이터를 그 파일에다가 써라 
    - @@@ 멀티태스크로 돌아가는데 파일을 어려개 여나@@@@@@@@@@@@ 아니면 @@@@@@@@@@@@@@@@@@@@
      - 디바이스 드라이버 파일은 동시에 여려개 열수 있다??
      - 멀티태스킹 두개가 동시에 믹싱되는거는 디바이스 드라이버 내부 동작이라 잘 모른다..@@
    - 오픈하는게 하나있고, 쓰고 읽고 하는 함수들이 있는거야
    - 오픈할때는 open("/dev/snd/@@@")
    - 커널의 파일시스템이 받아요, 알사의 처리 전체적인 맥락이 이렇다. 알사 라이브러리를 경험해보기 위한 코드를 준비해왔어요
    - 

> n교시 : 
  - DD는 두가지 : 커널에 박혀있는 무조건 로드되는 모듈, 넣다빼따 하나느 모듈 두가지
     - 부팅한다음에 올리는게 모듈이야
  - 파일시스템 하이라키 이해하는게 중요
    ```
    pi@raspberrypi:/ $ ls
    bin   dev  home  lost+found  mnt  proc  run   srv  tmp  var
    boot  etc  lib   media       opt  root  sbin  sys  usr
    ```
  - 하늘색은 링크파일  

  - 링크파일을 만드는 이유
    ```
    pi@raspberrypi:/ $ which gcc
    /usr/bin/gcc
    pi@raspberrypi:/ $ ls -l /usr/bin/gcc
    lrwxrwxrwx 1 root root 5 Apr  9  2017 /usr/bin/gcc -> gcc-6
    pi@raspberrypi:/ $ ls -l /usr/bin/gcc-6
    lrwxrwxrwx 1 root root 25 Mar  1  2018 /usr/bin/gcc-6 -> arm-linux-gnueabihf-gcc-6
    pi@raspberrypi:/ $
    ``` 
  - usr : 모든 사용자가 쓰는것들
   ```
    'user'라는 뜻으로 쓰이다가 나중에 'Unix System Resources'라는 해석이 붙었다는 의견도 있고, 위키 백과의 POSIX 환경에서 파일 시스템 계층에 대한 표준을 보면, '/usr'에 대한 설명은 아래와 같이 나와있습니다:

    Secondary hierarchy for read-only user data; contains the majority of (multi-)user utilities and applications.
   ```
  - 오픈소스를 잘 활용하는 두가지방법 
    - 라이브러리 이해
    - 빌드시스템 구조 이해

  - 라이브러리는 /usr/lib 위치 : 스테틱과 다이나믹, 두가지가 있음
  - usr/include 밑에 저런게 있단다 : <###.h>
  - 해당 위치에 해더가 없음 컴파일이 안됨
  - 설치하는법
    ```
    sudo apt-get install libasound2-dev
    ```
  - 빌드시스템이 중요한거 : 오픈소스 가져다가 빌드할 수 있는 능력이 중요하단다....!!
  - 유용한 커맨드 pushd / popd
  ```  
    pi@raspberrypi:~/iot-mm/ch01/02.audio_pcm $ pushd /
    / ~/iot-mm/ch01/02.audio_pcm
    pi@raspberrypi:/ $ pwd
    /
    pi@raspberrypi:/ $ popd
    ~/iot-mm/ch01/02.audio_pcm
    pi@raspberrypi:~/iot-mm/ch01/02.audio_pcm $
  ```
  - /boot/ : 부팅코드: 빌드된 커널이미지
  - 실제 디바이스드라이버 단 연결할려면 커널을 공부해야해요...
  - 지금 하고계신 커널강의 들으면 될꺼같고.. 라즈베리파이 커널 빌드.. 커널 어떻게 움직이는지, 디바이스드라이버 만드는 팁... 커널소스 다운로드.. 
    - 커널이 요기 들어있어요.. 
    - 커널프로그래밍 디바이스 드라이버 프로그래밍
  - /etc/ : 리눅스 기반에서 뭔가.. 누구누구를 부팅할때 살릴껀지, etc를 공부해야 etc 뭐하는거니
    - 리눅스 쉘 스크립트
    - 서비스 데몬 .d : 복잡한 설정(네트워크 와이파이)
    - 디게디게 중요한 디렉토리
  - /lib  : 루트밑에 라이브러리 : 오브젝트들의 빌드가 여기에 다 되어있어요
    - /usr/lib는 c라이브러리
    - 커널도 빌드가 아주 쉬워요 손을 많이 안타도 되는데요, 모드프로브 임베디드 설정파일 만들어야하는데요, 모듈프로브 알아서 셋팅이 끝나거든요
    - 모듈빌드는 커널강의 한번 들으시면 도움이 되구요
  - /mnt/ : 유에스비같은거
  - /media/  : CD나 DVD같은거 연결함 여기
  - /opt/ : usr이랑 거의 비슷
  - /root/ : 
  - /sb/  : 시스템바이너리, 슈퍼유저권한실행(/bin은 모든유저)
  - /var/ : 대량파일, 로그파일이 들어있음
  - /sys/ , /proc/ : 시스템정보가 들어있는,
  - ./proc을 보면 많은 정보 획득 가능
    - 파일처럼 보이지만, 파일이 아니다, 디스크에 존재하지않고, 커널이 제공하는 서비스, 커널이 가지고 있는 정보를 우리한테 보여주는것 뿐이다.
    ```
        pi@raspberrypi:/proc $ ls -l cpuinfo
        -r--r--r-- 1 root root 0 Jun 29 16:03 cpuinfo
        pi@raspberrypi:/proc $ cat cpuinfo
        processor       : 0
        model name      : ARMv7 Processor rev 4 (v7l)
        BogoMIPS        : 38.40
        Features        : half thumb fastmult vfp edsp neon vfpv3 tls vfpv4 idiva idivt vfpd32 lpae evtstrm crc32
        CPU implementer : 0x41
        CPU architecture: 7
        CPU variant     : 0x0
        CPU part        : 0xd03
        CPU revision    : 4

        processor       : 1
        model name      : ARMv7 Processor rev 4 (v7l)
        BogoMIPS        : 38.40
        Features        : half thumb fastmult vfp edsp neon vfpv3 tls vfpv4 idiva idivt vfpd32 lpae evtstrm crc32
        CPU implementer : 0x41
        CPU architecture: 7
        CPU variant     : 0x0
        CPU part        : 0xd03
        CPU revision    : 4

        processor       : 2
        model name      : ARMv7 Processor rev 4 (v7l)
        BogoMIPS        : 38.40
        Features        : half thumb fastmult vfp edsp neon vfpv3 tls vfpv4 idiva idivt vfpd32 lpae evtstrm crc32
        CPU implementer : 0x41
        CPU architecture: 7
        CPU variant     : 0x0
        CPU part        : 0xd03
        CPU revision    : 4

        processor       : 3
        model name      : ARMv7 Processor rev 4 (v7l)
        BogoMIPS        : 38.40
        Features        : half thumb fastmult vfp edsp neon vfpv3 tls vfpv4 idiva idivt vfpd32 lpae evtstrm crc32
        CPU implementer : 0x41
        CPU architecture: 7
        CPU variant     : 0x0
        CPU part        : 0xd03
        CPU revision    : 4

        Hardware        : BCM2835
        Revision        : a020d3
        Serial          : 000000008609c591
    ```
  - ps도 하나의 어플인데, ps를 만들 수 있어요! 뭐가 필요하겠어요?? ps를 만드는건 커널의 정보를 가져다가
  - 안드로이드 ps소스를 만드는 방식 :  proc아래 소스를 긁어다가 뿌리는것 이기 떄문에.. 
  - 리눅스 우분투나 여기저기 흩어져 있어, 안드로이드는 한곳에 딱 모여있어.... 안드로이드 시스템 전문가이심
  - 안드로이드 미들웨어 분석.. 안드로이드 
  - 리눅스는 흩어져 있어서 보기 어려워
  - more meminfo
  - more modules : 이걸 긁어다가 lsmodule
  - 프로그램 실행중이면 "/proc/@@@@"

  - ls -l fd : 파일이 열려인
  - proc을 알면 태스크들을 설치를 잘 할 수 있다!@!!!!!!!
  - /run/ /srv/ : 프로세스 통신메카니즘, 하드디스크의 파일이 아니니까 무시하시라
  - 파일시스템은 진짜 하드에 있는게 있고 없는게 있다.. 
  - sys proc dev 등등은 없음, 리더파일시스템 아니고 쉐도우(슈도 파일시스템
  - /proc 같은데다가 뭔가 파일이든 디렉토리 만들고 리부팅 하면 
  - 파일시스템 구조를 모르고 쓰면 황당한 일을 겪을 수 있다..
- gcc 쓸때 -c 옵션주면 에러가 뜬다? : 문법에러
  - 없으면 링킹혹은 다른에러
- gcc -c alsapcm.c
  - 오브젝트파일만 생성됨
- gcc alsapcm.o -lasound
  - sin함수 포함되어있는데, 없어서 에러뜸 
- gcc alsapcm.o -lasound -lm
  - 이렇게 해야지 컴파일이 된단다!!
- 음성의 퀄리티를 
  - 샘플링레이트
  - 비트레이트
- aplay는 압축X, mplay : 압축파일 디코더 필요(리눅스 커널에 디코더+인코더 내장되어있음)
- 기본이 wav파일이지만, 압축한게 mp3, 오디오+비디오:mp4
- pcm 라이브러리를 부르시기 전에 파라미터 셋팅..!
- 시작과 끝날때 말해줭
- 참고링크
  - http://equalarea.com/paul/alsa-audio.html
  - http://www.alsa-project.org/alsa-doc/alsa-lib/index.html


```c
#include <stdio.h>
#include <fcntl.h>
#include <limits.h>
#include <math.h>
#include <sys/ioctl.h>
#include <alsa/asoundlib.h>

#define BITS            2                       //bit rate : 2ytes

#if 1
#define FRAGMENT        8
#else
#define FRAGMENT        2
#endif

#define DURATION        5.0                     //sec
#define MODE            1                       //채널수:mono
#define FREQ            44100           //sampling rate
#define BUFSIZE         (int)(BITS*FREQ*DURATION*MODE)

int setupDSP(snd_pcm_t *dev, int buf_size, int format, int sampleRate, int channels);

int main(int argc, char *argv[])
{
        snd_pcm_t *playback_handle;
        double total = DURATION, t;

#if 1
        int freq = 440;                                         //재생음의 주파수:440Hz
#else
        int freq = 8000;                                        //재생음의 주파수:8KHz
#endif

        int i, frames, count=1;
        char *snd_dev_out = "plughw:0,0";       //오디오 디바이스의 이름
        short buf[BUFSIZE];                                     //입출력 오디오를 위한 버퍼

        //오디오 디바이스 열기
        if(snd_pcm_open(&playback_handle, snd_dev_out, SND_PCM_STREAM_PLAYBACK, 0) < 0) {
                perror("Could not open output audio device");
                return -1;
        }
        printf("Identifier of PCM handle : %s\n", snd_pcm_name(playback_handle));

        //오디오 디바이스 설정
        // setupDSP() 함수 오지게 기니까 코드 주석 달아놨음 읽어라 근데 읽고들어도 모르지않겠니
        if(setupDSP(playback_handle, BUFSIZE, SND_PCM_FORMAT_S16_LE, FREQ, MODE) < 0) {
                perror("Could not setup output audio device");
                return -2;
        }



        //
        //정현파 데이터 생성
        printf("Make Sine Wave!!\n");
        for(i=0; i<BUFSIZE; i++) {
                t = (total/BUFSIZE) * i;
                buf[i] = SHRT_MAX * sin((int)(2.0 * M_PI * freq * t)); ///sin파 만드는 공식이야
                
        }

        frames = BUFSIZE / (MODE * BITS);

        while(count--) {
                //오디오 출력을 위한 준비
                snd_pcm_prepare(playback_handle);

                //오디오 데이터를 디바이스로 출력(쓰기)
                snd_pcm_writei(playback_handle, buf, frames);   //i:interleaved, n:non-interleaved
        }

        //오디오 버퍼 버리기
        //막아도 돌지만 버퍼에 찌꺼기 남을수 있음
        snd_pcm_drop(playback_handle);

        //알사 라이브러리가 어떤지가 이렇구나! 라고 느끼기만 해랴
        //코딩을 직접하는건 별 의미 없다 어떻게 움직이는지는 이해해야된다.
        //오디오 디바이스 닫기
        snd_pcm_close(playback_handle);

        return 0;
}

int setupDSP(snd_pcm_t *dev, int buf_size, int format, int sampleRate, int channels)
{
        snd_pcm_hw_params_t *hw_params;
        snd_pcm_uframes_t frames;
        int fragments = FRAGMENT;
        int bits = (format == SND_PCM_FORMAT_S16_LE)?2:1;

        //오디오 디바이스의 매개변수 구조를 위한 메모리 할당
        if(snd_pcm_hw_params_malloc(&hw_params) < 0) {
                perror("Could not allocate parameters");
                return -1;
        }

        //오디오 디바이스의 매개변수들의 초기화
        if(snd_pcm_hw_params_any(dev, hw_params) < 0) {
                perror("Could not initialize parameters");
                return -2;
        }


        //억세스 타입을 정함. INTERLEAVED기법을 사용
        // INTERLEAVED기법은 레프트 라이트 섞어서 쓴다
        //오디오 데이터 접근(access) 타입(인터리브, 넌인터리브)을 설정함
        if(snd_pcm_hw_params_set_access(dev, hw_params, SND_PCM_ACCESS_RW_INTERLEAVED) < 0) {
                perror("Could not set access type");
                return -3;
        }



        //// PCM은 16비트로 쓰겠다
        //샘플링 레이트를 설정함 : 부호있는 16비트 리틀엔디안
        if(snd_pcm_hw_params_set_format(dev, hw_params, format) < 0) {
                perror("Could not set sample format");
                return -4;
        }

        //set_rate 
        // near : 하드웨어가 해당srate 를 지원하지 않을때
        //샘플의 포맷을 설정함 : 44.1KHz(CD 수준의 품질)
        if(snd_pcm_hw_params_set_rate_near(dev, hw_params, &sampleRate, 0) < 0) {
                perror("Could not set sample rate");
                return -5;
        }
        //snd_pcm_hw_params_get_rate()

        //채널 설정 : MONO(1)
        if(snd_pcm_hw_params_set_channels(dev, hw_params, channels) < 0) {
                perror("Could not set channel count");
                return -6;
        }

        //프레임 주기 설정
        //전체 데이터가 크면 쪼개보ㄴ내나 완장크기냐
        if(snd_pcm_hw_params_set_periods_near(dev, hw_params, &fragments, 0) < 0) {
                perror("Could not set fragments");
                return -7;
        }
        //snd_pcm_hw_params_set_periods_xxx(), xxx:near,first,last,min,max,minmax,integer

        //버퍼의 크기 설정
        //snd_pcm_hw_params_set_buffer_size_near() 함수 : 지원하는 크기의 함수인지, 에러가 뜨믄
        frames = (buf_size * fragments) / (channels * bits);
        if(snd_pcm_hw_params_set_buffer_size_near(dev, hw_params, &frames) < 0) {
                perror("Could not set buffer_size");
                return -8;
        }
        

        //지금까지 설정한 파라미터 함수를 셋팅!!!!!!!!!
        //앞에서 설정한 오디오 디바이스의 매개변수를 ALSA 시스템에 적용
        if(snd_pcm_hw_params(dev, hw_params) < 0) {
                perror("Could not set HW params");
                return -9;
        }

        return 0;
}

```


> 마지막시간 마지막!!!
  - 사운드 오늘은 주로 사운드, 내일은 카메라 및 비디오.. 라즈베리파이용 LCD
  - 오디오 볼륨제어 프로그래밍
  - API 한번 슥 설명해주고 어플리케이션 돌려

```c

//ALSA Tutorial site :
//http://equalarea.com/paul/alsa-audio.html
#include <stdio.h>
#include <stdlib.h>
#include <alsa/asoundlib.h>

int main(int argc, char *argv[])
{
        snd_mixer_t *mixer;
        snd_mixer_elem_t *elem;                 //믹서를 위한 PCM 엘리먼트
        snd_mixer_selem_id_t *id;
        int status;
        long maxVal=100, minVal=0;
        //long outVal=50;
        long outVal = (argc==1) ? 50 : atol(argv[1]);

        static const char *mix_name = "PCM";    //PC의  ALSA는 "Master"를 사용
        static const char *card = "default";
        static int mix_index = 0;

        snd_mixer_open(&mixer, 0);              //mixer 디바이스 열기
        snd_mixer_attach(mixer, card);  //기본 믹서 사용하기
        snd_mixer_selem_register(mixer, NULL, NULL);
        snd_mixer_load(mixer);                  //믹서 불러오기

        //믹서 사용을 위한 ID 객체의 할당,얼로캐이션 한다
        snd_mixer_selem_id_alloca(&id); //snd_mixer_selem_id_malloc()

        //ID에 믹서의 이름(name)과 인덱스(index) 설정
        snd_mixer_selem_id_set_index(id, mix_index);
        snd_mixer_selem_id_set_name(id, mix_name);

        //설정된 ID를 이용해서 해당 믹서의 엘리먼트 찾기
        //믹서의 엘리맨트를 찾아와서...
        elem = snd_mixer_find_selem(mixer, id);
    

#ifdef SETVOL  // gcc alsavolume.o -lasound :: 로 컴파일하고 볼륨의 범위를 0부터 100으로 변경 , 코드에다가 #define SETVOL로 줘도 되고 빌드할때 해도됨
        //볼륨의 범위(최소값/최대값)를 설정하고 현재의 값을 설정하기
        outVal = (outVal * (maxVal - minVal) / (long)(100-0)) + minVal;
        snd_mixer_selem_set_playback_volume_range(elem, minVal, maxVal);//여기서 볼륨의 레인지를 설정할 수 있다.
        snd_mixer_selem_set_playback_volume_all(elem, outVal);// 시스템의 모든 볼륨 설정이 이값으로 바뀌는

        //현재 설정된 믹서의 범위를 가져와서 화면에 표시
        snd_mixer_selem_get_playback_volume_range(elem, &minVal, &maxVal);//get, 위에서 설정한 기능들이 맞게 설정됬는지 찍어본다.
        fprintf(stdout, "Set volume %d(%d/%d)\n", outVal, minVal, maxVal);
#else
        //현재 설정된 믹서의 범위를 가져와서 화면에 표시
        snd_mixer_selem_get_playback_volume_range(elem, &minVal, &maxVal);
        fprintf(stdout, "Current volume (%d/%d)\n", minVal, maxVal);
#endif

        snd_mixer_close(mixer);

        return 0;
}
```
  - gcc alsavolume.o -lasound로  컴파일하고 볼륨의 범위를 0부터 100으로 변경 , 
  - 코드에다가 #define SETVOL로 줘도 되고 빌드할때 해도됨
    - gcc alsavolume.c -lasound -DSETVOL
  - 시스템 볼륨을 변경하는 코드
  - 일일이 코딩실습 이렇게 안해 어플에서 못해요
  - 이런걸 할려면 뭐다? 미들웨어  : 어플에서 일일이 동기화처리.. 뒤짐.. ㅠㅠㅠ
  - 멀티미디어 미들웨어 라이브러리를 쓰셔야되요, 오디오비디오 스트리밍 라이브러리 : 쥐스트리머
  - 전문적인 솔루션업체는 지스트리머 쓴다..!!!!

  - Wav파일 플레이어, 
  - 파이썬 파이게임 모듈을 활용한 MP3플레이어 만들기, 간단한 응용은 Python
  - C언어로 wave파일 만드는 기능을 제작..
  - hd(헥사덤프) 
    -  hd police_s.wav
        - 00000000  52 49 46 46 71 03 01 00  57 41 56 45 66 6d 74 20  |RIFFq...WAVEfmt |
    - wav파일의 기본 형식.. 파일이 이런식으로 만들어져요..
    - 엠플레이어는 이런 기능이 구현되어있다.
    -     



```
리눅스 시스템 프로그래밍 강좌
  
리눅스 커널 강좌

리눅스 디바이스트리/드라이버 차이가 뭐징?
  내일
추가적인 튜토리얼 이그잼플?
알사 라이브러리 
직접 라이브러리 만드시는 분이 누구냐면 : 플레이어 제작업체, 디바이스 드라이버(사운드 디바이스 드라이버), 기본으로 잘 돌아야,,, 
  그렇지 않은 보직이다 하면 이해만 하면 된다.. 볼륨제어 등등.. -> 가져다 쓰기만 해라
소리의 크기는 진폭인가요??
웨이브랑 엘사 (쥐스트리머) 공식 이그잼플은 어디에서 받을수 있나요?
```
```
Q) HAL이랑 ALSA랑 같나 다르나? 
A) 비슷하고 다르다...
```