https://leetcode.com/problems/group-anagrams/

- List.of(), Arrays.asList() -> immutable list, add() 메서드를 사용하려고 하면 UnsupportedOperationException 예외를 발생시킨다.
- new ArrayList<>() -> mutable list

``` java
public static List<List<String>> groupAnagrams(String[] strs) {

        
        Map<String, List<String>> stringMap = new HashMap<>();
        for (String str : strs) {
            char[] chars = str.toCharArray();
            Arrays.sort(chars);
            String key = String.valueOf(chars);
            // stringMap.containsKey(key);로 새로운 key인지 확인할 수도 있다
            List<String> stringList = stringMap.getOrDefault(key, new ArrayList<>());
            stringList.add(str);
            stringMap.put(key, stringList);
        }

        return new ArrayList<>(stringMap.values());
    }
```
