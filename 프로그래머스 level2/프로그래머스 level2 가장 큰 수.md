## 프로그래머스 level2 가장 큰 수 

문제설명: 0 또는 양의 정수가 주어졌을 때, 정수를 이어 붙여 만들 수 있는 가장 큰 수를 알아내 주세요.

예를 들어, 주어진 정수가 [6, 10, 2]라면 [6102, 6210, 1062, 1026, 2610, 2106]를 만들 수 있고, 이중 가장 큰 수는 6210입니다.

0 또는 양의 정수가 담긴 배열 numbers가 매개변수로 주어질 때, 순서를 재배치하여 만들 수 있는 가장 큰 수를 문자열로 바꾸어 return 하도록 solution 함수를 작성해주세요.

##### 제한 사항

- numbers의 길이는 1 이상 100,000 이하입니다.
- numbers의 원소는 0 이상 1,000 이하입니다.
- 정답이 너무 클 수 있으니 문자열로 바꾸어 return 합니다.

##### 입출력 예

| numbers           | return  |
| ----------------- | ------- |
| [6, 10, 2]        | 6210    |
| [3, 30, 34, 5, 9] | 9534330 |

___

```
#include <string>
#include <vector>
#include <algorithm>
using namespace std;

bool compare(string a, string b)//문자열 크기 비교 
{
	return a + b > b + a;
}

string solution(vector<int> numbers) {
	string answer = "";
	
	vector<string> s_num;
	
	for (int i = 0; i < numbers.size(); i++)
	{
		s_num.push_back(to_string(numbers[i]));//문자열로 저장
	}
	
	sort(s_num.begin(), s_num.end(), compare);//주어진 문자열을 크기순서로 정렬을 한다

	for (int i = 0; i < numbers.size(); i++)
	{
		if (s_num.at(0) == "0")//처음 숫자가 0일경우 0을 반환하도록 한다 
			return "0";
		answer += s_num[i];
	}


	return answer;
}
```

이 문제는 각 숫자를 조합해서 가장 큰 수를 만들어내는 문제인데 반환하는 값을 문자열로 하는것이 조건입니다. 그래서 저는 먼저 주어진 int형 숫자들을 string형으로 변환해서 새로운 벡터에 저장을 한후에 문자열을 compare이라는 비교함수를 만들어서 정렬을 했습니다. 

정렬한 문자열들을 answer값에 더해주면 가장 큰 값이 만들어지게 됩니다. 이때, 첫 문자가 0일 경우"0"을 리턴안시켜주면 0이 안나오게 되어 이부분을 예외적으로 처리해주어야 합니다.



사용언어: c++

출처: https://programmers.co.kr/learn/courses/30/lessons/42746