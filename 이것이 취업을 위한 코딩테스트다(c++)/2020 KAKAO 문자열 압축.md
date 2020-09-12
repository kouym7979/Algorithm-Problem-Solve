## 2020 KAKAO 문자열 압축

```
#include <string>
#include <vector>
#include <algorithm>

using namespace std;


int solution(string s) {
	int answer = s.length();
	
	for (int i = 1; i<=s.length() / 2; i++)
	{
		int pos = 0;
		int len = s.length();//압축이 된길이 표현

		while(1)
		{
			string u = s.substr(pos, i);//한글자씩 잘라서 비교할 문자확인
			pos += i;

			if (pos >= s.length())
				break;

			int cnt = 0;
			while(1)
			{
				if (u.compare(s.substr(pos, i)) == 0)//다음글자와 같다면
				{
					cnt++;
					pos += i;//위치도 이동
				}
				else
					break;
			}

			if (cnt > 0) {
				len -= i * cnt;
				
				if (cnt < 9) len += 1;
				else if (cnt < 99) len += 2;
				else if (cnt < 999) len += 3;
				else
					len += 4;
			}
		}
		answer = min(answer, len);
	}
	

	return answer;
}
```

___

사용언어:c++

문제출처:https://programmers.co.kr/learn/courses/30/lessons/60057#qna