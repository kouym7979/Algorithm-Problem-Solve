## 프로그래머스 level2 전화번호목록

문제설명: 전화번호부에 적힌 전화번호 중, 한 번호가 다른 번호의 접두어인 경우가 있는지 확인하려 합니다.
전화번호가 다음과 같을 경우, 구조대 전화번호는 영석이의 전화번호의 접두사입니다.

- 구조대 : 119
- 박준영 : 97 674 223
- 지영석 : 11 9552 4421

전화번호부에 적힌 전화번호를 담은 배열 phone_book 이 solution 함수의 매개변수로 주어질 때, 어떤 번호가 다른 번호의 접두어인 경우가 있으면 false를 그렇지 않으면 true를 return 하도록 solution 함수를 작성해주세요.

##### 제한 사항

- phone_book의 길이는 1 이상 1,000,000 이하입니다.
- 각 전화번호의 길이는 1 이상 20 이하입니다.

##### 입출력 예제

| phone_book                  | return |
| --------------------------- | ------ |
| [119, 97674223, 1195524421] | false  |
| [123,456,789]               | true   |
| [12,123,1235,567,88]        | false  |

##### 입출력 예 설명

입출력 예 #1
앞에서 설명한 예와 같습니다.

입출력 예 #2
한 번호가 다른 번호의 접두사인 경우가 없으므로, 답은 true입니다.

입출력 예 #3
첫 번째 전화번호, “12”가 두 번째 전화번호 “123”의 접두사입니다. 따라서 답은 false입니다.

____

```
#include <string>
#include <vector>
#include <algorithm>
using namespace std;

bool solution(vector<string> phone_book) {
	bool answer = true;
	int count = 0;
	int p_length = 0;

	sort(phone_book.begin(), phone_book.end());

	for (int i = 0; i < phone_book.size(); i++)
	{
		string temp = phone_book[i];//i번째의 문자열을 저장
		p_length = temp.length();
		for (int j = i+1; j < phone_book.size(); j++)
		{
			if (temp == phone_book[j].substr(0, p_length))//다른번호의 접두사인 경우가 있으면
			{
				count=1;
				break;
			}
		}
		if (count==1)
			break;
	}
	if (count == 1)
		answer = false;
	return answer;
}
```

이 문제는 해시에 관한 문제인데... 문제를 해석하면서 이건 굳이 해시로 푸는 것보다는 해당 문자열이 다른 문자열의 접두사만 되면 확인하면 되는 문제여서 파악하고자 하는 문자열을 저장하고 그 길이만큼 다른 문자열을 앞에서부터 비교했을때 하나라도 접두사 되는 경우가 있으면 false를 반환하도록 했습니다. 좀더 빨리 계산하기 위해서 입력받아온 전화번호부 목록을 길이순으로 정렬을하여 짧은 문자열부터 검사를 할 수 있도록 코드를 구성했습니다.

다음번에는 해시문제인만큼 해시를 사용해서도 한번 풀어보도록 하겠습니다.



사용언어: c++

출처: https://programmers.co.kr/learn/courses/30/lessons/42577