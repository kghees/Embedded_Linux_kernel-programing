# Embedded_Linux_kernel-programing  
## 리눅스 커널 프로그래밍이란?  
커널의 도움을 받아 H/W를 제어하는 디바이스 드라이버 개발    

### Bootloader(부트로더)  
- 운영 체제가 시동되기 이전에 미리 실행되면서 커널이 올바르게 시동되기 위해 필요한 모든 관련 작업을 마무리하고.
  최종적으로 운영 체제를 시동시키기 위한 목적을 가진 프로그램
 - Disk에 저장되어 있는 운영체제를 실행 시키는 역할
 - 부팅을 하기 위한 수많은 동작들을 도와주는 프로그램
 - 부트 스트랩 로더를 줄여 부트스트랩 or 부트로더 라고 한다.
 - 라즈베리파이는 자체 부트로더 사용 중!
  
- 부트로더(Bootloader)의 역할
    컴퓨터 시스템이 부팅 프로세스를 시작하고 운영체제를 로드하는 중요한 역할을 하는 프로그램
      - 다중 OS 부팅기능
      - 장치 제어 및 테스트 기능
      - 부팅 옵션 관리
      - 하드웨어 초기화 등등
- Linux Boot Loader
    - GRUB2
    - Grand Unified Bootloader
    - GNU 프로젝트에서 개발한 부트로더
**Bootloader를 사용하는 이유**
운영체제의 부팅에 있어서 가장 중요한 것중에 하나로, 운영체제가 시동되기 전에 미리 실행되어
커널이 올바르게 사용되기 위해 필요한 모든 작업을 마무리 하고 최종적으로 운영체제를 시동시키기
위한 목적을 가진 프로그램

### PC Booting Process  
#### CMOS(Complementary Metal-Oxide Semiconductor)(H/W chip)  
- CMOS Chipset (RTC/NVRAM), 비휘발성 메모리
- 마이크로프로세서나 S램 등 디지털 회로를 구성하는데 사용되는 집적회로의 한 종류.
- 컴퓨터의 설정 정보를 저장함(메모리 크기, 부팅순서, H/W 구성 정보 등)
- BIOS로 설정 정보를 수정할 수 있다.

#### BIOS(Basic Input/Output System)(S/W)
-  운영 체제 중 가장 기본적인 소프트웨어이자 컴퓨터의 입출력을 처리하는 펌웨어
-  컴퓨터 부팅 시 바로 BIOS(Firmware)가 동작을 시작한다.
-  주변 장치(H/W)와 컴퓨터 운영 체제(S/W) 사이의 데이터의 흐름을 관리한다.
-  CMOS의 설정 값들을 변경 가능하다.
-  BIOS는 요즘 UEFI로 대체되었다.

#### POST(Power-on self-test)  
- BIOS에서 Power를 켜자마자 주변장치들을 검사하는 과정
- BIOS가 POST를 하고 있을 때, Log Message가 출력됨

#### UEFI(Unified Extensible Firmware Interface)(통합 확장 펌웨어 인터페이스)  
- BIOS를 대체하는 펌웨어 규격.

### 임베디드 부팅  
#### U-Boot(Universal Boot Loader)이란  
- 임베디드 리눅스 개발에 **가장 많이 쓰이는 OpenSource Bootloader**
- 리눅스, Android 및 다른 운영 체제를 실행하는 임베디드 시스템의 부팅 프로세스를 관리
- 특징
  - 포팅 가능성
  - 부트로더 역할
  - 디버깅 및 테스트
  - 네트워크 부팅 등등

### Device Driver  
- 특정 하드웨어나 장치의 입출력을 제어하기 위해 커널의 일부분으로 동작하는 컴퓨터 소프트웨어
- Software Interface를 통해 Application이 H/W Spec을 이해하지 않아도 되는 장점
**필요성**
  - 커널에서 동작할 수 있는 커널 모듈 형식의 디바이스 드라이버를 개발 동작 중인 커널에 적재(insmod)하여 테스트를 한다.
  - 테스트 마다 배번 커널을 빌드한 필요가 없어서 개발 시간이 단축된다.
**커널 모듈(Kernel Module)** 이란
- 커널 내부에 삽입될 수 있는 Build된 Binary 파일
  - .ko 확장자, insmod/rmmod를 사용해 커널에 삽입/제거 할 수 있다.
**디바이스 파일의 필요성**
- App은 Kernel안에서 동작 중인 디바이스 드라이버에 직접 접근이 불가하다!
  - 그래서 Device Driver와 연결된 디바이스 파일을 만들고 App이 장치 파일에 신호를 보내서
    Device Driver가 H/W를 제어하도록 한다.
    
**Device Driver의 종류**
1. chrdev : 캐릭터 디바이스 드라이버
   - Byte 단위로 값 전달
   - 일반적인 임베디드 장치에 사용
2. blkdev : 블록 디바이스 드라이버
   - kb 이상의 '블록' 단위로 값 전달
   - Disk 장치에 사용되는 디바이스 드라이버
3. netdev : 네트워크 디바이스 드라이버
   - socket을 열고 ioctl이라는 System call로 장치를 제어

## 디바이스 드라이버 실습  
- insmod : [영어이름] 출력
- rmmod : [SSAFY embedded] 출력
**Build Code**
```
make
sudo insmod geonhee.ko
sudo rmmod geonhee
```
![image](https://github.com/kghees/Embedded_Linux_kernel-programing/assets/92205960/92a348a9-c786-4540-aaed-d375c4c24c22)
