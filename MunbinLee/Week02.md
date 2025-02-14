## 기간
**24.11.25 ~ 24.12.01**

---

## 사지방 컴퓨터에 관한 연구 기록
하모니카 OS에 설치되어 있는 크로뮴 브라우저는 2019년 버전이어서 많은 웹사이트, 확장 프로그램과 호환이 잘 되지 않았다.  

루트 권한이 없는 사지방 컴퓨터 특성을 고려했을 때, 크로뮴을 업데이트하는 것보다 새로운 브라우저를 사용하는 것이 좋은 것 같았다.

크로뮴 계열이 아닌 브라우저는 사실상 파이어폭스 밖에 없기 때문에 파이어폭스를 설치하여 사용하고 있다.  

설치 방법을 여기 올리면 국방부가 막을 것 같으므로 생략하겠다.

그리고 터미널을 실행할 일이 있을 때마다 vscode를 키는데, 사지방 컴퓨터에게는 살짝 무거워서 나만의 터미널 프로그램을 만들려고 시도 중이다.

원래 KDE Konsole을 설치하려고 했는데,

KDE Konsole을 설치하려면...

- 다른 사람들은 apt로 딸깍 설치하면 되므로 설치 방법에 대해 관심을 가지는 사람이 없음

- - 빌드하려면 extra-cmake-modules를 설치해야 함

- - - 다른 사람들은 apt로 딸깍 설치하면 되므로 설치 방법에 관심을 가지는 사람이 없음

- - - - 빌드하려면 cmake를 설치해야함

- - - - - 다른 사람들은 apt로 딸깍 설치하면 되므로 설치 방법에 관심을 가지는 사람이 없음

시도하다가 화병이 걸릴 것 같아 그냥 직접 만들어보려 한다.

QT Creator 4를 사용하여 만들 예정인데, 너무 마이너한 프로그램이라 정보가 너무 없어서 좀 걸릴 것 같다.

---

## 러스트와 소유권 시스템

Week01에서 언급했듯, 러스트는 메모리 안정성이 보장된 언어이다.  

메모리 안정성에 큰 기여를 하는 것이 바로 소유권 시스템이다.

(정수, char, bool 등의 타입에는 적용되지 않는다. 이유는 나중에 서술)

소유권 시스템에는 세 가지 원칙이 있다.

1. 각 값에는 그 소유권을 보유한 소유자가 있다.
2. 각 값에는 한 번에 한 개의 소유자만이 존재한다.
3. 소유자가 범위(스코프)를 벗어나면 값은 파기된다.

예시를 통해 이해하여보자.

```Rust
// 메모리가 확보되고, s1이 소유권을 지닌다. (1번 원칙)
let s1 = String::from("Hello");

// s1의 소유권이 s2로 이동한다. (2번 원칙)
let s2 = s1;

// s1은 소유권을 잃었으므로 컴파일 타임 에러가 발생한다.
println!("{}", s1);
```

다른 언어에서는 대입 연산자가 복사를 담당하지만 러스트에서는 이동을 담당한다.

만약 값을 복사하여 다른 곳에서 사용하고 싶다면

```Rust
let s2 = s1.clone();
```

이렇게 2개의 메모리 영역을 가진 2개의 값과 2개의 소유자를 만드는 방식으로 처리해야한다.<br><br>

3번 원칙은 언뜻 보면 당연한 소리 같아보이지만 1번, 2번과 조합되면 골때리는 규칙이 된다.

```Rust
fn main() {
    let s = String::from("Hello!");
    my_println(s);

    // 컴파일 타임 에러 발생
    println!("{}", s);
}

fn my_println(s: String) {
    println!("{}", s);
}
```

함수를 호출할 때 소유권이 s에서 함수로 넘어가버린다.  

그 후 함수가 종료되면서 3번 원칙에 의해 메모리가 파기된다.<br><br>

이를 방지하려면 코드를 이런 식으로 짜야된다.

```Rust
fn main() {
    let mut s = String::from("Hello!");
    s = my_println(s);

    println!("{}", s);
}

fn my_println(s: String) -> String {
    println!("{}", s);
    s
}
```
함수를 호출하면서 s의 소유권이 함수에게로 넘어가지만 함수가 다시 s에게 소유권을 넘겨주기 때문에 이 코드는 정상적으로 실행된다.<br><br>

객체를 사용하는 모든 함수를 이런 식으로 작성하게 된다면 mut을 사용하는 것도 문제지만 엄청나게 번거로울 것이다.  

그래서 러스트는 소유권을 빌리는 시스템을 만들었다.

```Rust
fn main() {
    let s = String::from("Hello!");
    my_println(&s);

    println!("{}", s);
}

fn my_println(s: &String) {
    println!("{}", s);
}
```

& 연산자로 값을 빌리는 참조자임을 나타낼 수 있다.

이렇게 하면 소유권이 일시적으로 이동하긴 하지만 함수가 종료되면 원래 소유자에게로 소유권이 돌아가기 때문에 정상적으로 실행된다.<br><br>

```Rust
fn main() {
    let mut s = 123;
    x2(&mut s);
    println!("{}", s); // 246
}

fn x2(num: &mut i32) {
    *num = *num * 2;
}
```

C의 포인터처럼, 러스트에서도 *로 포인터의 실젯값에 간섭할 수 있다.<br><br>

println!()이 함수가 아니라 매크로인 이유도 소유권 시스템 때문이다.

함수라면 실행할 때마다 소유권이 이동하기 때문에 참조자를 사용해야해서 불편할 것이다.

---

## 러스트와 구조체

러스트에는 클래스가 없다. 대신 구조체(struct)가 있다.

단순히 이름만 다른 것은 아니고, 클래스 상속이 불가능하다는 특징이 있다.<br><br>

```Rust
struct Body {
    weight: i32,
    height: i32,
}

impl Body {
    fn calc_bmi(&self) -> f64 {
        let h = self.height / 100.0;
        self.weight / h.powf(2.0)
    }
}
```
구조체에는 타입을 가진 필드 정의를 넣을 수 있다.

구조체의 메서드는 **impl 구조체명**으로 정의할 수 있다.  

방금 전 러스트에는 클래스 상속이 없다고 했는데, 그렇다면 공통된 메소드는 어떻게 처리해야할까?

---

## 러스트와 트레잇

트레잇(Trait, 특성)을 통해 다른 구조체에 대한 공통된 메서드를 구현할 수 있다.

자바나 C#의 인터페이스와 유사한 기능이다.<br><br>

가령, 정사각형과 원이 있는데, 둘 다 넓이를 구하는 메소드를 필요로 한다면

```Rust
trait Shape {
    fn get_area(&self) -> f64;
}

struct Square {
    side: f64,
}

struct Circle {
    radius: f64,
}

impl Shape for Square {
    fn get_area(&self) -> f64 {
        self.side * self.side
    }
}

impl Shape for Circle {
    fn get_area(&self) -> f64 {
        self.radius * self.radius * 3.14
    }
}
```

이런 식으로 구현할 수 있다.

---

## 그 외...

제네릭, 반복자, 패턴 매칭 등의 시스템에 대하여 알게 되었음

흠... 제네릭이 굳이 필요한가... 했는데 러스트는 함수 오버로딩이 없어서 공부해야할듯 아직 완벽한 이해는 못함

정수, char, bool 등의 기본형 타입에 대하여 소유권 시스템이 적용되지 않는 이유는 이 타입들은 사이즈가 컴파일 타임에 정해져있어서 힙 메모리 대신 스택 메모리에 넣을 수 있고, 그에 따라 겁나게 빠르기 때문이다.