## 배열처럼 동작하는 API 설계
```Java
public class intArrayBasic {  
  
    public static void main(String[] args) {  
        // 정수 5개를 배열에 저장하고 출력  
        int[] nums=new int[5]; // 생성동작 : 고정길이(단점) -> 가변길이는?  
        nums[0] = 1; // 저장동작  
        nums[1] = 2;  
        nums[2] = 3;  
        nums[3] = 4;  
        nums[4] = 5;  
  
        // nums.length : 길이를 구하는 동작  
        for(int i=0; i<nums.length; i++){  
            int data = nums[i]; // 데이터를 가져오는 동작  
            System.out.println(data);  
        }  
  
        // 향상된 for문(foreach)  
        for(int data : nums){  
            System.out.println(data);  
        }  
    }
```
- API로 만들 수는 없나? -> 배열처럼 동작하는 클래스
	- 생성
	- 저장
	- 값 가져오기
	- 크기 구하기

## IntArray 클래스 설계, 활용
```Java
public class IntArray {  
    private static final int DEFAULT_CAPACITY = 5;  
    private int[] elements;  
    private int size = 0;  
  
    // 생성 동작  
    public IntArray(){  
        elements = new int[DEFAULT_CAPACITY];  
    }  
  
    // 배열 크기 가져오는 동작  
    public int size(){  
        return size;  
    }  
  
    // 값 가져오는 동작  
    public int get(int index){  
        if(index < 0 || index>=size){  
            throw new IndexOutOfBoundsException("범위초과");  
        }  
        return elements[index];  
    }  
  
    // 저장 동작  
    public void add(int element){  
        if(size==elements.length){  
            ensureCapacity(); // 공간 늘리기  
        }  
        elements[size++] = element;  
    }  
  
    private void ensureCapacity(){  
        int newCapacity = elements.length*2;  
        elements = Arrays.copyOf(elements, newCapacity);  
    }  
}
```

```Java
public class MyIntArrayTest {  
  
    public static void main(String[] args) {  
        IntArray list = new IntArray();  
        list.add(1);  
        list.add(2);  
        list.add(3);  
  
        System.out.println(list.get(0));  
        System.out.println(list.get(1));  
        System.out.println(list.get(2));  
  
        System.out.println(list.size());  
  
        for(int i = 0; i<list.size(); i++){  
            System.out.println(list.get(i));  
        }  
  
        //list.get(4); // 예외 발생  
        list.add(4);  
        list.add(5);  
        list.add(6);  
  
    }
```

- `Arrays.copyOf(list, newCapacity)` : 복사해서 새로운 배열을 생성

## BookArray 클래스 설계, 활용
- int가 아닌 사용자 정의 클래스 Book의 배열 설계
```Java
public class Book {  
    private String title;  
    private int price;  
    private String company;  
    private String author;  
  
    public Book() { // 디폴트 생성자  
    }  
  
    // 생성자메서드의 중복정의 (오버로딩)  
    public Book(String title, int price, String company, String author) {  
        this.title = title;  
        this.price = price;  
        this.company = company;  
        this.author = author;  
    }  
  
    //getter, setter  
    public String getTitle() {  
        return title;  
    }  
  
    public void setTitle(String title) {  
        this.title = title;  
    }  
  
    public int getPrice() {  
        return price;  
    }  
  
    public void setPrice(int price) {  
        this.price = price;  
    }  
  
    public String getCompany() {  
        return company;  
    }  
  
    public void setCompany(String company) {  
        this.company = company;  
    }  
  
    public String getAuthor() {  
        return author;  
    }  
  
    public void setAuthor(String author) {  
        this.author = author;  
    }  
  
    @Override  
    public String toString() {  
        return "Book{" +  
            "title='" + title + '\'' +  
            ", price=" + price +  
            ", company='" + company + '\'' +  
            ", author='" + author + '\'' +  
            '}';  
    }  
}
```

```Java
public static void main(String[] args) {  
    // 책 세 권의 데이터를 배열에 저장, 출력  
    BookArray list = new BookArray(); // 책, 길이 5    list.add(new Book("자바", 15000, "한빛", "홍길동"));  
    list.add(new Book("C++", 12000, "능률", "김복동"));  
    list.add(new Book("Python", 17000, "정보", "엄준식"));  
    Book vo = list.get(0);  
    System.out.println("vo = " + vo);  
  
    for(int i=0; i<list.size(); i++){  
        System.out.println(list.get(i));  
    }  
}
```

## ObjectArray 클래스 설계, 활용
- Object : 최상위 클래스
	- Object 클래스의 배열에는 **다양한 타입**의 데이터 저장 가능

```Java
public class ObjectArray {  
    private static final int DEFAULT_CAPACITY = 5;  
    private Object[] elements; // 다형성 배열!  
    private int size = 0;  
  
    // 생성 동작  
    public ObjectArray(){  
        elements = new Object[DEFAULT_CAPACITY];  
    }  
  
    // 배열 크기 가져오는 동작  
    public int size(){  
        return size;  
    }  
  
    // 값 가져오는 동작  
    public Object get(int index){  
        if(index < 0 || index>=size){  
            throw new IndexOutOfBoundsException("범위초과");  
        }  
        return elements[index];  
    }  
  
    // 저장 동작  
    public void add(Object element){  
        if(size==elements.length){  
            ensureCapacity(); // 공간 늘리기  
        }  
        elements[size++] = element;  
    }  
  
    private void ensureCapacity(){  
        int newCapacity = elements.length*2;  
        elements = Arrays.copyOf(elements, newCapacity);  
    }  
}
```

```Java
public class MyObjectArrayTest {  
  
    public static void main(String[] args) {  
        // A, B, C 객체를 배열(Object)에 저장하고 출력  
        ObjectArray list = new ObjectArray();  
        list.add(new A()); // Upcasting 발생!  
        list.add(new B()); // Object element = new B();  
        list.add(new C());  
  
        A a = (A) list.get(0); // 사용할 때 Downcasting        a.display();  
    }  
  
}
```

## ArrayList 클래스 활용
- 자바에서 제공하는 ArrayList 클래스
- 설명서 : 공식 스펙 -> `java.util`
- 생성자를 다음과 같이 활용도 가능
```Java
public ObjectArray(){  
    this(5); // 생성자 안에서 다른 생성자 호출  
}  
  
// 생성 동작  
public ObjectArray(int capacity) {  
    elements = new Object[capacity];  
}
```

```Java
public class ArrayListTest {  
  
    public static void main(String[] args) {  
        // ArrayList = ObejctArray  
        List list = new ArrayList(1); // 기본 크기 10        list.add(new Book("자바", 15000, "한빛", "홍길동"));  
        list.add(new Book("C++", 12000, "능률", "김복동"));  
        list.add(new Book("Python", 17000, "정보", "엄준식"));  
  
        Book b = (Book)list.get(0);  
        System.out.println(b); // JVM에서 자동으로 b.toString() 대신 호출  
    }  
}
```

- 다음과 같이 선언하면(제네릭) Downcasting 필요 X
	- `List<Book> list = new ArrayList<Book>();`
	- 특정 타입을 명시