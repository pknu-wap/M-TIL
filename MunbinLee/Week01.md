## 기간
**24.11.18 ~ 24.11.24**

## 서론
어느덧 입대한지 150일 정도 지났다.  
그동안 아무것도 안 한 것은 아니지만, 구체적인 목표를 정하고 실행한 것이 없어 하루하루를 비효율적으로 사용하는 것처럼 느껴졌다.  
문득 성우가 같이 TIL을 하자고 했던 리포지토리가 떠올라 이제부터라도 목표를 구체화하기로 했다.  
<br>

목표는 총 5가지이다.
1. 컴퓨터활용능력 1급
2. 정보처리기능사
3. 만들면서 배우는 러스트 프로그래밍 완독
4. 전역 전까지 개인 프로젝트 완성
5. 티스토리 블로그 개편  
<br>

## 컴퓨터활용능력
부대에 컴퓨터를 잘 다루는 사람이 없어 얼떨결에 유사 행정병(훈련은 훈련대로, 행정은 행정대로... ◠̈)이 되었다.  
엑셀을 체계적으로 학습하고 싶어 컴퓨터활용능력 1급을 준비하려한다.  
<br>

## 정보처리기능사
군대에서 수수료 할인, 부대 내 응시, 포상휴가 등의 혜택을 누릴 수 있기 떄문에  
전역 전까지는 취득하는 것을 목표로 잡았다.  
<br>

## 러스트
최근 사지방 컴퓨터가 하모니카(데비안 계열 OS)가 설치된 컴퓨터로 교체되었다.  
처음에는 루트 권한도 없고 터미널도 없어서, 정말 되는 것이 거의 없어 화가 났다.  
이 쓰레기같은 컴퓨터를 욕하면서 연구하다가 생각보다 개발하기 좋은 환경이란 걸 깨달았다.  
왜 하필 Rust냐면, 메모리 안전성이 검증된 언어이기 때문에  
메모리를 관리할 일이 많은 게임계에서 어떻게든 써먹을 길이 있다고 생각했기 때문이다.  
윈도우 대비 설치 속도가 엄청 빠르기도 하고...  
<br>

## 개인 프로젝트
군대에 오기 전 프로젝트를 5개나 진행했지만, 애정을 가지고 끈질기게 유지보수 및 업데이트한 프로젝트가 없다.  
이유는 여러가지 있겠지만 대부분은 시간의 타이트함 때문이라고 생각한다.  
시간에 쫓기다보니 쓰레기같은 코드를 만들고, 업데이트하려고 코드를 보면 쓰레기 같아서 하기 싫어지고...  
다행히 내게는 1년 넘게 남은 시간이 있다.  
사지방 컴퓨터의 성능을 고려하면 GCP 같은 클라우드로 개발해야할 것 같다.  
<br>

## 티스토리
지금까지 티스토리에 글을 작성할 때 너무 딱딱하게 작성한 적이 많았다.  
백준 문제 풀이랍시며 글 몇 줄과 코드 덩어리로만 설명을 끝낸 적도 있고.  
PS 글을 모두 지운 후에 문제를 풀 때 떠올린 발상과 아이디어, 필요한 지식들을 정리해서 재작성하려한다.  
<br><br><br>

# 러스트 공부 시작!

하모니카와의 첫 만남은 충격적이었다.  
터미널도 없고, 루트 권한도 없고, 인터넷 속도도 느리고, 호환도 잘 안되고...  
지금도 깃허브 웹사이트가 호환이 안되어서 로컬 저장소에 클론한 후 깃허브 토큰을 발급받아 푸시하고 있다.  

그런데 vscode가 설치된 것을 보고 혹시나? 하면서 vscode에서 터미널을 열어보았다.  
결과는 성공이었다. 이게 왜 됨?  
곧바로 `dpkg-query -l` 명령어로 무슨 패키지가 설치되어 있는지 확인했다.  
gcc, g++, java, node, python 등 쓸만한 패키지가 많이 설치되어 있었다.  

며칠간은 C++로 PS를 하였으나 solved.ac, leetcode.com 이 호환이 잘 되지 않아 짜증이 났다.  
선택지가 얼마 없는 이 컴퓨터로 무슨 공부를 할까 고민하다 문득 러스트가 생각났다.  

`apt install rust` 로 간단하게 설치가 되면 좋았겠지만 상대는 루트 권한이 없는 하모니카다.  
그래서 홈페이지에 나와있는 방법인 `curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh` 로 설치를 시도했는데 실패했다.  
스크립트에서 PATH를 변경하는 권한이 없기 때문에 오류가 발생한 것이 아닐까?  
그래서 `curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- --no-modify-path -y` 로 설치를 성공하였다.  

매번 PATH를 설정하는 것도 귀찮기 때문에 설치 스크립트에 `echo PATH=\$PATH:\$HOME/.cargo/bin | xclip` 를 추가하여 PATH를 설정하는 명령어를 클립보드에 복사하도록 만들었다.  
이러면 설치 후에 마우스 휠 키만 딸깍 누르면 붙여넣기와 실행이 동시에 되기 때문에 편하다.  
<br>

# 만들면서 배우는 러스트 프로그래밍
<img src = "https://contents.kyobobook.co.kr/prvw/009/688/18/5800010968818/5800010968818001.jpg" width=30%>

The Rust Programming Language와 이 책 중 무엇을 살지 고민하다 이 책을 샀다.  
전자는 https://doc.rust-kr.org/ 에서 내용을 확인할 수 있기 때문이다.  

이 책의 특징은 파이썬 코드와 러스트 코드를 비교하며 설명한다는 것이다.  

```Python
print("Hello, World!");
```

```Rust
fn main() {
    println!("Hello, World!");
}
```

이런 식으로.  
이 짧은 예제를 통해 함수 키워드가 **fn** 이라는 것, 엔트리 포인트가 **main** 함수라는 것, 출력은 **println!** 으로 한다는 것과 ;이 필요하다는 것을 알 수 있다.  
**println!** 처럼 뒤에 !가 붙은 것은 함수가 아니라 매크로를 나타낸다.  
print, printf, println, cout 등 다른 언어가 출력에 함수를 사용하는 것을 생각하면 굉장히 이질적이다.  
이유는 아직 모르겠고, 어쨌든 매크로를 통해 함수가 할 수 없는 복잡한 일을 처리할 수 있다.  
<br><br>

```Rust
let banana = 300; // i32

let apple : i32 = 400;
apple = 500; // error: cannot assign twice to immutable variable

let mut grape : i32;
grape = 600;
grape = 700;

let mut orange = 800; // warning: variable does not need to be mutable
```

러스트에서 변수는 **let** 키워드를 사용하여 정의할 수 있다.  
타입추론이 가능하며, 기본적으로 불변적이다.  
**let mut** 키워드로 가변 변수를 만들 수 있다.  
가변 변수는 초깃값을 생략할 수 있지만, 생략할 경우 타입을 직접 지정해야한다.  
깐깐한 러스트 컴파일러는 가변 변수를 만든 후 값을 변경하지 않는 것조차도 경고를 뱉는다.  
<br><br>

```Rust
// 1부터 100까지 FizzBuzz 문제 풀기
fn main() {
    for i in 1..101 {
        if i % 3 == 0 && i % 5 == 0 {
            println!("FizzBuzz");
        } else if i % 3 == 0 {
            println!("Fizz");
        } else if (i % 5 == 0) { // warning: unnecessary parentheses around `if` condition
            println!("Buzz");
        } else {
            println!("{}", i);
        }
    }
}
```

C와 파이썬을 섞은 듯한 문법이다.  
[start, end) 범위를 **start..end** 문법으로 나타낼 수 있고, (std::ops::Range Struct)  
**for *loop_variable* in *Iterator*** 키워드로 범위를 순회할 수 있다.  
특이하게, 조건을 괄호로 감싸는 C와 달리 조건을 괄호로 감싸면 오히려 경고를 뱉는다.  
<br><br>

![](https://upload.wikimedia.org/wikipedia/commons/thumb/2/2b/Caesar3.svg/320px-Caesar3.svg.png)

알파벳을 3글자씩 밀어서 암호화하는 시저 암호를 만들어보자.  

```Rust
fn encrypt(text: String) -> String {
    let mut result = String::new();

    for ch in text.chars() {
        if 'A' <= ch && ch <= 'Z' {
            let ord = (ch as u8 - 'A' as u8 + 26 + 3) % 26 + 'A' as u8;
            result.push(ord as char);
            continue;
        }
        result.push(ch);
    }

    result
}

fn main() {
    let mut line = String::new();
    std::io::stdin().read_line(&mut line).unwrap();
    println!("{}", encrypt(line));
}
```
**String** 은 힙에 데이터를 저장하는 문자열 객체이다. C++의 std::string과 비슷하다.  
함수의 패러미터와 리턴 값의 타입은 직접 입력해야한다.  
문자열의 각 문자는 String::chars()를 통해 순회할 수 있다.  
C와 달리 char과 정수는 호환이 되지 않으므로 **as u8 *(unsigned 8비트 정수)*** 을 통해 강제로 형 변환을 해야한다.  
**return result;** 대신 **result**로 표현할 수 있다.  
처음에는 이게 단순히 return과 ;를 생략한 syntactic sugar인 줄 알았는데,  
이것을 응용해서 `let var = if condition_a {var_a} else {var_b}` 처럼 삼항 연산자로 사용하는 등의 활용이 가능하다는 것을 알았다.  
<br>

러스트는 파이썬의 람다 함수와 비슷하게, 익명 함수를 사용할 수 있다.  
이를 클로저라 한다.

**let *closure_name* = |*parameter*| definition;**  
<br>

```Rust
fn encrypt(text: String) -> String {
    let is_alpha = |ch| 'A' <= ch && ch <= 'Z';
    let convert = |ch| ((ch as u8 - 'A' as u8 + 26 + 3) % 26 + 'A' as u8) as char;
    let encrypt_char = |ch| if is_alpha(ch) {convert(ch)} else {ch};
    text.chars().map(|ch| encrypt_char(ch)).collect()
}
```
클로저를 사용하여 시저 암호를 더욱 간편하게 구현할 수 있다.
