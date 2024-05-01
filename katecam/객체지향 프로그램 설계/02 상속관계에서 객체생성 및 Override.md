- 클래스의 행위(동작, 메서드) 정보에 초점을 맞춰 클래스를 설계(상속)

## 동작측면에서 클래스 설계
#### 클래스 동작 측면에서 상속
- 수평적 구조 : 메서드 중복이 발생
- 수직적 구조 : 상위 클래스로부터 상속
	- `Animal 클래스` - `먹다()` : 너무 추상적 -> 구체화는 어떻게?

- 타인이 설계한 Dog 클래스를 사용?
	- 컴파일된 `Dog.class` 파일만 획득
	- 내부 코드, 동작을 모름
	- **Dog 클래스를 동작시키는 별도의 interface 클래스를 정의, 배포**

## 상속관계에서의 객체생성 방법
- 클래스 `Dog`를 동작시키는 다른 클래스를 정의
	- 해당 클래스를 동작시키는 상위 클래스 정의

#### 업캐스팅
- 부모가 자식을 가리키는 객체 생성방법
- 자식의 객체를 부모 타입 변수에 대입
- `Animal X = new Dog();`
- 자식 메모리에는 접근 X

## 상속 체이닝과 super
- **상속 체이닝**
	- 맨 위 부모클래스 부터 객체가 생성되어 자식까지 연결되는 구조

- **`super()`**
	- 상위 클래스의 생성자를 호출
	- **생성자 메서드의 첫 문장에 사용**

- A - B - C 로 상속인 경우
	- C는 A, B, C에 접근 가능
	- B는 A, B에 접근 가능

- 업캐스팅의 경우
	- 부모 타입 변수는 자식 공간에는 접근 X

 - **오버라이드 : 부모의 메서드를 자식의 메서드가 재정의**
	- Dog의 `eat()` -> Animal 의 `eat()`를 재정의
	- 재정의된 **자식의 `eat()`를 실행! -> 동적 바인딩**
	- 컴파일시엔 모름, 런타임에 실행

## 메서드의 재정의(Override)
- **Override(재정의)**
	- 상속관계에서 하위클래스가 상위클래스의 동작을 재정의(기능추가, 변경)

- **동적바인딩**
	- 실행시점에서 사용될 메서드가 결정됨

```Java
public class Animal {  
    public void eat(){  
        System.out.println("동물같이 먹는다.");  
    }  
}
```

```Java
public class Dog extends Animal{  
    public Dog(){  
        super(); // 무조건 생성자 첫 문장에 위치  
    }  
  
    public void eat(){  
        System.out.println("개같이 먹는다.");  
    }  
}
```

```Java
public class Cat extends Animal{  
    public void eat(){  
        System.out.println("고양이같이 먹는다.");  
    }  
  
    public void night(){  
        System.out.println("밤에 눈이 빛난다.");  
    }  
}
```

```Java
public class OverrideTest {  
    public static void main(String[] args) {  
        // Upcasting  
        Animal ani = new Dog();  
        ani.eat(); // Dog에서 재정의한 eat() 함수 실행  
  
        ani = new Cat();  
        ani.eat(); // Cat에서 재정의한 eat() 함수 실행  
    }  
}
```

