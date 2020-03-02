## 2020 KAKAO BLIND RECRUITMENT 문자열 압축

문제설명: 데이터 처리 전문가가 되고 싶은 **어피치**는 문자열을 압축하는 방법에 대해 공부를 하고 있습니다. 최근에 대량의 데이터 처리를 위한 간단한 비손실 압축 방법에 대해 공부를 하고 있는데, 문자열에서 같은 값이 연속해서 나타나는 것을 그 문자의 개수와 반복되는 값으로 표현하여 더 짧은 문자열로 줄여서 표현하는 알고리즘을 공부하고 있습니다.
간단한 예로 aabbaccc의 경우 2a2ba3c(문자가 반복되지 않아 한번만 나타난 경우 1은 생략함)와 같이 표현할 수 있는데, 이러한 방식은 반복되는 문자가 적은 경우 압축률이 낮다는 단점이 있습니다. 예를 들면, abcabcdede와 같은 문자열은 전혀 압축되지 않습니다. 어피치는 이러한 단점을 해결하기 위해 문자열을 1개 이상의 단위로 잘라서 압축하여 더 짧은 문자열로 표현할 수 있는지 방법을 찾아보려고 합니다.

예를 들어, ababcdcdababcdcd의 경우 문자를 1개 단위로 자르면 전혀 압축되지 않지만, 2개 단위로 잘라서 압축한다면 2ab2cd2ab2cd로 표현할 수 있습니다. 다른 방법으로 8개 단위로 잘라서 압축한다면 2ababcdcd로 표현할 수 있으며, 이때가 가장 짧게 압축하여 표현할 수 있는 방법입니다.

다른 예로, abcabcdede와 같은 경우, 문자를 2개 단위로 잘라서 압축하면 abcabc2de가 되지만, 3개 단위로 자른다면 2abcdede가 되어 3개 단위가 가장 짧은 압축 방법이 됩니다. 이때 3개 단위로 자르고 마지막에 남는 문자열은 그대로 붙여주면 됩니다.

압축할 문자열 s가 매개변수로 주어질 때, 위에 설명한 방법으로 1개 이상 단위로 문자열을 잘라 압축하여 표현한 문자열 중 가장 짧은 것의 길이를 return 하도록 solution 함수를 완성해주세요.

아래는 코드입니다.

___

```
#include <string>
#include <vector>

using namespace std;

int cut(string s, int cut_num);


int solution(string s) {
	int answer = s.length();
	int s_length = s.length() / 2;
	
	
	for (int i = 1; i <= s_length; i++)
	{

		int result = cut(s, i);
		
		if (result < answer)
			answer = result;
	}
	return answer;
}

int cut(string s, int cut_num)
{
	vector<string>sub;
	string temp = "";
	int count;

	if (s.length() % cut_num == 0)//딱 나누어 떨어질때
	{
		count = s.length() / cut_num;
	}
	else
	{
		count = s.length() / cut_num + 1;
	}

	for (int j = 0; j < count; j++)
	{
		sub.push_back(s.substr(j*cut_num, cut_num));
	}
	for (int x = 0; x < count; x++)
	{
		int y;
		for (y = x + 1; y < count; y++) {
			if (sub[x].compare(sub[y]) != 0)
				break;
		}
		if (y == x + 1)
			temp += sub[x];
		else
		{
			temp += to_string(y - x) + sub[x];
			y = x - 1;
		}
	}
	
	return temp.length();
}
```

이 문제에서는 문자열을 잘라서 비교할 수 있는 알고리즘을 구성하는 것이 가장 큰 핵심이라고 생각합니다. 문자열을 자르기 위해서 C++의 substr 함수를 이용해서 압축길이에 따른 자른 문자열을 비교했습니다. 

substr은 자르고자 하는 문자열(위의 코드의 경우 s) s.substr(시작하는 위치, 자르고싶은 길이)를 입력해서 사용하는 함수입니다. 그리고 문제 조건에서 반복되는 문자열의 경우 abab이면 2로 잘랐을때 2ab로 새로 압축이 되어야하므로 자른 to_string을 통해 int형으로 변환 시켜준뒤 이것을 다시 문자열에 붙여주는 작업이 필요합니다.

위와 같은 작업을 반복 실행해준뒤 가장 길이가 짧게 생성된 문자열을 반환해주면 되는 문제였습니다.



사용언어: c,c++

출처: https://programmers.co.kr/learn/courses/30/lessons/60057