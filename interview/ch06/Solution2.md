https://leetcode.com/problems/reverse-string/description/

``` java
public void reverseString(char[] s) {
            int end = s.length - 1;
            for (int i = 0; i < s.length / 2; i++) {
                char tmp = s[i];
                s[i] = s[end-i];
                s[end-i] = tmp;
            }
        }
```
