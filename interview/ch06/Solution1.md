``` java
class Solution {
    public boolean isPalindrome(String s) {
        String[] strings = s.strip().split("");
        int end = strings.length - 1;
        for (int i = 0; i < strings.length / 2; i++) {
            if (!strings[i].equals(strings[end - i])) {
                return false;
            }
        }
        return true;
    }
}
```

### 틀린이유
- 공백만 고려하고 대소문자, 특수문자 고려하지 않아서 test case 1개 틀림

### 해결방법
- 영문자가 아니면 모두 "" 으로 치환한 다음에 charAt으로 문자 하나하나 추출해서 비교

``` java
public class Solution1 {
    public boolean isPalindrome(String s) {
        String strings = s.replaceAll("[^A-Za-z0-9]", "").toLowerCase();
        int end = strings.length() - 1;
        for (int i = 0; i < strings.length() / 2; i++) {
            if (strings.charAt(i) != strings.charAt(end - i)) {
                return false;
            }
        }
        return true;
    }
}
```

### 1ms 풀이
- charAt으로 문자열 하나하나 비교, 최대 O(n/2)  
``` java
class Solution {
    public boolean isPalindrome(String s) {
        int start = 0;
        int end = s.length() - 1;

        while(start < end) {
            if (!Character.isLetterOrDigit(s.charAt(start))) {
                start++;
            } else if (!Character.isLetterOrDigit(s.charAt(end))) {
                end--;
            } else {
                if (Character.toLowerCase(s.charAt(start)) != Character.toLowerCase(s.charAt(end))) {
                    return false;
                }
                start++;
                end--;
            }
        }
        return true;
}
}
```
