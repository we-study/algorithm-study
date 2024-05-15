# 4. 자료형

## 원시자료형(primitive type) vs 참조자료형(reference type) 속도 차이
``` java
        int[] intEl = new int[MILLION];
        long start = System.currentTimeMillis();
        for (int i = 0; i < MILLION; i++) {
            intEl[i] = 1;
        }
        long end = System.currentTimeMillis();
        System.out.println("time for insert data : " + (end - start));

        intEl[MILLION - 1] = 2;

        int index = 0;

        long start2 = System.currentTimeMillis();
        while (intEl[index] != 2) {
            index++;
        }
        long end2 = System.currentTimeMillis();
        System.out.println("time for lookup data : " + (end2 - start2));
    }
```
primitive type :
//    time for insert data : 150ms
//    time for lookup data : 39ms

reference type : 
//    time for insert data : 333ms
//    time for lookup data : 50ms

- 참조형이 데이터 삽입은 2배, 찾기는 1.3배 더 걸림

## 원시형과 자료형의 메모리 점유 비교
- 원시형 int : 4바이트 (32비트)
- 참조형 Integer : 16바이트 (128비트)
  - 참조형 자바 객체를 보면 실제로 값이 보관되는 영역은 마지막 4바이트 / 나머지 12바이트는 모두 부가정보를 보관하는 헤더


