- 자바 람다식 : 함수를 간결하게 표현하기 위한 방법
	- 자바 8 부터 도입
	- 익명 함수의 형태로서 메서드의 구현을 간결하게 표현

## 함수형 인터페이스
- **함수형 인터페이스** : 단 하나의 추상 메서드를 가진 인터페이스
	- `@FunctionalInterface` 어노테이션 사용
- 구현체를 사용 클래스 내부에 구현해서 바로 사용
- 사용 이유
	1. 람다 표현식 지원
	2. **메서드 참조**
	3. Stream API와의 통합
	4. 병렬 프로그래밍
	5. 코드 재사용

```Java
@FunctionalInterface // 함수형 인터페이스  
public interface MathOperations {  
    public int operation(int x, int y); // 추상 메서드  
}
```

```Java
public class FunctionInterfaceTest {  
  
    public static void main(String[] args) {  
        MathOperations mo = new MathOperations() {  
            @Override  
            public int operation(int x, int y) {  
                return x + y;  
            }  
        };  
        int result = mo.operation(10, 20);  
        System.out.println(result);  
    }  
  
}
```

## 함수형 인터페이스 메서드 참조
- 메서드 참조
	- 이미 정의된 메서드를 직접 참조
	- 기존 메서드를 재사용
- 유형
	1. 정적 메서드 참조 `클래스명::메서드명`
	2. 인스턴스 메서드 참조 `객체참조::메서드명`
	3. 특정 객체의 인스턴스 메서드 참조 `클래스명::메서드명`
	4. 생성자 참조 `클래스명::new`
		- 람다 표현식이나, 익명 클래스 방법도 가능

- 인터페이스
```Java
@FunctionalInterface  
public interface Converter<F, T> {  
    T convert(F from);  
}
```

1. **정적 메서드 참조**
```Java
public class IntegerUtils {  
    // 정적메서드, 클래스메서드  
    public static int stringToInt(String s){  
        return Integer.parseInt(s);  
    }  
}
```

```Java
public class IntegerUtilsTest {  
  
    public static void main(String[] args) {  
        // 정적메서드 참조  
        Converter<String, Integer> converter = IntegerUtils::stringToInt;  
        Integer result = converter.convert("123");  
        System.out.println("result = " + result);  
    }  
  
}
```

2. **인스턴스 메서드 참조**
```Java
public class StringUtils {  
    // 인스턴스 메서드  
    public String reverse(String s){  
        return new StringBuffer(s).reverse().toString();  
    }  
}
```

```Java
public class StringUtilsTest {  
  
    public static void main(String[] args) {  
        StringUtils stringUtils = new StringUtils();  
        Converter<String, String> converter = stringUtils::reverse;  
        String result = converter.convert("Hello");  
  
        System.out.println("result = " + result);  
    }  
  
}
```

3. **특정 객체 참조**
```Java
public class SortCompareTest {  
  
    public static void main(String[] args) {  
        List<String> names = Arrays.asList("김", "홍", "이");  
        Collections.sort(names, String::compareTo);  
        System.out.println(names);  
    }  
  
}
```

4. **생성자 참조**
```Java
@FunctionalInterface  
public interface PersonFactory {  
    public Person create(String name, int age);  
}
```

```Java
public class PersonFactoryTest {  
  
    public static void main(String[] args) {  
//        PersonFactory personFactory = Person::new;  
//        Person person = personFactory.create("홍길동", 40);  
//        System.out.println(person);  
        PersonFactory personFactory = new PersonFactory() {  
            @Override  
            public Person create(String name, int age) {  
                return new Person(name, age);  
            }  
        };  
        Person person = personFactory.create("나길동", 32);  
        System.out.println(person);  
    }  
}

```

## 람다식이란
- 함수를 간결하게 표현하는 방법
- 익명 함수
- `(int x, int y) -> { return x + y; }`
- 함수형 인터페이스와 함께 사용
```Java
public class LambdaExample {  
  
    public static void main(String[] args) {  
        MathOperation add = (x, y) -> x+y;  
        // MathOperation add = (int x, int y) -> { return x + y; };  
        int result = add.operation(10, 20);  
        System.out.println("result = " + result);  
    }  
  
}
```

## 람다식의 사용 방법
- 람다 표현식을 메서드 내에서 사용하거나 메서드의 인자로 전달
```Java
public class LambdaApply {  
  
    public static void main(String[] args) {  
        StringOperation toUpperCase = s -> s.toUpperCase();  
        StringOperation toLowerCase = s -> s.toLowerCase();  
  
        String input = "Lambda Experssion";  
        System.out.println(processString(input, toUpperCase));  
        System.out.println(processString(input, toLowerCase));  
    }  
  
    public static String processString(String input, StringOperation operation) {  
        return operation.apply(input);  
    }  
  
}
```

## Stream API의 이해
- 배열 -> 스트림 변환
	- 배열의 원소들을 스트림 형태로 변환하여 처리
- **스트림** : 데이터의 흐름
	- 원본을 변경 X
	- 필터링, 매핑, 정렬 등 처리

```Java
int[] numbers = {1,2,3,4,5};
// IntStream stream = Arrays.stream(numbers);

int sumOfEvens = Arrays.stream(numbers).filter(n->n%2==0).sum();

int[] evenNumbers = Arrays.stream(numbers).filter(n->n%2==0).toArray();
```

- **중간 연산**
	- 스트림을 처리하고 다른 스트림 반환
- **최종 연산**
	- 스트림을 처리하고 반환

## Stream API 활용
- 각 숫자를 제곱한 후 모든 숫자의 합을 계산
```Java
public class StreamExample {  
  
    public static void main(String[] args) {  
        List<Integer> numbers = Arrays.asList(1,2,3,4,5,6,7,8,9,10);  
        Predicate<Integer> isEven = n->n%2==0;  
  
        int sumOfSquares = numbers.stream()  
            .filter(isEven)  
            .sorted()  
            .map(n->n*n)  
            .reduce(0, Integer::sum);  
        System.out.println("sumOfSquares = " + sumOfSquares);  
    }  
  
}
```

- 숫자 배열 각각을 제곱으로
``` Java
public class MapStreamExample {  
  
    public static void main(String[] args) {  
        List<Integer> numbers = Arrays.asList(1,2,3,4,5);  
        List<Integer> squaredNumbers = numbers.stream()  
            .map(a->a*a)  
            .collect(Collectors.toList());  
        System.out.println("squaredNumbers = " + squaredNumbers);  
    }  
  
}
```

- 문자열 배열 각각을 대문자로
```Java
public class MapStreamExample2 {  
  
    public static void main(String[] args) {  
        List<String> words = Arrays.asList("apple", "banana", "cherry", "orange");  
  
        List<String> uppercase = words.stream()  
            .map(word->word.toUpperCase())  
            .collect(Collectors.toList());  
        System.out.println("uppercase = " + uppercase);  
    }  
  
}
```