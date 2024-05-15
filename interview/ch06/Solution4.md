
``` java
public static String mostCommonWord(String paragraph, String[] banned) {
        String[] s = paragraph.replaceAll("\\W+", " ").toLowerCase().split(" ");
        HashMap<String, Integer> wordMap = new HashMap<>();
        List<String> bannedList = Arrays.stream(banned).collect(Collectors.toList());

        String result = "";
        int max = 0;
        for (String s1 : s) {
            if (bannedList.contains(s1)) {
                continue;
            }
            Integer count = wordMap.get(s1);
            if (count == null) {
                wordMap.put(s1, 1);
            } else {
                wordMap.replace(s1, count + 1);
            }

            if (wordMap.get(s1) > max) {
                result = s1;
                max = wordMap.get(s1);
            }
        }

        return result;
    }
```


``` java

public static String mostCommonWordUseCollection(String paragraph, String[] banned) {
        // \w -> 문자, \W -> 문자아님, + -> 연속적인 값 ==> \\W+ -> 연속적으로 문자가 아닌 값
        String[] s = paragraph.replaceAll("\\W+", " ").toLowerCase().split(" ");

        // 배열 -> Set으로 변환
        /**
         * - Set은 중복을 허용하지 않고, 내부적으로 해시 테이블을 사용하는 구조이므로 해당 값을 해시함수를 이용해서 빠르게 검색한다. -> contains 메서드를 수행하는 데 걸리는 시간은 O(1)
         * - ArrayList는 내부적으로 배열을 사용하는 구조 -> 해당 값이 존재하는지 리스트의 요소를 순차적으로 비교하여 검색하므로 contains를 수행하는 데 걸리는 시간은 리스트의 길이에 비례한다 O(n)
         */
        Set<String> ban = new HashSet<>(Arrays.asList(banned));
        HashMap<String, Integer> wordMap = new HashMap<>();

        for (String w : s) {
            if (!ban.contains(w)) {
                // getOrDefault(key, defaultValue); -> 값이 존재하지 않으면 default value return ¬L
                wordMap.put(w, wordMap.getOrDefault(w, 0) + 1);
            }
        }


        // Collections.max(max 값을 찾을 Collection, max 값 비교 기준(Comparator)) -> 가장 큰 값을 찾음
        return Collections.max(wordMap.entrySet(), Map.Entry.comparingByValue()).getKey();
    }

```
