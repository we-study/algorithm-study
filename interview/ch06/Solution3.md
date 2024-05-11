
https://leetcode.com/problems/reorder-data-in-log-files/

1. 배열만 사용한 풀이 -> 12ms 

``` java

public static String[] reorderLogFile(String[] logs) {
        int length = logs.length;
        String[] result = new String[length];
        String[][] letters = new String[length][];
        int l = 0;
        int d = length-1;

        // digits 먼저 입력 순으로 정렬
        for (int i = length-1; i >= 0; i--) {
            if (logs[i].charAt(logs[i].length()-1) < 'a') {
                result[d] = logs[i];
                d--;
            } else {
                letters[l] = logs[i].split(" ");
                l++;
            }
        }

        // letters -> 사전, 식별자 순으로 정렬
        for (int i = 0; i < l-1; i++) {
            for (int j = i+1; j < l; j++) {
                String[] left = letters[i];
                String[] right = letters[j];
                int size = Math.min(left.length, right.length); // 3
                int idx = 1;
                while (idx < size) {
                    if (right[idx].compareTo(left[idx]) == 0) {
                        idx++;
                    } else if (right[idx].compareTo(left[idx]) < 0) {
                        switchArray(letters, i, j);
                        break;
                    } else {
                        break;
                    }
                }
                if (idx == size) {
                    if (left.length > right.length) {
                        switchArray(letters, i, j);
                    } else if (left.length == right.length && right[0].compareTo(left[0]) < 0) {
                        switchArray(letters, i, j);
                    }
                }
            }
        }

        for (int i = 0; i < l; i++) {
            String letter = "";
            for (String s: letters[i]) {
                letter += " " + s;
            }
            result[i] = letter;
        }
        return result;
    }

    private static void switchArray(String[][] letters, int left, int right) {
        String[] tmp = letters[left];
        letters[left] = letters[right];
        letters[right] = tmp;
    }

```


2. 람다 사용한 풀이 -> 4ms

``` java
// 람다 표현식
arrayList.sort((x1, x2) -> {
....
}
```

``` java
Character.isDigit() // 숫자면 true 반환
Character.isLetter() // 문자면 true 반환

```

``` java

// 리스트를 배열로 변환하기
arrayList.toArray(new String[0]);

```





- 람다가 3배나 빠름

``` java
        List<String> digits = new ArrayList<>();
        List<String> letters = new ArrayList<>();


        // Character.isDigit 을 사용해서 숫자와 문자 로그 분리
        for (String log : logs) {
            if (Character.isDigit(log.charAt(log.length()-1))) {
                digits.add(log);
            } else {
                letters.add(log);
            }
        }

        // 람다로 문자로그 정렬
        letters.sort((s1, s2) -> {
            String[] s1x = s1.split(" ", 2);
            String[] s2x = s2.split(" ", 2);

            int compare = s1x[1].compareTo(s2x[1]);
            if (s1x[1].compareTo(s2x[1]) == 0) {
                return s1x[0].compareTo(s2x[0]);
            } else {
                return compare;
            }
        });
        letters.addAll(digits);

        // 리스트를 String 배열로 변환
        return letters.toArray(new String[0]);
```
