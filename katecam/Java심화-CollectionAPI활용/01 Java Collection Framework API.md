- 데이터 구조 컬렉션을 표현하는 인터페이스와 클래스의 모음(API)
- 객체만 가능(기본 자료형 X)
## Wrapper 클래스란
- **Wrapper 포장 클래스**
	- 기본 데이터 타입을 객체로 다룰 수 있도록 만들어진 클래스
	- **자동**으로 boxing / unboxing (기본 자료형 <-> wrapper 클래스 객체)
	- 기본 데이터 타입의 첫 글자를 **대문자**로

```Java
public class WrapperTest {  
  
    public static void main(String[] args) {  
        // 정수형 변수에 10을 저장  
        int a = 10; // 기본 자료형  
  
        // Auto-boxing  
        Integer aa = 10; // 사용자정의 자료형  
        System.out.println(aa.intValue()); // Unboxing  
  
        Integer bb = new Integer(20); // boxing  
        int b = bb; // Auto-unboxing  
        System.out.println(b);  
        System.out.println(bb);  
    }  
  
}
```

## 숫자와 문자열의 상호 변환
- 숫자형 문자열 -> 정수 (String to int)
	- `Integer.parseInt()`
- 정수 -> 문자열 (int to String)
	- `String.valueOf()`
	- `"" + 정수`

```Java
public class IntegerStringTest {  
  
    public static void main(String[] args) {  
        String str1 = "123";  
        String str2 = "123";  
  
        System.out.println(str1+str2); // "123"+"123"="123123"  
        int num = Integer.parseInt(str1)+Integer.parseInt(str2); // 123+ 123 = 246 
        System.out.println(num);  // 246

		int su1 = 123;
		int su2 = 123;
		// su1 + su2 = 246
		String str = String.valueOf(su1) + String.valueOf(su2) // "123123"

		str = (su1+"") + (su2+""); // 이것도 가능 "123123"
    }  
  
}
```

## Collection Framework API란
- Java에서 제공하는 데이터 구조인 컬렉션을 표현하는 인터페이스와 클래스의 모음
- 개발자가 데이터를 저장하고 관리하는 다양한 방법을 제공
- `List` : **순서가 있는 객체 다루는 인터페이스**
	- `ArrayList` : List 인터페이스 구현 클래스
	- `LinkedList` : List 인터페이스 구현 클래스 
- `Set` : **중복된 원소가 없는 객체의 모음을 다루는 인터페이스**
	- `HashSet` : Set 인터페이스 구현 클래스
	- `TreeSet` : SortedSet 인터페이스 구현 클래스
- `Map` : **키-값 쌍의 객체를 다루는 인터페이스**
	- `HashMap` : Map 인터페이스 구현 클래스
	- `TreeMap` : SortedMap 인터페이스 구현 클래스

## 순서가 있고 중복 가능한 List API
- `List` 구현 클래스 중 `ArrayList` 사용
```Java
public class MovieListExample {  
  
    public static void main(String[] args) {  
        ArrayList<Movie> list = new ArrayList<Movie>(); // Movie[]  
        list.add(new Movie("괴물", "봉준호", "2006", "한국"));  
        list.add(new Movie("기생충", "봉준호", "2019", "한국"));  
        list.add(new Movie("완벽한 타인", "이재규", "2018", "한국"));  
  
        for(Movie movie : list){  
            System.out.println(movie);  
        }  
  
        String searchTitle = "기생충";  
        // 순차검색->이진검색(*)  
        for(Movie m : list){  
            if(m.getTitle().equals(searchTitle)){  
                System.out.println(m);  
                break;            }  
        }  
    }  
  
}
```

## 순서가 없고 중복 불가능한 Set API
- `set`의 구현 클래스 `HashSet`
- 중복 X
- `add()` 추가
- `contains()` 포함 -> T/F
- `remove()` 삭제
- `clear()` set 초기화
- `isEmpty()` 비었는지 -> T/F
```Java
public class HashSetExample {  
  
    public static void main(String[] args) {  
        Set<String> set = new HashSet<>();  
  
        set.add("Apple");  
        set.add("Banana");  
        set.add("Cherry");  
        set.add("Apple"); // 중복 X  
        System.out.println("size : " + set.size());  
  
        for (String str : set) {  
            System.out.println(str);  
        }  
  
        set.remove("Banana");  
  
        System.out.println("size : " + set.size());  
  
        for (String str : set) {  
            System.out.println(str);  
        }  
  
        boolean contains = set.contains("Cherry");  
        System.out.println("Does Set contain Cherry? " + contains);  
  
        set.clear();  
        ;        boolean empty = set.isEmpty();  
        System.out.println("Is set cleared? " + empty);  
    }  
  
  
}
```

```Java
public class UniqueNumbers {  
  
    public static void main(String[] args) {  
        int[] nums = {1,2,3,4,5,6,7,1,2,3};  
  
        Set<Integer> uniqueNums = new HashSet<>();  
  
        for(int number : nums){  
            uniqueNums.add(number);  
        }  
  
        System.out.println("Unique numbers .....");  
        for(int n : uniqueNums){  
            System.out.println(n);  
        }  
    }  
}
```

## Key-Value로 관리하는 Map API
- key는 중복 X
- `get()` 조회
- `put(key, value)`
	- 추가 or 수정
- `remove()` 삭제 -> 없으면 `NULL` 반환
- `entrySet()` : Entry<> 한 쌍
	- `Map.Entry<type1, type2>` : Entry 타입

```Java
public class MapExample {  
  
    public static void main(String[] args) {  
        Map<String, Integer> stdScores = new HashMap<>();  
  
        stdScores.put("Kim", 95);  
        stdScores.put("Lee", 100);  
        stdScores.put("Park", 85);  
        stdScores.put("Choi", 90);  
  
        System.out.println("Kim's score = " + stdScores.get("Kim"));  
        System.out.println("Lee's score = " + stdScores.get("Lee"));  
  
        stdScores.put("Kim", 59); // KIM의 value 수정  
        System.out.println("Kim's score = " + stdScores.get("Kim"));  
  
        for(Map.Entry<String, Integer> entry : stdScores.entrySet()){  
            System.out.println("key-val = " + entry.getKey() + entry.getValue());  
        }  
    }  
}
```

```Java
public class CharacterCount {  
  
    public static void main(String[] args) {  
        String str = "Hello, World";  
        Map<Character, Integer> charCountMap = new HashMap<>();  
        char[] strArray = str.toCharArray();  
  
        for(char c : strArray){  
            if(charCountMap.containsKey(c)){  
                charCountMap.put(c, charCountMap.get(c)+1);  
            } else{  
                charCountMap.put(c,1);  
            }  
        }  
  
        System.out.println("Char Counts");  
        for(char c : charCountMap.keySet()){  
            System.out.println(c + " : " + charCountMap.get(c));  
        }  
    }  
  
}
```

- `toCharArray()` : String을 char 배열로 변환