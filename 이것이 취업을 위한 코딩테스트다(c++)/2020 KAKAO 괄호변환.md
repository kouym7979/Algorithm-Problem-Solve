## 2020 KAKAO 괄호변환

```
#include <string>
#include <vector>
#include <stack>
#include <iostream>
#include <algorithm>

using namespace std;

bool cut(string s, int *pos)
{
	bool ret = true;
	
	stack<char> check;
	int left = 0, right = 0;
	for (int i = 0; i < s.length(); i++)
	{
		
		if (s[i] == '(') {
			check.push('(');
			left++;
			
		}
		else if ( s[i] == ')')
		{
			right++;
			if (check.empty())
			{
				ret = false;
			}
			else
				check.pop();
		}
		if (left == right) {//가장짧은 균형잡힌 문자열
			*pos = i + 1;
			return ret;
		}
	}
}

string solution(string p) {
	string answer = "";
	int pos;
	string u = "";
	string v = "";
	bool chk = false;
	if (p.length() == 0)//빈 문자열일 경우 빈 문자열 반환
		return answer;
	
	chk=cut(p, &pos);

	u = p.substr(0, pos);//균형잡힌 곳까지 u로 분리
	v = p.substr(pos, p.length()-pos);

	if (chk == true) {//균형잡힌 문자열일 경우 v를 1단계부터 수행한후 붙여서 반환
		return u+solution(v);
		
	}
	else
	{
		string temp = "(" + solution(v) + ")";

		for (int i = 1; i < u.length() - 1; i++) {
			if (u[i] == '(')
			{
				temp = temp + ')';
			}
			else
				temp = temp + '(';
		}
		answer = temp;
	}

	return answer;
}
```

___

문제설명: 문자열의 괄호짝을 확인하기위해서 자료구조 스택을 이용하여 풀이했습니다.



사용언어:c++

문제출처:https://programmers.co.kr/learn/courses/30/lessons/60058