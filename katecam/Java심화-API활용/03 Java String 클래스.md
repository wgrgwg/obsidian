- 문자열은 Java에서 객체로 취급

## 문자열 생성방법 2가지
1. `String str1 = new String("Hello World");`
	- Heap 메모리에 저장
2. `String str2 = "Hellow World";`
	- 문자열 상수 : Literal Pool 메모리 -> **재활용 가능**

```Java
// 1. new : Heap 메모리
String str1 = new String("Hello World");
String str2 = new String("Hello World");
// 새로운 객체를 생성후 str2가 가리킴

// 2. 문자열 상수 : Literal Pool 메모리
String str1 = "HelloWorld";
String str2 = "HelloWorld"; // 기존 객체를 str2가 가리킴
```

## String 클래스에서 제공하는 Method
- `charAt(i)` : 인덱스 해당하는 문자 한 개 반환
- `replaceAll("A", "B")` : 모든 A를 B로 치환해서 반환
- `indexOf("A")` : A의 위치를 반환
	- 없으면 -1 반환
- `length()` : 길이 반환
- `toUpperCase` : 대문자로 변환해서 반환
- `substring(i)` : 위치 i 부터 끝까지
	- `substring(s, e)` : 위치 s부터 e-1까지

```Java
public class StringManipulation {  
  
    public static void main(String[] args) {  
        String str = new String("HelloWorld");  
        // String str = "HelloWorld"; 도 가능  
        System.out.println(str.charAt(0)); // H  
        System.out.println(str.replaceAll("o", "X")); // HellXWXrld  
        System.out.println(str.length()); // 10  
        System.out.println(str.toUpperCase()); // HELLOWORLD  
        System.out.println(str.toLowerCase()); // helloworld  
        System.out.println(str.substring(5)); // World  
        System.out.println(str.substring(5, 8)); // Wor  
    }  
}
```

## Java에서 문자열 비교
- 문자열은 `==` 사용 X
- `equals()`
	- 같으면 True, 다르면 False
- `compareTo()`
	- 같으면 0
	- 비교 대상 문자열이 기존 문자열보다 작으면 음수, 크면 양수
	- 아스키값 뺄셈(str3 - str4)

```Java
public class StringCompare {  
  
    public static void main(String[] args) {  
        String str1 = "Hello";  
        String str2 = "World";  
  
        if (str1.equals(str2)) {  
            System.out.println("같음");  
        } else {  
            System.out.println("다름");  
        }  
  
        String str3 = "apple";  
        String str4 = "banana";  
  
        int result = str3.compareTo(str4);  
  
        if (result == 0) {  
            System.out.println("같음");  
        } else if (result < 0) {  
            System.out.println("str3이 str4보다 앞에 있음");  
        } else {  
            System.out.println("str3이 str4보다 뒤에 있음");  
        }  
    }  
  
}
```

## Java에서 문자열을 분리
- 문자열을 특정 구분자(delimitr)를 기준으로 분리하여 출력
	- 배열로 리턴
	- `str.split(",)`
- 정규표현식
	- `str.split("\\s+")`
	- `\s+` : 하나 이상의 공백 문자

```Java
public class StringSplit {  
  
    public static void main(String[] args) {  
        String str = "Hello,World,Java";  
        String[] strArray = str.split(",");  
  
        for(String s : strArray){  
            System.out.println(s);  
        }  
  
        String str2 = "Hello World Java";  
  
        String[] strArray2 = str2.split("\\s+"); // '\' 주의
        for(String s : strArray2){  
            System.out.println(s);  
        }  
    }  
  
}
```