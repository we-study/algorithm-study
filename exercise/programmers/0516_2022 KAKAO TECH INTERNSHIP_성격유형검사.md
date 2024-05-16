# ✓ 문제 번호
2022 KAKAO TECH INTERNSHIP_성격유형검사




# 📝 문제 풀이 (내용)
성격분석테스트를 진행한다.        
각 문항별로 지표와 점수를 배열로 받아 점수를 매기고, 배점이 높은 순 - 알파벳 순으로 타입을 리턴한다.
```java
import java.util.*;
class Solution {
    public String solution(String[] survey, int[] choices) {
        String answer = "";

		    Map<Integer, Integer> pointChart = new HashMap<>();
		    pointChart.put(1, 3);
		    pointChart.put(2, 2);
		    pointChart.put(3, 1);
		    pointChart.put(4, 0);
		    pointChart.put(5, 1);
		    pointChart.put(6, 2);
		    pointChart.put(7, 3);
		    String[] ch = {"R,T", "C,F", "J,M", "A,N"};
		
		    Map<String, Integer> typeMap = new HashMap<>();
		    String types = "";
		    int temp = 0;
		    for (int i = 0; i < choices.length; i++) {
		      if (choices[i] > 4) {
		        types = survey[i].substring(1, 2); 
		        temp = pointChart.get(choices[i]); 
		        typeMap.put(types, typeMap.getOrDefault(types, 0) + temp);
		
		      }
		      if (choices[i] < 4) {
		        types = survey[i].substring(0, 1);
		        temp = pointChart.get(choices[i]); 
		        typeMap.put(types, typeMap.getOrDefault(types, 0) + temp);
		      }
		    }
		    for (String s : ch) {
		      String t1 = s.split(",")[0];
		      String t2 = s.split(",")[1];
		   
				 answer += typeMap.getOrDefault(t1, 0) >= typeMap.getOrDefault(t2, 0) ?
		          t1 : t2;
		    }
        return answer;
    }
}
```




# 📚 참고
함수형 프로그래밍.      
이렇게 짜는 사람도 있다..! 
```java
import java.util.Arrays;
import java.util.Comparator;
import java.util.List;
import java.util.Map;
import java.util.function.Function;
import java.util.stream.Collectors;
import java.util.stream.IntStream;

class Solution {
    public String solution(String[] survey, int[] choices) {
        return new Survey(survey)
                .report(choices)
                .getReport();
    }

    public static class Report {
        private final String report;

        public Report(String report) {
            this.report = report;
        }

        public String getReport() {
            return report;
        }
    }

    public static class Survey {
        private final List<CharacterType> survey;

        public Survey(String[] survey) {
            this(Arrays.stream(survey)
                    .map(CharacterType::findType)
                    .collect(Collectors.toList()));
        }

        public Survey(List<CharacterType> survey) {
            this.survey = survey;
        }

        public Report report(int[] scores) {
            return IntStream.range(0, survey.size())
                    .mapToObj(i -> new Choice(survey.get(i), scores[i]))
                    .collect(Collectors.collectingAndThen(Collectors.toList(), this::report));
        }

        public Report report(List<Choice> choices) {
            Map<CharacterType, Integer> report = CharacterType.getAllTypes().stream()
                    .collect(Collectors.toMap(Function.identity(), __ -> 0));

            choices.forEach(choice -> report.put(choice.getCharacterType(), 
                    report.get(choice.getCharacterType()) + choice.score));

            return report.entrySet().stream()
                    .sorted(Comparator.comparing(entry -> entry.getKey().indicator))
                    .map(entry -> {
                        if (entry.getValue() > 0) {
                            return entry.getKey().getUpperElement();
                        }

                        return entry.getKey().getLowerElement();
                    })
                    .map(CharacterTypeElement::name)
                    .collect(Collectors.collectingAndThen(Collectors.joining(), Report::new));
        }
    }

    public static class Choice {
        private final CharacterType characterType;
        private final Integer score;

        public Choice(String characterType, Integer score) {
            this(CharacterType.findType(characterType), score);
        }

        public Choice(CharacterType characterType, Integer score) {
            if (characterType.isReversed()) {
                this.characterType = characterType.reverse();
                this.score = Math.abs(7 - score) + 1 - 4;
            } else {
                this.characterType = characterType;
                this.score = score - 4;
            }
        }

        public CharacterType getCharacterType() {
            return characterType;
        }

        public Integer getScore() {
            return score;
        }
    }

    public enum CharacterType {
        RT(1, false), TR(1, true),
        CF(2, false), FC(2, true),
        JM(3, false), MJ(3, true),
        AN(4, false), NA(4, true);

        private final Integer indicator;
        private final boolean isReversed;

        CharacterType(Integer indicator, boolean isReversed) {
            this.indicator = indicator;
            this.isReversed = isReversed;
        }

        public static CharacterTypeElement findDefaultElementByIndicator(int indicator) {
            return Arrays.stream(values())
                    .filter(type -> type.indicator.equals(indicator))
                    .findFirst()
                    .map(CharacterType::getLowerElement)
                    .orElseThrow();
        }

        public static CharacterType findType(String type) {
            return Arrays.stream(values())
                    .filter(characterType -> characterType.name().equals(type))
                    .findAny()
                    .orElseThrow();
        }

        public static List<CharacterType> getAllTypes() {
            return List.of(RT, CF, JM, AN);
        }

        public CharacterType reverse() {
            return findType(new StringBuilder(this.name()).reverse().toString());
        }

        public boolean isReversed() {
            return isReversed;
        }

        public CharacterTypeElement getLowerElement() {
            return CharacterTypeElement.findType(String.valueOf(this.name().charAt(0)));
        }

        public CharacterTypeElement getUpperElement() {
            return CharacterTypeElement.findType(String.valueOf(this.name().charAt(1)));
        }
    }

    public enum CharacterTypeElement {
        R, T, C, F, J, M, A, N;

        public static CharacterTypeElement findType(String element) {
            return Arrays.stream(values())
                    .filter(characterType -> characterType.name().equals(element))
                    .findAny()
                    .orElseThrow();
        }
    }
}
```
