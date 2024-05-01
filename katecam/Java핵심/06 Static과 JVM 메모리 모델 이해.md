- static 키워드와 메모리 관계 이해
- JVM이 사용하는 메모리 모델(4가지)

## Static과 메모리의 관계
- 메인(시작) 클래스는 왜 객체생성(`new`) 없이 실행?
- 메인 클래스 동작 방식을 이해
	1. JVM이 실행할 클래스 탐색
	2. static 키워드가 붙은 멤버들을 **정해진 메모리(static-zone) 위치**에 한번 자동으로 로딩
		- static 멤버들은 클래스를 사용하는 시점에서 딱 한번 메모리에 로딩
	3. JVM이 static-zeone에서 main() 메서드를 호출
	4. 호출된 메서드를 **Call Stack Frame Area(Stack Area)에** push하고 동작을 시작

- **Call Stack Frame Area**
	- 메서드가 호출되면 호출된 기계어 코드가 push되고 실행되는 메모리공간
	- LIFO(스택) 구조
	- 지역변수는 life cycle이 method와 같음
- **Method Area는 static zone과 none-static zone으로 나뉨**
	- 메서드의 기계어 코드가 할당

## Static과 None-Static 멤버들의 접근 방법
- static 메서드에서는 static 메서드에만 접근 가능
```Java
public class StaticTest {  
    public static void main(String[] args) {  
        int a = 10;  
        int b= 20;  
  
        int res = StaticTest.hap(a, b); // 인스턴스가 아닌 클래스 이름으로 접근  
        System.out.println("res = " + res);  
    }  
  
    public static int hap(int a, int b){  
        int v = a+b;  
        return v;  
    }  
}
```

- static 메서드에서 none-static 메서드 접근 위해선, 메모리에 올려야 함
	- 클래스에 대한 **객체를 생성**
```Java
public class NoneStaticTest {  
    public static void main(String[] args) {  
        int a = 10;  
        int b= 20;  
  
        NoneStaticTest nst = new NoneStaticTest();  
  
        int res = nst.hap(a, b); // 인스턴스가 아닌 클래스 이름으로 접근  
        System.out.println("res = " + res);  
    }  
  
    public int hap(int a, int b){  
        int v = a+b;  
        return v;  
    }  
}
```

- **Heap Area에 객체를 생성**
	- Method Area의 기계어 코드를 가리킴(pointer)

- Static 멤버는 클래스를 사용하는 시점에, 자동으로 static-zone으로 로딩
	- new로 객체 생성할 필요 X
	- `클래스이름.method1()`
```Java
public class StaticAccess {  
    public static void main(String[] args) {  
        int a = 10;  
        int b = 20;  
  
        // MyUtil  
        int sum = MyUtil.hap(a, b); // Static 메서드  
        System.out.println("sum = " + sum);  
    }  
}
```

## JVM이 사용하는 메모리 영역
- **Method Area**
	- 메서드의 바이트코드(기계어 코드)가 할당되는 공간
	- static-zone과 none-static-zone으로 나뉨
- **Heap Area**
	- 객체가 생성되는 메모리 공간(new 연산자)
	- GC(Garbage Collector)에 의해서 메모리 수집
	- 가리키지 않는 객체는 GC가 소멸시킴
- **Stack Area(Call Stack Frame)**
	- 메서드가 실행되는 메모리공간
	- LIFO 구조
- **Runtime Constant Pool(Literal Pool)**
	- 상수 값 할당이 되는 메모리 공간
	- 문자열 상수가 할당

## 객체생성과 static과의 관계
- 어떤 클래스의 **모든 멤버가 static 멤버**인 경우?
	- 객체 생성할 필요 X -> 클래스명으로 호출이 더 바람직
	- **생성자를 private으로 설정** -> 객체 생성을 방지 `private AllStatic(){}`
- java `System` 도 객체 생성 불가

```Java
public class AllStatic {  
  
    // 객체 생성 방지  
    private AllStatic(){}  
  
    public static int hap(int a, int b){  
        return a+b;  
    }  
  
    public static int max(int a, int b){  
        return a>b? a : b;  
    }  
  
    public static int min(int a, int b){  
        return a<b? a : b;  
    }  
}
```

## Class, Obejct, Instance 상호관계 
- **클래스(Class)** : 객체를 모델링하는 도구
- **객체(Obeject)** : 클래스를 통해서 선언되는 변수
	- 변수가 구체적인 대상을 가리키지 않는 상태(객체 변수)
	- 객체가 구분되지 않는 시점
- **인스턴스(Instance)** : 객체생성에 의해 메모리(Heap)에 만들어진 객체
	- 객체가 구체적인 실체를 가리키는 상태
	- 객체가 서로 구분이 됨

`Student st = new Student();`