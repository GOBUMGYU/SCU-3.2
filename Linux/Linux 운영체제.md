## 리눅스 운영체제

### 시스템 프로그래밍

운영체제와 같은 커널 및 핵심 라이브러리를 직접 사용하여 하위 레벨에서 동작하는 시스템 소프트웨어를 프로그래밍하는 기술

**리눅스란 ?**

1991년 리누스 토르발스가 처음 출시한 운영체제 커널인 리눅스 커널에 기반을 둔 오픈 소스 유닉스 계열 운영체제 계열

**리누스 배포판**

- 리눅스는 일반적으로 리눅스 배포판 안에 패키지 처리됨
- 데비안, 페도라, CentOS, 우분투 등이 있음

**CentOS8 리눅스**

- 업스트림 소스인 레드햇 엔터프라이즈 리눅스의 소스 코드를 그대로 가져와서 빌드함
- 레드햇 엔터프라이즈 리눅스와 완벽하게 호환되는 무료 기업용 컴퓨팅 플랫폼을 제공함

**GNU프로젝트**

모두가 공유할 수 있는 소프트웨어를 만드는 것을 모티브로 리차드 스톨만에 의해 시작됨

**리눅스 시스템 구성 요소**

**리눅스 운영체제 : 3개 요소로 구성 (커널, 셀, 사용자 프로그램)**

![image](https://user-images.githubusercontent.com/106207558/231195965-3116c68f-b54a-45d3-9c01-d1e1cb07a8d9.png)


**커널 : 명령어를 받아서 그것을 가지고 하드웨어를 직접 제어해주는 것**

- 1991년 리눅스 토발즈에 의해 생긴 용어
- 명령어를 받아 해당 작업을 수행하는 기능
- 커널 업그레이드(또는 커널 컴파일)를 통해 최신 버전 유지

**셸**

- 사용자와 운영체제 내부(커널)사이 인터페이스를 감싸는 층
- 명령 줄 인터페이스 CLI와 그래픽 사용자 인터페이스 GUI를 제공
- 커널이 수행하는 작업은 실제로 눈으로 보이지 않지만 그 결과값이 셸에 의해 사용자가 볼 수 있는 언어로 번역되어 화면에 출력

**셸의 의미**

운영체제 상에서 다양한 운영체제 기능과 서비스를 구현하는 인터페이스를 제공함

- 사용자와 운영체제의 내부(커널) 사이에서 명령을 해석하는 역활을 함
- 일반적으로 명령줄과 그래픽 형의 두 종류로 분류 됨

**리눅스 시스템의 구성 요소**

**셸의 역활**

- 대화식(Interactice) 사용
    - 사용자의 요청을 기다려서 요청 즉시 결과 값을 출력해주는 대화형 구조
- 프로그래밍
    - 복합적인 작업을 수행할 수 있도록 일련의 명령어들을 묶어서 사용
- 리눅스 셰션(Session)의 설정(Customization)
    - 리눅스의 세션에 대한 변수들을 정의해서 사용자가 리눅스 환경을 자신이 원하는 상태로 설정

**리눅스 시스템의 특징**

- 독립된 플랫폼을 갖는 운영체제
- 빠른 업그레이드와 강력한 네트워크 지원
- 다중 작업과 가상 터미널 환경 지원
- 유닉스와 리눅스의 완벽한 호환
- 공개형 오픈 소스의 운영체제
- 다중 사용자 환경 지원
- 저사양 컴퓨터도 서버 구축 가능

**UID와 GID키워드**

**UID : 사용자의 ID를 구별**

**GID : 그룹의 ID를 구별**

**강력한 네트워크 지원**

- 리눅스는 강력한 네트워크를 지원하는 운영체제로, 클라이언트 프로그램 지원 뿐만 아니라 서버 기능도 제공함

다중 작업과 가상 터미널 환경지원

다중 작업(Multi-Tasking)

동시에 여러 작업을 처리

가상 터미널(Virtual Terminal)

하나의 모니터에 여러 개의 가상 화면을 두는 기능

유닉스와 리눅스의 완벽한 호환

완벽한 호환성이라고 해서 실제로 유닉스 코드를 리눅스에서 사용할 수 있는 것은 아님

다만, 프로그램을 개발하는 경우가 아니라면 유닉스에서 사용하는 프로그램 등을 별도의 수정 없이도 리눅스에서 사용할 수 있음을 의미

공개형 오픈 소스의 운영체제

비공개형 Windows와 달리 소스가 공개되어 있어 누구든지 사용할 수 있다.

누구나 소스를 변형.개발.재배포할 수 있다는 특징이 있다.

그 외의 특징

- 많은 작업을 동시에 수행 할 수 있으면서도 저렴한 비용
- 구형 컴퓨터에서도 리눅스 운영체제를 효율적으로 사용가능
- 저급사양의 개인용 컴퓨터에서도 서버 구축 가능

**정리**

운영체제란 처리하고자 하는 과정을 일련의 작업순서로 정하고 중앙처리장치(CPU)와 주기억장치(RAM), 컴퓨터 주변장치(키보드,모니터,마우스 등) 등 여러 하드웨어 시스템에 일련의 작업을 할당하는 시스템

### 운영체제를 사용하는 목적

기계장치인 하드웨어를 사용할 수 있도록 기반을 조성함

하드웨어 단말기를 구동하게 하기 위해서는 운영체제 설치가 필수임

응용프로그램 ↔ 운영체제 ↔ 장치드라이버 ↔ 하드웨어

운영체제의 역활

![image](https://user-images.githubusercontent.com/106207558/231196058-836743ee-961a-4c37-b003-e2ddce1436d6.png)


**가상머신 (VM : Virtual Machine)**

컴퓨팅 환경을 소프트웨어로 구현한 것, 즉 컴퓨터 시스템 에퓰레이션(가상현실화)하는 소프트웨어

가상머신 프로그램 기존 운영체제 안에 가상의 컴퓨터를 만들어 운영체제를 설치하여 운영할 수 있도록 제작된 프로그램

**가상 머신 프로그램의 종류**

VMware Player - 리눅스

Virtual 컴퓨터 - 리눅스

Hyper-V - 윈도우

Virtual Box

**Vmware Player 특징**

무료 버전으로 제공되는 소프트웨어임

스냅숏, 클론, 보안 등의 기능은 제외된 버전임 ( 유료버전에서는 가능 )


