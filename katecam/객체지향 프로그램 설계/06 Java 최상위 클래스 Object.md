
## Object 클래스 이용한 객체 생성
- 클래스 생성 시 기본적으로 생략된 코드
```Java
import java.lang.*; // 1
public class A extends Object {  // 2
	public A(){ super(); } // 3
}
```
1. **default package**
2. **java.lang.Object 최상위 클래스**
3. **default 생성자**

- Object는 모든 클래스의 부모이므로, upcasting 가능

## Object 클래스 활용한 다형성 적용
- 다형성 인수 활용
- 다형성 배열 활용
- Object 타입으로 Upcasting 하면 반드시 Downcasting 하여 사용
	- `instanceof` 사용!

```Java
public class ObjectPolyArg {  
    public static void main(String[] args) {  
        A a = new A();  
        display(a);  
  
        B b = new B();  
        display(b);  
    }  
  
    private static void display(Object obj) {  /// 다형성 인수 활용
        if(obj instanceof A)  
            ((A)obj).printGO();  
        else if(obj instanceof B)  
            ((B)obj).printGO();  
    }  
}
```

- Object 배열도 같은 식으로 적용

## Object 클래스의 toString()
- `toString()` : 객체의 번지를 문자열로 출력
	- 재정의할 시  다른 용도로 사용 가능
```Java
public class Board extends Object{  
    private String title;  
  
    public String getTitle() {  
        return title;  
    }  
  
    public void setTitle(String title) {  
        this.title = title;  
    }  
  
    // toString 재정의 안할 시 -> 번지수 반환  
    @Override  
    public String toString() {  
        return "Board{" +  
                "title='" + title + '\'' +  
                '}';  
    }  
}
```