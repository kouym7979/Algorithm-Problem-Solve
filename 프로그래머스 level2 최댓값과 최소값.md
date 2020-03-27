## 프로그래머스 level2 최댓값과 최소값

###### 문제 설명

문자열 s에는 공백으로 구분된 숫자들이 저장되어 있습니다. str에 나타나는 숫자 중 최소값과 최대값을 찾아 이를 (최소값) (최대값)형태의 문자열을 반환하는 함수, solution을 완성하세요.
예를들어 s가 1 2 3 4라면 1 4를 리턴하고, -1 -2 -3 -4라면 -4 -1을 리턴하면 됩니다.

##### 제한 조건

- s에는 둘 이상의 정수가 공백으로 구분되어 있습니다.

##### 입출력 예

| s           | return |
| ----------- | :----: |
| 1 2 3 4     |  1 4   |
| -1 -2 -3 -4 | -4 -1  |
| -1 -1       | -1 -1  |

___

```
#include <string>
#include <vector>
#include <algorithm>
#include <iostream>


using namespace std;

//문자열중에서 최소값과 최대값을 찾아서 문자열로 반환하는 함수


string solution(string s) {

	string answer = "";
	string temp = "";
	int sub = 0;
	vector<int>sort_n;//문자열의 값들을 저장할 벡터

	for (int i = 0; i < s.length(); i++)
	{
		if (s.at(i) == '-')//음수를 만날경우
		{
			temp += s.at(i);
			temp += s.at(i + 1);
			i += 1;
			sub = stoi(temp);
			sort_n.push_back(sub);
			temp.erase();
		}
		else if (s.at(i) != ' ')//공백이 아닐경우
		{
			temp += s.at(i);
			sub = stoi(temp);
			sort_n.push_back(sub);
			temp.erase();
		}
	}

	sort(sort_n.begin(), sort_n.end());//오름차순 으로 정렬
	
	answer += to_string(sort_n.front());
	answer += ' ';//두 수를 구분할 공백
	answer += to_string(sort_n.back());
	return answer;
}
```

위의 경우는 테스트케이스는 전부 통과했지만 숫자가 한자리일 경우만 검사가 가능해서 테스트결과는 실패했습니다.

아래는 두자리 수 이상까지 검사할 수 있는 코드입니다.

```
#include <string>
#include <vector>
#include <algorithm>
#include <iostream>


using namespace std;

//문자열중에서 최소값과 최대값을 찾아서 문자열로 반환하는 함수


string solution(string s) {

	string answer = "";
	string temp = "";
	int sub = 0;
	vector<int>sort_n;//문자열의 값들을 저장할 벡터

	for (int i = 0; i < s.length(); i++)
	{
		if (s.at(i) != ' ')//공백을 만날때가지 수를 계속 푸쉬
		{
			temp += s.at(i);
		}
		else if (s.at(i) == ' ')//공백을 만나게 되면
		{
			sub = stoi(temp);//이전까지 넣은 수를 정수로 변환
			sort_n.push_back(sub);
			temp.erase();
		}
		if (i == s.length() - 1)//마지막까지 진행되면
		{
			sub = stoi(temp);//이전까지 넣은 수를 정수로 변환
			sort_n.push_back(sub);
			temp.erase();
		}
	}

	sort(sort_n.begin(), sort_n.end());//오름차순 으로 정렬
	
	answer += to_string(sort_n.front());
	answer += ' ';//두 수를 구분할 공백
	answer += to_string(sort_n.back());
	return answer;
}
```

___

문제해설: 

1. 문자열을 잘라서 정수로 저장할 벡터를 선언합니다.
2. 공백을 만나기 전까지 자른 문자열을 임시로 temp라는 문자열에 옮겨놓습니다
3. 공백을 만나면 temp에 지금까지 넣은 - 부호 또는 숫자를 int형으로 변환한뒤에 벡터에 푸쉬합니다.
4. 위의 과정을 주어진 문자열의 끝까지 실행하면 지금까지의 수들을 정렬하여 최소값과 최대값을 answer 문자열에 공백과 함께 넣어주면 마무리 됩니다.



사용언어 : c++

출처: https://programmers.co.kr/learn/courses/30/lessons/12939