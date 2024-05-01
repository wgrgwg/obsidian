## 상속의 컨셉
- 컨셉 : 자식과 부모는 상속 관계이기 때문에 자식은 부모의 것 사용 가능
	- **접근 허락 필요**
	- 상속 : 부모가 자식에게 사용을 허락

## 수직적 구조와 수평적 구조
##### EX) 사원의 VO 클래스를 설계?
- 비슷한 클래스의 경우, **중복적인 요소** 발생
- **수평적 구조 단점**
	1. 코드 중복 발생
	2. 새로운 요구사항 발생시 반영(유지보수) 어려움
	3. 확장성 ↓
- **수직적 구조**
	- 상속, 계층화
	- 부모(사원)을 **확장 Extends (상속)** -> 자식들이 사원의 정보를 사용가능
	- 코드의 중복부분 최소화
	- 상속 : 클래스와 클래스간의 관계 설계

## 클래스 계층화의 장점
- 상속관계(`is a kind of`)
	- Java는 단일 상속만 지원
1. 코드 중복 최소화
2. 새로운 요구사항 발생시 반영 쉬움
3. 확장성 ↑

## 메모리를 통한 상속(Extends)의 이해
- 하위 클래스가 **상위클래스를 재활용** 가능
	- 하위클래스가 상위클래스에 접근하여 사용 가능
	- 부모의 기억공간 사용가능
- **부모 Super class -> 자식 Sub class**
	- 부모 : 일반화, 추상화, 개념화, 포괄적
	- 자식 : 구체화, 세분화
- `protected` : 상속관계에서 하위 클래스에게 접근을 허용
- `super()` : 상위클래스의 생성자를 호출
	- 생략됨
	- 자식 클래스 객체 생성시 -> 자동으로 부모 클래스 객체 생성
	- **Java의 모든 클래스는 `Object` 클래스를 상속**

- Employee (공통 사원 - 부모 클래스)
```Java
public class Employee {  
    // protected : 상속, 같은 패키지 내에 잇어야 함  
    protected String name;  
    protected int age;  
    protected String phone;  
    protected String empDate;  
    protected String dept;  
    protected boolean marriage;  
  
    public Employee(){  
        super(); // 상위 클래스의 생성자 호출 -> Object(최상위 클래스)  
    }  
  
    // toString()  
  
    @Override  
    public String toString() {  
        return "Employee{" +  
                "name='" + name + '\'' +  
                ", age=" + age +  
                ", phone='" + phone + '\'' +  
                ", empDate='" + empDate + '\'' +  
                ", dept='" + dept + '\'' +  
                ", marriage=" + marriage +  
                '}';  
    }  
}
```

- RempVO (일반사원 - 자식 클래스)
```Java
public class RempVO extends Employee{  
    public RempVO(){  
        super(); // Employee 생성자 호출  
    }  
}
```

- main
```Java
public class EmployeeTest {  
    public static void main(String[] args) {  
        RempVO vo = new RempVO();  
  
        /**  
         * vo에 정보 입력  
         */  
  
        //출력  
        System.out.println("vo = " + vo);  
    }  
}
```

- 하지만, 부모 클래스에 자식이 마음대로 접근 -> **정보 은닉 위배!**

## 상속관계에서 객체생성
- 정보 은닉을 어떻게 유지?
	- protected? X -> 자식에서 직접 접근 막아야 함
	- 자식 생성자를 이용해 초기화? X -> 결국엔 자식에서 직접 접근
	- **super를 통해서 부모 생성자가 초기화 하도록 함!!**

## 상속관계에서 객체초기화
- `super()` 을 이용해 부모의 생성자로 값을 넘겨줌 -> 부모 생성자가 초기화
```Java
// 사원(DO, VTO)  
public class Employee {  
    // protected : 상속, 같은 패키지 내에 잇어야 함  
    private String name;  
    private int age;  
    private String phone;  
    private String empDate;  
    private String dept;  
    private boolean marriage;  

	public Employee(){
		super(); // 상위 클래스의 생성자 호출 -> Object(최상위 클래스)  
	}

    public Employee(String name, int age, String phone, String empDate, String dept, boolean marriage){  
		// 초기화
        this.name = name;  
        this.age= age;  
        this.phone = phone;  
        this.empDate = empDate;  
        this.dept = dept;  
        this.marriage = marriage;  
    }  
  
    // toString()  
  
    @Override  
    public String toString() {  
        return "Employee{" +  
                "name='" + name + '\'' +  
                ", age=" + age +  
                ", phone='" + phone + '\'' +  
                ", empDate='" + empDate + '\'' +  
                ", dept='" + dept + '\'' +  
                ", marriage=" + marriage +  
                '}';  
    }  
}
```

```Java
//일반사원 VOpublic class RempVO extends Employee{  
  
    public RempVO(String name, int age, String phone, String empDate, String dept, boolean marriage) {  
        // 초기화(자식이 부모의 기억공간에 초기화)  
        super(name, age, phone, empDate, dept, marriage);  
    }  
}
```