## 2020 KAKAO BLIND RECRUITMENT 가사검색

###### 문제 설명

**[본 문제는 정확성과 효율성 테스트 각각 점수가 있는 문제입니다.]**

친구들로부터 천재 프로그래머로 불리는 **프로도**는 음악을 하는 친구로부터 자신이 좋아하는 노래 가사에 사용된 단어들 중에 특정 키워드가 몇 개 포함되어 있는지 궁금하니 프로그램으로 개발해 달라는 제안을 받았습니다.
그 제안 사항 중, 키워드는 와일드카드 문자중 하나인 '?'가 포함된 패턴 형태의 문자열을 뜻합니다. 와일드카드 문자인 '?'는 글자 하나를 의미하며, 어떤 문자에도 매치된다고 가정합니다. 예를 들어 `"fro??"`는 `"frodo"`, `"front"`, `"frost"` 등에 매치되지만 `"frame"`, `"frozen"`에는 매치되지 않습니다.

가사에 사용된 모든 단어들이 담긴 배열 `words`와 찾고자 하는 키워드가 담긴 배열 `queries`가 주어질 때, 각 키워드 별로 매치된 단어가 몇 개인지 **순서대로** 배열에 담아 반환하도록 `solution` 함수를 완성해 주세요.

### 가사 단어 제한사항

- `words`의 길이(가사 단어의 개수)는 2 이상 100,000 이하입니다.
- 각 가사 단어의 길이는 1 이상 10,000 이하로 빈 문자열인 경우는 없습니다.
- 전체 가사 단어 길이의 합은 2 이상 1,000,000 이하입니다.
- 가사에 동일 단어가 여러 번 나올 경우 중복을 제거하고 `words`에는 하나로만 제공됩니다.
- 각 가사 단어는 오직 알파벳 소문자로만 구성되어 있으며, 특수문자나 숫자는 포함하지 않는 것으로 가정합니다.

### 검색 키워드 제한사항

- `queries`의 길이(검색 키워드 개수)는 2 이상 100,000 이하입니다.

- 각 검색 키워드의 길이는 1 이상 10,000 이하로 빈 문자열인 경우는 없습니다.

- 전체 검색 키워드 길이의 합은 2 이상 1,000,000 이하입니다.

- 검색 키워드는 중복될 수도 있습니다.

- 각 검색 키워드는 오직 알파벳 소문자와 와일드카드 문자인 `'?'` 로만 구성되어 있으며, 특수문자나 숫자는 포함하지 않는 것으로 가정합니다.

- 검색 키워드는 와일드카드 문자인

   

  ```
  '?'
  ```

  가 하나 이상 포함돼 있으며,

   

  ```
  '?'
  ```

  는 각 검색 키워드의 접두사 아니면 접미사 중 하나로만 주어집니다.

  - 예를 들어 `"??odo"`, `"fro??"`, `"?????"`는 가능한 키워드입니다.
  - 반면에 `"frodo"`(`'?'`가 없음), `"fr?do"`(`'?'`가 중간에 있음), `"?ro??"`(`'?'`가 양쪽에 있음)는 불가능한 키워드입니다.

### 입출력 예

| words                                                     | queries                                         | result            |
| --------------------------------------------------------- | ----------------------------------------------- | ----------------- |
| `["frodo", "front", "frost", "frozen", "frame", "kakao"]` | `["fro??", "????o", "fr???", "fro???", "pro?"]` | `[3, 2, 4, 1, 0]` |

### 입출력 예에 대한 설명

- `"fro??"`는 `"frodo"`, `"front"`, `"frost"`에 매치되므로 3입니다.
- `"????o"`는 `"frodo"`, `"kakao"`에 매치되므로 2입니다.
- `"fr???"`는 `"frodo"`, `"front"`, `"frost"`, `"frame"`에 매치되므로 4입니다.
- `"fro???"`는 `"frozen"`에 매치되므로 1입니다.
- `"pro?"`는 매치되는 가사 단어가 없으므로 0 입니다.

___

```
#include <string>
#include <vector>
#include <algorithm>
#include <iostream>

using namespace std;

vector<int> solution(vector<string> words, vector<string> queries) {
	cin.tie(0);
	vector<int> answer;
	string temp = "";
	int leng = 0;
	bool check = false;

	for (int i = 0; i < queries.size(); i++)
	{
		temp = queries[i];
		leng = queries[i].length();
		int count = 0;
		check = false;
		for (int j = 0; j < words.size(); j++)
		{
			
			for (int k = 0; k < words[j].length(); k++)
			{
				if (words[j].length() != leng) {//길이가 다르면 다른 단어로
					check = false;
					break;
				}
				else {//길이가 같으면
					if (words[j][k] == temp[k] || temp[k] == '?') {
						check = true;
					}
					else if (words[j][k] != temp[k]){
						check = false;
						break;
					}
				}
			}
			if (check == true)
				count++;
		}
		answer.push_back(count);
	}

	return answer;
}
```

문제설명: 

1. queries문에 들어있는 단어의 길이와 word에서 비교할 단어의 길이를 먼저 비교해줍니다.
2. 길이가 같을경우 '?'나오기 전까지 check를 통해 확인을 하고 최종적으로 check가 true가 되면 count를 늘려주는 방식을 반복합니다.

이와 같이 선형구조로 작성을하면 테스트 케이스는 전부 통과하지만 일부 효율성 테스트에서는 시간초과가 발생합니다.

이 효율성 테스트를 통과하기 위해서는 트라이(Trie)자료구조, 또는 이분탐색을 이용해야 통과할 수 있습니다. 추가적인 코드도 작성하도록 하겠습니다.



사용언어:c++

출처:https://programmers.co.kr/learn/courses/30/lessons/60060