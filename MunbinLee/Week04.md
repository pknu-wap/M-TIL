## 기간
**24.12.09 ~ 24.12.15**

Rust 공부를 하던 중 문득 그리운 어떤 분이 생각나서 웹 해킹 공부를 시작하였다.

---

# 쿠키 취약점

HTML 프로토콜의 특징인 Connectionless, Stateless 때문에 HTTP에서는 특정 상태를 유지 및 기록할 수 없다.

이를 보완하기 위해 클라이언트에 쿠키(Cookie)를 발급하여 상태를 기록한다.

https://dreamhack.io/wargame/challenges/6

```py
username = request.cookies.get('username', None)
if username:
    return render_template('index.html', text=f'Hello {username}, {"flag is " + FLAG if username == "admin" else "you are not admin"}')
```

쿠키는 이용자가 임의로 조작할 수 있기 때문에, 서버에서 검증 없이 신뢰하면 안된다.

위 코드는 쿠키만으로 이용자의 정보를 식별하는 취약점을 가지고 있다.

콘솔에 document.cookie='username=admin'; 을 입력하면 플래그를 얻을 수 있다.

이 취약점은 인증 정보를 세션으로 저장하고, 세션에 해당하는 랜덤한 키를 쿠키에 저장하여 막을 수 있다.<br><br><br>

# XSS

XSS는 Cross Site Scripting의 약자(스타일시트와 구분하기 위해 XSS로 부른다)로, 공격자가 웹 리소스에 스크립트를 삽입하는 클라이언트 사이드 취약점이다.  

https://dreamhack.io/wargame/challenges/28/

```py
param = request.args.get("param", "")
return param
```

위 코드는 이용자가 param 파라미터로 입력한 값을 그대로 출력한다.

이 코드의 문제점은 이용자가 파라미터로 텍스트뿐만 아니라 스크립트도 넣을 수 있다는 것이다.

파라미터를 `<script>alert(1)</script>`로 설정하면 페이지 접속 시 1이라는 메시지가 뜬다.

이를 통해 이 페이지가 임의 코드 실행이 가능한 XSS 취약점을 가지고 있음을 확인할 수 있다.

플래그 정보를 쿠키로 가지고 있는 이용자가 `~param=<script>location.href='/memo?memo='+document.cookie</script>` 페이지에 접속하면 이용자의 쿠키를 탈취하여 플래그를 얻을 수 있다.


이 취약점은 입력 정보를 필터링하여 막을 수 있다.<br><br><br>

# CSRF

CSRF는 이용자를 동의하지 않은 작업을 수행하게 만드는 공격이다.

예를 들어, https://github.com/delete-account 에 접속하면 아무런 절차 없이 깃허브 계정이 탈퇴된다고 하자.

[전국민 재난지원금 100,000원 바로 받기](https://github.com/delete-account) 따위로 이용자를 속여서 접속하게 만든다.

이용자의 쿠키에 로그인 정보가 있을 경우 그 계정이 탈퇴된다.

https://dreamhack.io/wargame/challenges/26

XSS 취약점처럼 `<script>location.href='https://github.com/delete-account'</script>`와 같은 스크립트를 실행시킬 수도 있겠지만

이 문제에서는 `<script>` 태그가 막혀있다.

따라서 `<img src = 'https://github.com/delete-account'>` 와 같은 코드를 입력하여 플래그를 탈취한다.

XSS와 CSRF 모두 클라이언트 사이드 취약점이고, 이용자를 악성 스크립트 페이지에 접속하도록 유도한다.

XSS는 세션 및 쿠키 탈취를 목적으로 하고, CSRF는 이용자가 임의 페이지에 HTTP 요청을 보내는 것을 목적으로 한다.<br><br><br>

# SQL 인젝션

```SQL
SELECT * FROM users WHERE userid="{userid}" AND userpassword="{userpassword}"
```

위 코드를 통해 아이디와 패스워드에 맞는 계정 정보로 로그인한다고 하자.

아이디와 패스워드를 정상적으로 입력할 경우는 문제되지 않겠지만

만약 유저가 아이디에 `admin"--` 을 입력할 경우

```SQL
SELECT * FROM users WHERE userid="admin"--" AND userpassword="password"
```

admin 계정에 패스워드 없이 로그인할 수 있다.

굉장히 쉽게 익스플로잇을 시도할 수 있는 취약점이지만 매년 수십 건의 사고가 터질 정도로 위험하다.

이 취약점은 변수를 문자열로 컴파일하거나 입력값을 필터링하여 막을 수 있다.