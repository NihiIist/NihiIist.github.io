---
layout: post
category: memo
---

m1 mac mini를 새로 구입하면서 셋팅한 개발 환경 정리하였다. silicon mac은 처음 사용하기 때문에, 기존 사용하던 intel mac과 상이하게 구성해야 했던 부분만을 기록한다.
apple silicon mac 환경 셋팅에 관한 구글링 시, 대부분의 문서가 workaround로 rosetta로 app(terminal, xcode 등)을 사용하는 방법만은 안내하고 있다.
rosetta를 사용하지 않고 싶지 않았기 때문에, rosetta로 terminal을 두 벌 가져가는 우회 방안을 사용하지 않고 mac mini silicon에 개발 환경을 구성한 내용을 정리하였다.

---
{: data-content="environment"}

- m1 silicon mac mini + bigsur
- python 3.7.x
- docker
- ios

---

### 1. python 3.7
m1 mac bigsur에서 python 3.7을 지원하지 않음. 해당 python 버전만을 intel homebrew로 설치하여 우회. python 버전관리는 pyenv + virtualenv 사용

- homebrew
    - apple silicon
        - /opt/homebrew 에 설치됨(brew --prefix 명령어로 설치 위치 확인 가능)
        > /bin/bash \-c "$(curl \-fsSL [https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh](https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh))"
        - eval "$(/opt/homebrew/bin/brew shellenv)" 로 쉘에 brew관련 환경변수 적용(~/.zshrc에 추가)
    - intel
        - /usr/local/homebrew 에 설치됨. rosetta2로 동작
        > arch -x86_64 /bin/bash \-c "$(curl \-fsSL [https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh](https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh))"
        - alias 적용
        > alias ibrew='arch -x86_64 /usr/local/bin/brew'

- python 3.7
    - m1 bigsur에서 python3.7을 공식적으로 지원하지 않음
    - intel homebrew로 설치(3.7.11) 
    > ibrew install python@3.7

- pyenv
    - silicon으로 설치
        > brew install pyenv
    - pyenv는 PYENV_ROOT(default는 $HOME/.pyenv)안의 shims에 존재하는 python executable이 python, pip등의 python관련 명령어를 가로채는 방식으로 버전 관리
    - 따라서 ~/.pyenv/shims가 PATH의 가장 앞에 위치하면 됨. pyenv 버전 관리에 오류가 있을 경우, 해당 사항부터 체크
    - shims enable 명령어는 "pyenv init -" 하나로 충분함.
        > echo 'eval "$(pyenv init -)"' >> ~/.zshrc
    - python 3.7 버전관리를 위해 ~/.pyenv/versions 에 3.7.x폴더를 생성하고 /usr/local/lib 에 설치된 python@3.7.x로 symbolic link를 걸어준다. 
    - 버전관리 확인
        > pyenv local 3.7.x

        > python3 -V, python -V
    - 버전 적용이 올바르게 안 될 경우, .../python@3.7.x/bin 의 pip3, python3, python, pip 에 sym link 알맞게 걸어주어서 해결 

- virtualenv


### 2. react-native
apple silicon에서 rosetta를 사용하지 않고 react native를 빌드하는 방법[^1]
* clean build
- test

- running on device
    - usb연결 후, open .xcworkspace(CocoaPods쓸 경우)
    - Targets > Signing & Capabilities 에서 Team 등록
    - build 

---
{: data-content="troubleshooting"}

- react-native build
    - undefined symbol ... for arm64(swift관련 library 에러)
        - xcode build settings > Search Paths > Library Search Paths 모두 삭제
    - react-vector-icons error
        - build phases 에서 Copy Bundle Resources 모두 삭제 
- react-native running on device
    - build할 때, Codesign wants to access key "access" in your keychain...팝업 창 뜰 경우
        - KeyChain Access app에서 Cumstom Keychains > Apple Development key에 대한 password
        - 별도로 설정하지 않았을 경우, password없음. password입력하지 않고 ok눌러서 진행
    - errors were encountered while preparing your device for development. please check the devices and simulators window.
        - iphone 재시동
    - device(iphone)에서 신뢰할 수 없는 App개발자 팝업창 뜰 경우
        - 설정 > 일반 > 기기관리 > 해당 App 신뢰함 터치

Feel free to reach out at my email to leave feedback and talk about the article.

---
{: data-content="footnotes"}

[^1]: [react-native-m1](https://github.com/aiba/react-native-m1)