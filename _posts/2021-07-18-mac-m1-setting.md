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
    - intel

    https://wannabewize.tistory.com/189


https://www.lainyzine.com/ko/article/how-to-install-homebrew-for-m1-apple-silicon/


### 2. react-native
apple silicon에서 rosetta를 사용하지 않고 react native를 빌드하는 방법[^1]
* clean build
- test

---
{: data-content="troubleshooting"}

This article has been discussed here:
- [lobste.rs](#)
- [/r/webdev](#)

Feel free to reach out at my email to leave feedback and talk about the article.

---
{: data-content="footnotes"}

[^1]: [react-native-m1](https://github.com/aiba/react-native-m1)