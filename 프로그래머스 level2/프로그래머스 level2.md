## 프로그래머스 level2

###### 문제 설명

전화번호부에 적힌 전화번호 중, 한 번호가 다른 번호의 접두어인 경우가 있는지 확인하려 합니다.
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

------

**알림**

2019년 5월 13일, 테스트 케이스가 변경되었습니다. 이로 인해 이전에 통과하던 코드가 더 이상 통과하지 않을 수 있습니다.

___

```
#include <string>
#include <vector>
#include <iostream>
#include <algorithm>

using namespace std;

bool solution(vector<string> phone_book) {
	bool answer = true;

	string temp = " ";
	int leng = 0;
	sort(phone_book.begin(), phone_book.end());//전화번호 길이 순으로 정렬

	for (int i = 0; i < phone_book.size(); i++)
	{
		temp = phone_book[i];
		if (i == phone_book.size() - 1)
			break;
		string sub = phone_book[i + 1];
		leng = temp.length();
		
		if (temp.compare(0, leng, sub, 0, leng) == 0)//접두에 해당이 되는경우
			answer = false;
		if (answer == false)
			break;
	}
	return answer;
}
```

___

문제설명: 전화번호부의 번호가 다른 전화번호의 접두어가 되는지 판단하는 문제

string의 compare 함수를 이용하여 풀었습니다.

비교할string.compare(begin,end,다른문자열,begin,end) 와 같은 형태로 작성합니다

해당 값은 0과 1 로 판단하며 0은 각 문자열의 begin에서 end까지 같은 형태임을 나타냅니다.



사용언어:c++

