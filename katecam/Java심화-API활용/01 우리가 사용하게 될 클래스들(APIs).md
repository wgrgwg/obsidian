1. 직접 구현
2. JDK 내부 Java 제공 API
3. Others API

## 직접 구현하는 Class들
#### 배열의 최대값, 최소값 구하는 클래스
- `MinMaxFiner` 클래스
- **Utility** 타입
- static으로 생성 -> 클래스명으로 호출
- 배열의 첫 번째 값을 대입해주고, 나머지를 순회하며 업데이트

```Java
public class MinMaxFinder {  
  
    private MinMaxFinder() {  
    }  
  
    public static int findMin(int[] arr) {  
        int min = arr[0]; // 초기값  
        for (int i = 1; i < arr.length; i++) {  
            if (arr[i] < min) {  
                min = arr[i];  
            }  
        }  
  
        return min;  
    }  
  
    public static int findMax(int[] arr) {  
        int max = arr[0]; // 초기값  
        for (int i = 1; i < arr.length; i++) {  
            if (arr[i] > max) {  
                max = arr[i];  
            }  
        }  
  
        return max;  
    }  
}
```

## Java에서 제공하는 클래스
#### Random 클래스
- 6개의 난수를 생성하여, 중복되지 않게 배열에 저장
- `rand.nextInt(x)` : 0 이상 x 미만의 난수를 반환

```Java
public static void main(String[] args) {  
    Random rand = new Random();  
  
    int[] arr = new int[6];  
    int i = 0; // 저장위치(pos)  
    while (i < 6) {  
        int num = rand.nextInt(45) + 1; // 1~45  
        boolean isDuplicate = false;  
        for (int j = 0; j < i; j++) {  
            if (arr[j] == num) {  
                isDuplicate = true;  
                break;            }  
        }  
        if (!isDuplicate) {  
            arr[i++] = num;  
        }  
    }  
  
    for(int num : arr){  
        System.out.println(num + " ");  
    }  
}
```

## 다운받아 사용하는 클래스
- Java API 다운받아 사용도 가능 -> `.jar` 파일
- `mvnrepository.com`
- `Gson` : 자바 객체를 JSON 형식으로 반환하거나, JSON 데이터를 자바 객체로 변환하는 라이브러리
	-  `fromJson()`, `toJson()`
- JSON
	- 경량의 데이터 교환 형식
	- 프로그래밍 언어나 플랫폼에 상관없이 데이터 교환하도록 해줌