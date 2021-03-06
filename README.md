# Study for Interview
---

## Table of Contents
- [Algorithm](#algorithm)
- [Data Structure](#data-structure)
- [Programming Language](#programming-language)
- [Database](#database)
- [Network](#network)
- [Operating System](#operating-system)
- [Web](#web)
- [iOS](#ios)
- [etc](#etc)

---

## Algorithm
- TBD
---

## Data Structure

### Hash란 무엇인가?
- 해시 테이블(hash table), 해시 맵(hash map), 해시 표는 컴퓨팅에서 키를 값에 매핑할 수 있는 구조인, 연관 배열 추가에 사용되는 자료 구조이다. 해시 테이블은 해시 함수를 사용하여 색인(index)을 버킷(bucket)이나 슬롯(slot)의 배열로 계산한다.
- ref: [https://ko.wikipedia.org/wiki/해시_테이블](https://ko.wikipedia.org/wiki/해시_테이블)


### Set, Array, Map을 설명하시오.
- List
  - 객체들이 들오온 순서대로 참조를 유지하기 위한 목적. 수집의 순서가 있으며, 동일한 데이터의 중복 입력이 가능. 순차적으로 대량의 데이터를 억세스하거나 입력할 때 유리한 방식.
- Map
  - Key & Value의 형태로 입력이 되며, 키 값을 입력하면 해당하는 value 값을 획득. 수집의 순서를 기억하지 않으며, 동일한 데이터를 Key값으로 사용할 수 없다. (물론 key값이 틀리고 value값이 동일한 건 가능.)다수의 데이터에서 원하는 특정 데이터에 접근할 때 유리한 방식.
- Set
  - 중복데이터를 불허하는 것을 제외하고는 큰 특징이 없습니다. 입력되는 당시의 순서에는 따르지 않으나... 순차적인 접근을 위해서는 Iterator로 접근하게 됩니다.
 

### Tree에서의 Pre-Order, In-order, Post-order 사용
- Pre-order: Used to create a copy of tree 
> Example: If you want to create a replica of a tree and need node values in an array and when you insert those values from index 0 to end in a new tree, you get a replica
- In-order: To get values of node in non-increasing order(Array로 소팅된다.)
- Post-order: When you want to delete a tree from leaf to root(ex. 메모리 해제시 댕글링 포인터 방지 위해 뒤에서부터 해제할 때)
 
---

## Programming Language

### Javascript
- Script 언어이므로 interpreter에 의해 실행된다.
- Object 기반의 언어이며 Single Thread이다.

#### Method Chaining이란, 어떻게 구현할지

### Node.js
- Chrome Javascript Engine V8 기반의 플랫폼
  - V8은 Google에 의해서 C++로 개발된 오픈 소스 자바스크립트 엔진
    - V8은 자바스크립트 코드를 인터프리터로 통역(interpret)하거나 중간 언어로 번역(compile)하는 기존의 방법 대신 각 코드를 실행하기 전 각 플랫폼에 최적화된 기계어로 번역하고 이를 캐시에 보관해 재사용한다. 그리고 외부로 드러나지는 않지만 가능한 경우 자바스크립트가 가진 동적 언어로서의 특징과 상반되는 형식 기반 멤버 바인딩을 내부적으로 사용한다.
- JavaScript를 compile하여 native machine code 변경 후 runtime시 다시 최적화하여 실행하는 구조.
- Garbage Collection을 통한 메모리의 효율적인 관리. ( memory leak는 개선의 여지가 있음 )
- Standalone 고성능 JavaScript 엔진으로 사용가능. 

- Single Thread 기반의 Non-Blocking I/O model 사용
  - 노드를 사용하는 가장 중요한 이유중 하나는 비동기형 방식이다.
  - 우선 Multi thread이란?
  ![Multi-thread](https://cloud.githubusercontent.com/assets/7614353/20128452/78c51038-a68b-11e6-8b26-3ff418da0bf2.png)
    - 동시에 Service할 수 있는 Client의 수는 Thread Pool안에 있는 가용한 Thread의 수와 동일
    - 일반적으로 Thread Pool안의 Thread는 500~2000. ( 2000을 넘는 경우는 거의 없다. )
    - 할당된 Thread가 IO작업( Network, File, DB )을 하게 되면 blocking 방식으로 처리되어 해당 Thread가 CPU를 사용하지 않는 상태(wait 상태)로 변환.
    - 즉, IO시간만큼 Thread는 blocking.

- Node.js 는 Single Thread로 구성되어 있다. 내부적으로는 Thread Pool 로 구성되어 있다.
 ![Non-Blocking I/O Model](https://cloud.githubusercontent.com/assets/7614353/20128262/3c0656c6-a68a-11e6-91d9-d11ad67cafb8.png)
  - 다양한 요인들이 결합된 데이터에 대한 통계적 분석 연산의 경우 다중 스레드 모델이 더 적합하다. 필요한 구간에 여러 개의 스레드를 배치해 시스템 자원을 최대한 활용하여 빠르게 연산을 완료하도록 설계할 수 있다.
  - 하지만 이와 같은 상황을 모든 프로그램이 맞닥뜨리는 것은 아니다. 요청에 대한 빠른 반응을 요구하는 네트워크 서버의 프로그램의 경우 단일 스레드 모델이 더 적합할 수도 있다. 하나의 스레드만 이용하는 방식은 다음과 같은 장점이 있다.
    - 자원 접근에 대한 동기화를 신경 쓰지 않아도 된다. 여러 개의 스레드가 공유된 자원을 사용할 경우 각 스레드가 원하는 결과를 얻게 하려면 공용 자원에 대한 접근이 통제되어야 하며 이 작업은 프로그래머에게 많은 노력을 요구하고 비용 또한 발생한다. 단일 스레드 모델에서는 이러한 작업이 필요 없다.
    - 문맥 교환(context switch) 작업을 요구하지 않는다. 문맥 교환은 여러 개의 프로세스가 하나의 프로세서를 공유할 때 발생하는 작업으로 많은 비용을 필요로 한다.

- Event-Based Asynchronous Pattern
  ![Processing model](https://cloud.githubusercontent.com/assets/7614353/20128535/fdc2d6bc-a68b-11e6-95c2-2e9ae0ff80da.png)
  - 비동기 동작의 과정과 결과를 이벤트로 통보하는 형식을 취하고 있다.
  - 비동기 작업이 시작되면 해당 작업의 진행 상황을 이벤트로 외부에 전달하는 기능을 포함하고 있으며, 해당 작업이 종료되면 마찬가지로 작업 종료 이벤트를 발생시키는 기능을 포함하고 있다.
- Ref: [Node.js - 노드 : 특징](http://posnopi13.tistory.com/28)

#### Node.js 특징
- 장점
  - 싱글스레드, 비동기 IO 처리에 기반한 빠른 속도(내부적으로는 Thread Pool 로 구성되어 있다.)
  - 파일 I/O나 네트워크 처리를 이벤트 드리븐 방식으로 처리하기 때문에 빠른 처리가 가능함
  - CPU의 대기시간을 최소화 할 수 있음
  - CPU 부하가 적고, 많은 커넥션을 동시에 처리해야 하는 구조에 적합
  - 자바스크립트를 이용해서 개발할 수 있기 때문에 프론트엔드 개발자의 진입장벽이 낮음
  - 기존 Java 서버에 비해 생산성이 높음
- 단점
  - 싱글스레드 모델이기 때문에 하나의 작업에 시간이 오래걸리면 시스템 전체의 성능이 급격하게 떨어짐
  - 이벤트 콜백 중심으로 코드가 중첩될 경우 가독성이 떨어짐
  - 에러가 발생할 경우 프로세스 자체가 죽어버리므로 주의해야 함(watch dog 등으로 처리 가능)
  - 세션을 공유할 경우 redis와 같은 부가적인 인프라가 필요함
  - Single thread 모델이기 때문에, 멀티 코어 머신에서 CPU 사용을 최적화할 수 없다는 문제가 있다. 하나의 쓰레드는 하나의 물리적 코어밖에 사용하지 못하기 때문제 코어가 많은 시스템이라도 성능이 올라가지 않는다 그래서 설계시, Cluster 모듈등을 이용하여, 하나의 서버에서 여러개의 노드 프로세스를 사용하는 모델을 가지고 가야함
  - V8 엔진을 기반으로 하는데, 이 V8 엔진은 Garbage collection  기반의 메모리 관리를 하기 때문에, GC시 CPU 사용률이 Spike를 치면서 순간적으로 서버를 멈추게할 수 있다는 문제점을 가지고 있다.
- 종합
  - 개발이 빠르고 쉬운 장점이 있지만 운영 과정의 어려움이 존재함
  - REST API 서버, Push 서버등에 사용해야 할 것 같음
- Ref: [node.js 의 장점과 단점](http://118k.tistory.com/197)


#### Node.js Single Thread 처리 방식, 장점, 어떤 경우에 안좋고 어떨때 좋은지


### C++

#### C++ Virtual Function
- 가상 메소드는 그 메소드를 호출하는 객체가 어떤 클래스인지에 따라 구현이 결정되는 메소드를 뜻한다.
- 자바의 경우, 정적 메소드를 제외한 모든 함수가 가상 메소드이며, C++의 경우 virtual 키워드를 선언해야 한다.
- 예부터 살펴보자.

```C++
class Parent {
    public:
        void say(){ std::cout << "parent's say" << endl; }
};

class Child : public Parent {
    public:
        void say(){ std::cout << "child's say" << endl; }
};

int main()
{
    Child* a = new Child();
    a->say();   // child's say 출력

    Parent *b = new Child();
    b->say();   // parent's say 출력

    return 0;
}
```

- 위에서 Parent 클래스의 포인터를 사용했지만, 실제 객체는 Child의 Instance 임에도 불구하고, Parent's say가 출력된다.

- 하지만 아래와 같이 virtual을 사용하는 경우

```C++
class Parent {
    public:
        virtual void say(){ std::cout << "parent's say" << endl; }
};

class Child : public Parent {
    public:
        void say(){ std::cout << "child's say" << endl; }
};

int main()
{
    Parent* a = new Child();
    a->say();   // child's say 출력

    return 0;
}
```

- child's say가 출력이 된다. virtual 키워드를 선언함으로써, Pointer의 타입이 아닌 Instance의 Type을 인지하여 호출한다.
- 바로 virtual이 이런 dynamic binding(late binding)이 가능하게 해주는 keyword이기 때문이다. 포인터의 타입이 아닌 실제 객체의 타입을 알아서 virtual function table을 찾아 동적으로 호출하는 것이다.
- 반면, virtual이 없는 함수들은 compile time binding이다. 이미 무엇을 호출할지 정해져 있다.
- Virtual class도 마찬가지다. pointer에 상관 없이 dynamic binding 이기 때문에 instance의 type에 맞는 method를 접근할 수 있게 된다.
- Ref: [C++Virtual Function](http://rapapa.net/?p=346)



#### 소멸자에 virtual을 쓰는 이유

- A클래스가 부모클래스, B클래스가 자식클래스 일때, 생성자의 호출 순서는 A::A(), B::B() 순서로 호출된다. 소멸자의 경우, 생성자의 반대 순서로 B::~B(), A::~A() 순서다.
- 다형성 이용을 위해 A클래스의 포인터로부터 B클래스를 호출할 때, 가상 함수로 정의되지 않은 B클래스의 오버라이딩된 함수를 호출하면 A클래스의 멤버 함수가 호출된다.
- 소멸자도 B클래스에서 오버라이딩된 함수라고 볼 수 있기 때문에 만약 A포인터로 객체를 삭제하면 A클래스의 소멸자가 호출된다. 따라서 소멸자를 가상 함수로 선언하지 않으면 이 경우 B클래스의 소멸자는 결코 호출되지 않는다.
- 가상 함수 키워드 virtual이 사용되었다면 이것은 B클래스에서 재정의될 수 있음을 명시하기 때문에 포인터의 종류에 상관없이 항상 B클래스의 메서드가 호출된다.
- 즉, 자식 클래스의 소멸자가 호출되고 나서 부모 클래스의 소멸자가 호출된다. 따라서 상속 관계가 있고 소멸자에서 리소스를 해제해야 하는 경우 반드시 소멸자를 가상 함수로 선언해야 한다.
- Ref: [C++/소멸자에 virtual을 쓰는 이유](http://hyacinth.byus.net/moniwiki/wiki.php/C%2B%2B/%EC%86%8C%EB%A9%B8%EC%9E%90%EC%97%90%20virtual%EC%9D%84%20%EC%93%B0%EB%8A%94%20%EC%9D%B4%EC%9C%A0)

#### C++ static
- 전역변수에 선언된 static
  - 선언된 파일 내에서만 참조를 허용하겠다는 의미
- 함수 내에 선언된 static의 의미
  - 한번만 초기화되고, 지역변수와 달리 함수를 빠져나가도 소멸되지 않는다.
- 초기값을 주지 않을 경우 항상 0 으로 초기화 되며 프로그램을 실행시킬 때 단 한번만 초기화된다. 
- static 멤버변수(클래스 변수)
  - static 멤버변수는 '클래스 변수'라고도 불린다. 일반적인 멤버변수와 달리 클래스당 하나씩만 생성되기 때문이다. 클래스 안에 선언된 static 변수의 경우 별개의 메모리에 할당되는 변수가 아닌 모든 객체가 공유하는 구조가 된다.
  - static 멤버변수는 생성자에서 초기화하면 안된다. static 멤버변수는 객체가 생성될때 동시에 생성되는 변수가 아니고, 이미 메모리공간에 할당이 이뤄진 변수이기 때문이다. 따라서 static 멤버변수의 초기화 문법은 다음과 같이 별도로 정의되어 있다.
  ```C++
  int student::objCnt; // static 멤버변수의 초기화 문법
  ```
- static 멤버함수
  - static 멤버함수 역시 그 특성이 static 멤버변수와 동일하다.
  - 선언된 클래스의 모든 객체가 공유한다.
  - public으로 선언이 되면, 클래스의 이름을 이용해서 호출이 가능하다.
  - 의 멤버로 존재하는 것이 아니다.
    
- 함수 내에서 static으로 변수를 선언해야 하는 경우는 **'전역 변수를 선언하고, 특정 함수에서만 사용하고 싶을 때'** 라고 생각하면 된다.
- static 전역 변수도 있는데, 이것은 여러 개의 파일을 컴파일 할 때 변수 이름의충돌을 막아 준다. 즉 **'그 파일에서만 그 변수를 사용하고 싶을 때'** 사용하면 된다. 
- 또 하나 static 함수인데, 이  것도 마찬가지로 여러 개의 파일을 컴파일 할 때 함수 이름의 충돌을 막아 준다. 즉 **'그 파일에서만 그 함수를 사용하고 싶을 때'** 사용하면 된다.

##### 일반 멤버 변수 및 멤버 함수와 static 멤버 변수와 멤버 함수에 대한 특징
- 일반 멤버 변수
  - 객체가 생성될 때마다 객체의 수만큼 생성된다.
  - 일반 멤버 변수를 객체의 생성 없이 직접 접근할 수 없다.
  - static 멤버 함수에서 접근할 수 없다.
  - 일반 멤버 함수에서 접근할 수 있다.
- 일반 멤버 함수
  - 객체가 생성되지 않아도 함수는 먼저 생성되어 있다. 그래서 언제든지 호출할 수도 있다. 단 객체가 생성되지 않았을 때의 호출은 아직 생성되지 않은 멤버 변수에 접근할 수 있기 때문에 프로그램을 다운시킬 수 있다.
  - 함수는 객체마다 하나씩 생성되는 것이 아니며, 오직 하나만 생성된다. 각 객체는 그 함수를 공유하여 사용하는 것 뿐이다.
  - 스레드에서 호출될 수 없다.
  - static 멤버 함수를 호출할 수 있다.
  - 상속할 수 있다.
  - this 포인터의 사용이 가능하다.
- static 멤버 변수
  - 객체의 생성과 관계 없이 생성되며, 객체에서 사용하는 전역 변수라고 생각하면 된다.
  - 반드시 ```int  T::count;```와 같은 추가적인 선언이 필요하다. 그렇지 않은 경우 LINK 에러가 발생된다.
  - private 영역에 선언되어 있으면, 멤버 함수에서만 접근 가능하고, public 영역에 선언되어 있으면, 멤버 함수 및 다른 함수에서 직접 접근할 수 있다.
  - 객체가 사용하는 전역 변수이기 때문에 오직 하나만 생성된다. 객체 변수들은 객체가 생성될 때마다 만들어 진다.
  - 일반 멤버 함수 및 static 멤버 함수에서 모두 접근 가능하다.
- static 멤버 함수
  - 일반 멤버 변수를 접근할 수 없다.
  - 일반 멤버 함수를 호출할 수 없다.
  - static 멤버 변수를 사용할 수 있다.
  - 상속할 수 없다.
  - 스레드에서 함수를 사용 가능하다.
  - public 영역에 선언되는 경우 전역에서 사용 가능하다.
  - this 포인터의 사용이 불가능하다. this 포인터는 객체가 생성되었을 때만 사용할 수 있기 때문이다. (객체가 없을 때 호출될 수 있는 static 멤버 함수가 객체 포인터(this)에 접근하는 것은 당연히 불가능)
  - 객체의 생성 없이 그 클래스의 일부 기능을 함수를 통해 제공할 때 사용한다.
  - 일반 멤버 함수는 스레드용 함수로 호출이 안되지만, static 멤버 함수는 스레드용 함수로 사용된다.


#### C++ 자료형(32bit)

| 구분   | 자료형        | 크기    |
|--------|---------------|---------|
| 문자형 | char          | 1 byte  |
|        | unsigned char | 1 byte  |
| 정수형 | int           | 4 byte  |
|        | unsigned int  | 4 byte  |
|        | short         | 2 byte  |
|        | long          | 4 byte  |
|        | unsigned long | 4 byte  |
| 실수형 | float         | 4 bytte |
|        | double        | 8 byte  |



### Java

#### Java static 
- static 변수(즉 정적변수)란  
  - Class 당 하나만 생성되는 변수, 객체(인스턴스)를 아무리 많이 만들더라도 변수는 하나만 존재 
  - 객체가 생성될 때마다 새롭게 생성되는 멤버 변수와는 달리 초기에 한번만 생성되고 공유하여 사용가능 
- static 변수 생성 시기
  - Class 이름이 언급되어 질때 생성 (new 뿐만 아니라 Class 명만 나와도 생성됨)
- static 변수 초기화 방법 
    - static 변수 는 초기 생성시 초기화 
    
    ```java
    public static int sTotal=0;
    ```

    - static 변수 는 초기 생성시 초기화. 최초 1회만 호출됨. 
    
    ```java
        public static int sTotal=0; 
        public int nTotal=0; 
        static { 
            sTotal += 10; 
            //nTotal += 10; //Static initializer 사용시 사용할 수 없다는 메시지 발생 
        } 
    ```
    
---

## Database

### Indexing의 장점과 단점은 무엇인가?
- 인덱싱이란?
  - 인덱싱은 데이터 검색에서 발생하는 비효율적인 문제를 해결하기 위한 대표적인 방법이다.
  - 즉, dbms에서 요청된 레코드에 빠르게 접근할 수 있도록 데이터와 관련된 부가적인 구조인 인덱스를 관리하는 것이다. 
  - 그리고 인덱스를 디자인하고 생성하는 작업을 인덱싱이라 한다. 
- 장점
  - 검색 속도가 무척 빨라질 수 있다. (반드시 그런것은 아니지만)
  - 그 결과 시스템의 부하가 줄어들어 시스템 전체 성능 향상에 도움이 된다.
- 단점
  - 인덱스가 데이터베이스 공간을 차지해 추가적인 공간이 필요해진다. (DB의 10퍼센트 내외의 공간이 추가로 필요)
  - 인덱스를 생성하는데 시간이 많이 소요될 수 있다.
  - 데이터 변경 작업이 자주 일어날 경우에 인덱스를 재작성해야 할 필요가 있기에 성능에 영향을 끼칠 수 있다.

### 정규화란?
- 관계형 데이터베이스의 설계에서 중복을 최소화하게 데이터를 구조화하는 프로세스를 정규화라고 한다. 
- 데이터베이스 정규화의 목표는 이상이 있는 관계를 재구성하여 작고 잘 조직된 관계를 생성하는 것에 있다. 일반적으로 정규화란 크고, 제대로 조직되지 않은 테이블들과 관계들을 작고 잘 조직된 테이블과 관계들로 나누는 것을 포함한다. 정규화의 목적은 하나의 테이블에서의 데이터의 삽입, 삭제, 변경이 정의된 관계들로 인하여 데이터베이스의 나머지 부분들로 전파되게 하는 것이다.
- Ref: [데이터베이스_정규화](https://ko.wikipedia.org/wiki/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4_%EC%A0%95%EA%B7%9C%ED%99%94)

### MongoDB
- MongoDB의 특징 
  - Flexibility: Schema-less 구조를 취함으로써 다양한 형태로 데이터를 저장 할 수 있다.
  - Performance: Read&Write 성능이 뛰어나다
  - Scalability: RDBMS의 한계로 잘 알려진 데이터 수용량을 확대 하고자 Scale Out 구조를 채택 함으로 인해 많은 데이터를 저장 할 수 있다.  
- MongoDB의 장점
  - Schema-less(Document Based): 데이터 모델의 유연한 변화가 가능하다. 데이터 모델에 대한 변경,추가 필드 확장이  간단하다. 그러나 RDBMS의 경우 스키마 변경에 따른 추가 작업이 필요 하다.
  - Structure of a single object is clearer: 가독성 측면에서 볼 때, json 구조를 사용하기 때문에 RDBMS 테이블 구조에 비해 데이터를 직관적으로 파악 할 수 있다.
  - No sql or hibernate queries (complex joins): MongoDB의 장점 중 하나는 사용하기 쉽다는 점다. 비교적 간단한 형태로 기존의 RDBMS의 SQL언어를 대체 할 수 있다. (i,e, $gt, $lt)
  - Tuning: consistency의 레벨이 컨트롤 가능 하기 때문에 성능에 중점을 두거나 또는 정합성에 중점을 둘지 선택 가능하다.
  - Ease of scale-out: Auto sharding을 지원 함으로서 장비 확장이 RDBMS 대비 간단하다.
- MongoDB의 단점
  - 만약 데이터 업데이트 중 장애가 발생한다면 데이터 손실이 발생할 수 있다. 따라서 중요데이터는 가급적 분리 보관을 추천한다.
  - 데이터의 복제 기능을 지원 하기는 하나 완전한 원복을 원한다면 데이터 센터를 분리해서 설치 해야 한다.
  - 인덱스 구조는 메모리에 저장 되기 때문에 많은 인덱스를 사용한다면 충분한 메모리를 사용하기 바란다.
  - 데이터는 필드네임과 함께 사용해야 함으로 데이터 공간 소모가 RDBMS 대비 많을 가능성이 있다.
  - 복잡한 join 사용시 성능 제약이 있다.Document Based 구조 임으로 가급적 join을 회피하는 구조로 사용해야 한다.  
- Summary
  - 데이터 전반적인 가이드의 결론은 많은 양의 데이터와 쓰기 읽기등 퍼포먼스에 치중한다면 MongoDB를, transaction과 같은 정합성 위주의 시스템을 사용한다면 RDBMS를 사용하기를 추천한다.
- Ref: [NoSQL – MongoDB를 RDBMS의 대안으로 고민 중이라면 참고할 만한 글](hochul.net/blog/nosql_mongodb_rdbms_alternative)



---

## Network

### TCP / UDP 차이점
- TCP(Transmission Control Protocol)
  - TCP는 신뢰성있는 데이터 전송을 지원하는 연결지향형 프로토콜이다. 연결지향형인 TCP는 3-way handshaking이라는 과정을 통해 연결 후 통신을 시작한다.
  - 흐름제어(보내는 측과 받는 측의 데이터 처리속도 차이를 조절)와 혼잡제어(네트워크 내의 패킷 수가 넘치게 증가하지 않도록 방지하는 것)를 지원하며 데이터의 순서를 보장한다.
  - TCP는 UDP에 비해 속도가 느리며, 대부분의 웹 HTTP 통신, 이메일, 파일전송에 사용된다.
- UDP(User Datagram Protocol)
  - UDP는 전송계층의 비연결형 프로토콜이다. TCP와 달리 연결 설정이 없으며, 혼잡제어를 하지 않기 때문에 TCP보다 빠르다.
  - 데이터 전송에 대한 보장을 하지 않기 때문에 패킷 손실이 발생할 수 있다. 이러한 특징 때문에 DNS, 멀티미디어에서 사용된다.
  - TCP와 같이 UDP도 헤더에 있는 Checksum 필드를 통해 최소한의 오류는 검출한다.
- Ref: [http://swalloow.tistory.com/77](http://swalloow.tistory.com/77)

#### 메신저 앱에서 TCP와 UDP는 어떤 경우에 사용될까?
- Ref: **[http://mintnlatte.tistory.com/307](http://mintnlatte.tistory.com/307)**

### TCP/IP 
- Server: socket() -> bind() -> listen() -> accept() -> read()/write() -> close()
- &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;↑
- Client: socket() ----------------------> connect() -> read()/write() -> close()

### 암호화의 3가지 종류를 설명하라.(by tutor)
- 대칭키 암호 시스템
- 공개키 암호 시스템
- ref: [https://ko.wikipedia.org/wiki/암호학](https://ko.wikipedia.org/wiki/암호학)
- ref: [https://ko.wikipedia.org/wiki/정보_보안](https://ko.wikipedia.org/wiki/정보_보안)


---

## Operating System

### Process와 Thread의 차이점
- Process
  - 운영체제에서 실행 중인 프로그램에 대한 인스턴스를 프로세스라고 한다. 운영체제로부터 주소 공간, 파일, 메모리 등을 할당 받고, 독립적이기 때문에 메모리 영역을 다른 프로세스와 공유하지 않는다.
- Thread
  - 한 Process에서 동작되는 실행의 단위이다. 프로세스가 생성될 때 기본적으로 하나의 쓰레드가 생성되며 이를 메인 쓰레드라고 한다. 프로세스는 여러 개의 쓰레드를 가질 수 있으며, 각 쓰레드마다 별도의 스택이 있다.
  - 각 쓰레드는 같은 프로세스에 있는 다른 쓰레드와 독립적으로 돌아가지만, 기본적으로 쓰레드끼리는 파일 핸들이나 메모리 같은 자원들을 공유한다. 때문에 공유 자원에 대한 접근 처리를 제대로 하지않으면 데드락 같은 문제가 생길 수 있다.

#### Thread와 Process의 차이점은 무엇인가? (by Tutor)
- Process : 프로그램 각각의 인스턴스를 의미. 멀티 프로세싱 OS에서는 동시에 여러 프로그램을 실행할 수 있다.
- Thread : 한 프로세스 내에서 동작되는 여러 실행의 흐름. 프로세스 내의 주소 공간이나 자원들을 대부분 공유하면서 실행된다.
- Ref: [http://ralf79.tistory.com/34](http://ralf79.tistory.com/34)

### Multi Process, Multi Thread
- 두 개의 프로세스는 완전히 독립된 두 개의 프로그램 실행을 위해서 사용되기 때문에 Context Switching으로 인한 성능 저하가 발생한다.
- 쓰레드는 메모리 영역을 공유하기 때문에 Context Switching이 더 빠르다.

### Context Switching
- 하나의 프로세스가 CPU를 사용 중인 상태에서 다른 프로세스가 CPU를 사용하도록 하기 위해, 이전의 프로세스의 상태(문맥)를 보관하고 새로운 프로세스의 상태를 적재하는 작업을 말한다. 한 프로세스의 문맥은 그 프로세스의 PCB(Process Control Block)에 기록되어 있다
- 참고로 운영체제의 스케쥴러가 실행 단위로 사용하는 것은 프로세스가 아닌 쓰레드이다. 프로세스는 상태(Running, Ready, Blocked)을 지니지 않으며 상태를 지니는 것은 쓰레드이다.
- Context Switching 동안에는 작업을 수행할 수 없기 때문에, Context Swithching 시간은 일종의 오버헤드라고 할 수 있다.
- Ref: [http://hso9201.tistory.com/212](http://hso9201.tistory.com/212)

### Thread Synchronization(쓰레드 동기화)
- Monitor
  - Mutual Exclusion Lock(이하 자물쇠)으로 보호되는 루틴의 집합
  - 쓰레드는 이 자물쇠를 획득하기 전까지는 모니터에 속하는 루틴을 실행할 수 없다. 즉, 한 모니터 내에서는 한 쓰레드씩 실행되며 다른 쓰레드는 전부 지금 실행 중인 쓰레드에서 그 자물쇠를 놓아줄 때까지 기다려야 한다.
- Semaphore
  - 공유 자원을 보호하기 위한 자물쇠
  - 쓰레드에서 공유 자원을 사용하려면 이 자물쇠를 획득해야 하고, 자물쇠를 쥐고 있는 쓰레드에서 놓아주기 전까지는 다른 쓰레드는 기다려야 한다. 대기하고 있던 쓰레드가 자물쇠를 획득하게 되면, 공유 자원에 접근할 수 있다. 이를 Mutex 세마포어(가장 기본적)라고 한다.
  - Counting Semaphore: 정해진 숫자 n이 있어서 최대 n개의 쓰레드에서 동시에 자원에 접근할 수 있음
  - Event Semaphore: 어떤 이벤트가 발생했음을 대기 중인 쓰레드 중 하나 또는 모든 쓰레드에게 알림
- Monitor, Semaphore 모두 같은 목적이지만, 자물쇠의 획득과 해제를 모두 처리해주는 Monitor 쪽이 간단하게 쓰기 좋다. Semaphore의 경우, 각 쓰레드에서 획득한 자물쇠를 해제하는 작업을 일일히 챙겨야 한다.
- DeadLock
  - 두 쓰레드가 서로 상대방이 쥐고 있는 자물쇠가 풀리기만을 기다리고 있을 때 발생한다.

### Heap, Stack 차이점(메모리 구조)
- 운영체제는 프로그램을 실행시킬 때 메모리 공간을 할당하는데, 이 공간은 Stack, Heap, Data 영역으로 나뉜다.
- Data 영역
  - 전역 변수, Static 변수가 할당되는 영역
  - 프로그램의 시작과 동시에 할당되고, 프로그램이 종료되어야 메모리에서 소멸된다.
- Heap 영역
  - 동적으로 메모리를 할당할때 사용(프로그래머가 직접 관리)
  - 할당해야 할 메모리의 크기를 프로그램이 실행되는 동안 결정해야 하는 경우(런 타임 때) 유용하게 사용되는 공간
- Stack 영역
  - 함수 호출 시 생성되는 지역 변수와 매개 변수가 저장되는 영역
  - 함수 호출이 완료되면 사라짐
   
 
---
## Web
- SPA(Single Page Application)
  - 단일 페이지 어플리케이션은 브라우저에 로드되고 난 뒤에 페이지 전체를 서버에 요청하는것이 아니라 최초한번 페이지전체를 로딩한후 이후부턴 데이터만 변경해서 사용할 수 있는 웹 어플리케이션을 말한다. 개발자들은 단일 페이지 어플리케이션을 만들기 위해 Backbone.js,Angular.js 등의 자바스크립트 라이브러리를 사용한다.
  - SPA의 Single Page라는 의미는 최초에 index.html 을 서버로부터 받은 후 부분적인 화면의 변경을 위하여 일부 HTML(Partial HTML)만을 받아 index.html의 특정 영역의 DOM 객체 변경을 통해 View를 바꿔준다. 이후 서버로 부터 받는 것은 View의 컨텐츠 데이터인 JSON 이나 XML 데이터이다. 이렇게 화면의 부분 변경을 위하여 클라이언트단에서 움직이는 Routing 기능을 제공한다. 이를 위하여 클라이언트 템플릿 엔진이 자체 내장되어 있다.
 - ref: [SPA(SINGLE PAGE APPLICATION) 이란?](http://devsh.tistory.com/entry/SPASingle-Page-Application-%EC%9D%B4%EB%9E%80)
 
 
---

## iOS

### Todo
- collection의  개념 설명하라 : list, hash, set
- mutable, in-mutable 차이를 설명하라
- GCD를 설명하라
- delegate / notification 각각 무엇이고 언제 써야하는지 설명하라
- ARC / Non-ARC의 차이는 무엇인가?
- UIViewController의 lifecycle 설명하라
- isKindOfClass / isMemberOfClass 의 차이를 설명하라
- OpenSource를 활용해보았는가?
- IB, StoryBoard를 어떻게 이용해보았는가?
- Memory Leak을 줄이기 위해서 어떤 방법들을 사용해보았는가?
- 네트워크 프로그래밍에서 중간에 다운로드가 중단된다면 어떻게 처리할 것인가?
- GCD(Grand Central Dispatch)를 사용해보았는가?
- CocoaPods를 써보았는가?
- 최신 iOS 개발기술 정보는 어디서 얻는가?
- 최근에 본 애플의 iOS 기술문서는 무엇인가?
- Swift언어에 대해 어떻게 생각하는가?

### Mutable 객체와 Mutable하지 않은 객체의 차이는 무엇인가?
- mutable 객체는 객채 내의 특정 요소를 변경 할 수 있는 객체를 mutable 객체라고 한다.

### NSArray와 NSMutableArray 중에서 Thread safe하지 않는 쪽은 어디인가?
- NSMutableArray는 스레드로부터 안전하지 않습니다. 경우 사람에 스레드 안전한 환경에서 removeAllObject 이상을 달성하고자, 나는 잠금 장치를 사용하여 하나 이외의 GCD를 사용하여 다른 솔루션을 제공 할 것입니다. 당신이해야 할 것은 행동 (/ 제거를 대체) 읽기 / 업데이트를 동기화하는 것입니다.

### Autorelease Pool을 직접 구현한다면 어떻게 만들겠나?
- [http://www.clien.net/cs2/bbs/board.php?bo_table=cm_app&wr_id=466](http://www.clien.net/cs2/bbs/board.php?bo_table=cm_app&wr_id=466)
- [http://www.programkr.com/blog/MgTM3ADMwYTz.html](http://www.programkr.com/blog/MgTM3ADMwYTz.html)

### Blocking I/O와 Non-Blocking I/O의 차이는 무엇인가?
- [http://devsw.tistory.com/142](http://devsw.tistory.com/142)

### Memory Warning이 발생하면 어떤 일이 일어날까?
- [https://developer.apple.com/library/ios/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/PerformanceTips/PerformanceTips.html](https://developer.apple.com/library/ios/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/PerformanceTips/PerformanceTips.html)
- [https://soulpark.wordpress.com/2013/07/25/ios-arc-from-top-developer/](https://soulpark.wordpress.com/2013/07/25/ios-arc-from-top-developer/)
- iOS 디바이스가 low-memory warning을 받으면 view가 unload되는데 이때 weak으로 처리해야 IBOutlet에 연결된 view도 자동으로 해제된다. 

### Static Library와 Dynamic Library를 설명하시오.
- [http://tadis.tistory.com/54](http://tadis.tistory.com/54)

### 파일을 (앱의 Sandbox 안에) 안전하게 저장하는 방법은?
### Sandbox안의 Document, Cache, Temp 폴더의 차이를 설명하시오.
- App 폴더 : 어플리케이션의 홈 디렉토리
- MyApp.app : bundle 이라고 하며 앱 실행을 위한 파일들이 위치한다. Xcode 를 통해 템플릿 프로젝트를 만들때 자동으로 생성되는 기본 아이콘 이미지들은 이 곳에 위치한다. 개발 중 추가되는 파일(이미지, 텍스트 파일 등)도 이곳에 위치한다. 앱 실행 중 폴더의 내용 변경 및 쓰기는 하지 말자.
- Documents : 사용자 정보를 저장한다. 이 곳의 데이터는 iTunes 에 의해 백업된다. Xcode 를 이용하여 이 곳에 파일을 추가할 수 없다. Runtime 에서만 접근 가능하다.
- Library : 사용자 정보를 제외한, 백업을 필요로 하는 데이터를 저장하는데 사용한다. Runtime 에서 접근 가능하다.
- tmp : 임시 파일을 위한 저장소이다. 개발자는 필요 없어진 파일을 삭제해야 한다. iOS 시스템은 앱이 실행 상태가 아닐 때 폴더내 파일을 삭제할 수 있다. Runtime 에서 접근 가능하다.
- ref: [https://soulpark.wordpress.com/2012/09/24/ios-file-system/](https://soulpark.wordpress.com/2012/09/24/ios-file-system/)

-----

## etc
- 전 직장에서 가장 많이 배운것?
- 전 직장에서 무엇을 중시했나
- 전 직장에서 모자랐던 부분과 잘했던 부분?
- 직장 외에 새로 공부하는 것 or 빠져있는 것?
- 전 직장에서 퇴사하는 이유?
- 본인이 회사에서 가장 중요시 여기는 것?
- 본인이 수행했던 프로젝트에 대한 설명
- 전 직장에서 뭐했나?
- 클라우드 컴퓨팅이란?
- 자신의 강점을 말하고 그것을 회사에서 어떻게 활용할건지?
- 마지막으로 할 말?


