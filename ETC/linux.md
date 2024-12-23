# 리눅스


### 리눅스 배포판

1. 데비안 계열
    - 데비안: 커뮤니티 데비안 프로젝트에서 개발하고있음. 자유도는 높지만 설정이 까다로워서 진입장벽 높음.
    - 우분투: 남아공 출신 사업가 마크 셔틀워스가 Canonical 이라는 회사를 설립하고, 데비안 계열 우분투를 개발함.
3. 레드햇 계열
    - 레드햇: Red Hat사(2019년에 IBM에서 인수)에서 redhat linux 9이후로 무료버전은 따로 배포하지않고, 유료버전인 RHEL(Red Hat Enterprise Linux)만 배포 시작함. 유료버전이지만, 코드는 공개되어있음.
    - 페도라: 레드햇 기반의 무료 배포판, 신기능은 페도라에 먼저 시험하고, 안정화되면 레드햇으로 들고옴
    - CentOS: RHEL의 대표적인 클론 리눅스, RHEL의 코드를 그대로 컴파일해서 무료배포
    - Rocky Linux: CentOS 8을 2020 마지막으로 지원하지않겠다고 하자, CentOS 원년 개발자중 한명이 CentOS 대체하는 리눅스 개발 프로젝트 진행
4. openSUSE
5. 아치(Arch) 계열
6. 등등...

### 리눅스 배포판 별 패키지 관리기법

1. 데비안
    - DPKG(debian pakage)
     + 오프라인 패키지 관리 툴
     + 파일형태: *.deb
    - APT(apt-get, advanced packaging tool get)
      + dpkg의 의존성 문제를 해결한 도구(특정 패키지를 설치할때 의존성이 있는 다른 패키지를 자동으로 설치함)

2. 레드햇
   - RPM(Redhat Package Manager)
     + 오프라인 패키지 관리 툴
     + 파일형태: *.reb
   - YUM(Yellowdog updator Modified)
      + RPM의 의존성 문제를 해결한 도구
   - DNF(Dandified yum)
      + yum의 고질적인 문제를 해결하여 성능을 높인 도구

3. openSUSE
   - YaST(Yet another Setup tool)
   - zypper






