# ✓ 문제 번호
2022 kakao blind recruitment 신고결과 받기




# 📝 문제 풀이 (내용)
중복 처리를 위해 set 사용

```java
import java.util.*;

class Solution {
    public int[] solution(String[] id_list, String[] report, int k) {
        int[] answer = new int[id_list.length];
        Map<String, Set<String>> reports = new HashMap<>();
        Map<String, Integer> reportCount = new HashMap<>();
        
        for(String rep : report){
            String reporter = rep.split(" ")[0];
            String reported = rep.split(" ")[1];
             reports.putIfAbsent(reporter, new HashSet<>());

            if (reports.get(reporter).add(reported)) {
                reportCount.put(reported, reportCount.getOrDefault(reported, 0) + 1);
            }
        }
        
        for(String reported : reportCount.keySet()){
            int count = reportCount.get(reported);
            if( count >= k ){
                for(int i = 0; i < id_list.length ; i++){
                    if(reports.containsKey(id_list[i])&&reports.get(id_list[i]).contains(reported)){
                        answer[i]++;
                    }
                }
            }
        }
        
        return answer;
    }
}
```





# 📚 참고

```java
class Solution {
    public int[] solution(String[] id_list, String[] report, int k) {
        List<String> list = Arrays.stream(report).distinct().collect(Collectors.toList());
        HashMap<String, Integer> count = new HashMap<>();
        for (String s : list) {
            String target = s.split(" ")[1];
            count.put(target, count.getOrDefault(target, 0) + 1);
        }

        return Arrays.stream(id_list).map(_user -> {
            final String user = _user;
            List<String> reportList = list.stream().filter(s -> s.startsWith(user + " ")).collect(Collectors.toList());
            return reportList.stream().filter(s -> count.getOrDefault(s.split(" ")[1], 0) >= k).count();
        }).mapToInt(Long::intValue).toArray();
    }
}
```
`List<String> list = Arrays.stream(report).distinct().collect(Collectors.toList());`

중복으로 신고하는 사용자를 distinct()를 이용해 처리하는 부분이 좋음.

```java
class Solution {
    public int[] solution(String[] id_list, String[] report, int k) {
        int[] answer = new int[id_list.length];
        ArrayList<User> users = new ArrayList<>();
        HashMap<String,Integer> suspendedList = new HashMap<>(); //<이름>
        HashMap<String,Integer> idIdx = new HashMap<String,Integer>(); // <이름, 해당 이름의 User 클래스 idx>
        int idx = 0;

        for(String name : id_list) {
            idIdx.put(name,idx++);
            users.add(new User(name));
        }

        for(String re : report){
            String[] str = re.split(" ");
            //suspendedCount.put(str[0], suspendedCount.getOrDefault(str[0],0)+1);
            users.get( idIdx.get(str[0])).reportList.add(str[1]);
            users.get( idIdx.get(str[1])).reportedList.add(str[0]);
        }

        for(User user : users){
            if(user.reportedList.size() >= k)
                suspendedList.put(user.name,1);
        }

         for(User user : users){
             for(String nameReport : user.reportList){
                 if(suspendedList.get(nameReport) != null){
                     answer[idIdx.get(user.name)]++;
                 }

             }
        }




        return answer;
    }
}

class User{
    String name;
    HashSet<String> reportList;
    HashSet<String> reportedList;
    public User(String name){
        this.name = name;
        reportList = new HashSet<>();
        reportedList = new HashSet<>();
    }
}
```
그리고 객체지향


-----
왜인지 자꾸 헤맸는데, 차근차근 시나리오를 생각해볼 것..!


