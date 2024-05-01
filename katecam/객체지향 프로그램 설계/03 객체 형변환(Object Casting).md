- 상속관계에서 객체를 생성하는 방법
	- 업 캐스팅(Upcasting)
	- 다운 캐스팅(Downcasting)

## 부모와 자식 간의 형 변환
- Upcasting 업캐스팅 (**자동**형변환)
- Downcasting 다운캐스팅 (**강제**형변환)
	- 상위클래스의 타입을 하위클래스의 타입으로 바꾸는 행위
	- `자식A c = (자식A)부모;`
	- `Dog d = (Dog)Animal()`

```Java
public class ObjectCasting {  
    public static void main(String[] args) {  
        // Animal --> Dog, Cat 업캐스팅
        Animal ani = new Dog();  
        ani.eat();  
  
        ani = new Cat();  
        ani.eat();  
        // ani.night(); X -> 고양이만 갖고 있는 함수는 불가
  
    }  
}
```

## Upcasting, Downcasting
- 부모는 자식의 요소 마음대로 사용 X
	- **자식 클래스 타입을 형변환 후 사용!** -> Downcasting
	- `((Cat)x).night();`

```Java
public class ObjectCasting {  
    public static void main(String[] args) {  
        // Animal --> Dog, Cat  
        Animal ani = new Dog();  
        ani.eat();  
  
        ani = new Cat();  
        ani.eat();  
        // ani.night(); -> 고양이만 갖고 있는 함수  
  
        //Downcasting으로 해결!  
        //        Cat c = (Cat)ani;  
//        c.night();  
  
        ((Cat)ani).night();  
    }  
}
```