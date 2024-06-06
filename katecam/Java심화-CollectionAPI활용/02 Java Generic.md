## Java 제네릭 타입의 이유
- 자바 **제네릭** : 데이터 타입을 일반화 시킴
	- 런타입에서 데이터 타입 결정
	- `List<String>`
- Object 보다 특정 타입으로 제한
	- 안전성을 보장
- 재사용성이 높아짐
- 제네릭 배열은 배열 생성 후 형변환
	- `array = (T[]) new Obejct[size];`

```Java
public class ObjectArr<T> {  
    private T[] array; // T는 아직 결정 X    private int size;  
  
    public ObjectArr(int size){  
        array = (T[])new Object[size];  
    }  
  
    public void set(int index, T value){  
        array[index] = value;  
        size++;  
    }  
  
    public T get(int index){  
        return array[index];  
    }  
  
    public int size(){  
        return size;  
    }  
  
}
```

```Java
public class GenericTest {  
  
    public static void main(String[] args) {  
        /*ObjectArr<String> array = new ObjectArr<>(5);  
        array.set(0, "Hello");        array.set(1, "World");        array.set(2, "Java");        array.set(3, "Generic");  
        for(int i=0; i<array.size(); i++){            System.out.println(array.get(i));        }*/  
        ObjectArr<Movie> bList = new ObjectArr<>(5);  
        bList.set(0, new Movie("괴물", "봉준호", "2006", "한국"));  
        bList.set(1, new Movie("기생충", "봉준호", "2019", "한국"));  
        bList.set(2, new Movie("완벽한 타인", "이재규", "2018", "한국"));  
  
        for(int i=0; i<bList.size(); i++){  
            System.out.println(bList.get(i));  
        }  
    }  
  
}
```

## Java 제네릭 타입이란
- 자바 제네릭 타입은 클래스, 인터페이스, 메소드 등에 사용가능한 **타입 매개변수**
- 타입 안정성을 보장

```Java
public class ArrayListGeneric {  
  
    public static void main(String[] args) {  
        List list = new ArrayList();  
        list.add(new Movie("괴물", "봉준호", "2006", "한국"));  
        list.add("Hello");  
        // 여러가지 타입을 저장 => 안정성 X 
        
        System.out.println(list.get(0));  
        System.out.println(list.get(1));  
    }  
  
}
```

## 제네릭 타입 멀티 파라미터
- 제네릭 타입을 여러개 선언해서 사용 가능
	- `HashMap<String, Integer>`

```Java
public class Pair<K, V> {  
  
    private K key;  
    private V value;  
  
    public Pair(K key, V value) {  
        this.key = key;  
        this.value = value;  
    }  
  
    public K getKey() {  
        return key;  
    }  
  
    public void setKey(K key) {  
        this.key = key;  
    }  
  
    public V getValue() {  
        return value;  
    }  
  
    public void setValue(V value) {  
        this.value = value;  
    }  
}
```

```Java
public class PairGenericTest {  
  
    public static void main(String[] args) {  
        Pair<String, Integer> pair = new Pair("hello", 1);  
        System.out.println(pair.getKey());  
        System.out.println(pair.getValue());  
    }  
}
```

## 제네릭 제한된 타입 파라미터
- 특정한 타입으로 제한된 타입 파라미터
- `<T extends Number>`
	- Number 클래스, 또는 하위 클래스의 타입만 사용 가능

```Java
public class AverageCalculator <T extends Number>{  
    private T[] numbers;  
  
    public AverageCalculator(T[] numbers) {  
        this.numbers = numbers;  
    }  
  
    public double calculateAverage(){  
        double sum = 0.0;  
        for(T n : numbers){  
            sum += n.doubleValue();  
        }  
  
        return sum/numbers.length;  
    }  
}
```

```Java
public class GenericLimitTest {  
  
    public static void main(String[] args) {  
        Integer[] integers = {1,2,3,4,5};  
        Double[] doubles = {1.0, 2.0, 3.0, 4.0, 5.0};  
  
        AverageCalculator<Integer> integerCalculator = new AverageCalculator<>(integers);  
        AverageCalculator<Double> doubleCalculator = new AverageCalculator<>(doubles);  
  
        System.out.println(integerCalculator.calculateAverage());  
        System.out.println(doubleCalculator.calculateAverage());  
    }  
}
```