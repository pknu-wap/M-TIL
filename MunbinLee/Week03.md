## 기간
**24.12.02 ~ 24.12.08**

---

![](https://i.imgur.com/dDaIB4r.png)

2024.12.03 ~ 2024.12.04 Nothing happened.

---

이번 주는 공부보다는 환경 세팅에 힘을 주었다.

일단 저번 주에 언급했던 QT4로 터미널 만들기는 실패했다.

생각보다 품이 너무 많이 들어 다른 방법을 찾아보았다.<br><br>

첫번째는 Rust로 작성된 Termie를 포크하기.

Rust 공부를 덤으로 할 수 있어 좋을 것 같다.

다만 기능이 많이 있는 프로그램은 아니라 수정할 부분이 좀 많을 것이다.

둘째는 Sublime Text의 TerminalView 플러그인 포크하기.

어쨌든 vim을 사용할 것이 아니라면 텍스트 에디터를 사용하기는 해야하므로

Sublime Text를 사용하면서 플러그인으로 터미널을 켜는 것이다.

기능은 풍부한데 플러그인이 파이썬으로 작성되어있는 것이 문제다.<br><br>

그 외 여러가지 시행착오를 겪으면서 어떻게 세팅해야 더 좋은 능률을 뽑아낼 수 있을지 고민했다.

- vscode

    vscode와 인터넷 브라우저를 같이 키면 매우 높은 빈도로 프리징이 발생한다.

    혹시나 vscode가 구버전이라 호환 문제가 발생하는건가 싶어 vscode를 업데이트하였다.

    루트 권한이 없어 apt 딸깍으로 설치는 못하고 .deb 파일을 다운받아 실행하였다.

    실행 자체는 성공하였지만 호환이 되지 않는 것인지 터미널이 안 켜진다...

    vscode는 이제 완전히 버려야겠다.

- Rust

    분명 Week01에는 ~/.bashrc 파일에 접근할 수 있는 권한이 없었는데 지금은 또 된다.

    PATH를 수동으로 변경하는 부분을 제거하고, 설치 완료시 zenity로 알림이 뜨도록 하였다.

    ```zenity --notification --window-icon="info" --text="Rust 설치 완료!"$(curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y && source ~/.bashrc)```

- Sublime Text

    패키지 설치 없이도 Rust 문법 하이라이팅을 지원하고 또 가볍기 때문에 앞으로 많이 쓸 것 같다.

    ```cd /tmp && [ -d sublime ] && sublime/opt/sublime_text/sublime_text || (mkdir sublime && cd sublime && wget https://download.sublimetext.com/latest/stable/linux/x64/deb && dpkg -x * . && opt/sublime_text/sublime_text)```

- 그 외 할 수 있는 것들

    .deb 파일 설치  
    압축된 빌드 파일 설치  
    rust cargo로 빌드하기

- 할 수 없거나 힘든 것들

    QT4 만지기  
    cmake로 빌드하기 (cmake 패키지는 설치되어있지만 느리고 호환이 잘 안 된다.)  
    C++ 20 이상 지원하는 g++ 설치  
    파이썬 모듈 설치하기 (RustPython을 설치해서 어찌저찌하면 가능할수도)  
    sh 파일 단독 실행 (실행은 가능한데, &&로 인해 길어지면 zenity 명령이 안 먹힌다. 위에서 Rust 설치할 때 $()로 설치한 이유도 이 때문)  
    wine 설치  
    러스트로 PS하기 (하면 혈압 오름...)  

<br><br>
다음 주 목표는 만들면서 배우는 러스트 프로그래밍 완독!