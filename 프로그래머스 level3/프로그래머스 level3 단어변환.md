## 프로그래머스 level3 단어변환

###### 문제 설명

두 개의 단어 begin, target과 단어의 집합 words가 있습니다. 아래와 같은 규칙을 이용하여 begin에서 target으로 변환하는 가장 짧은 변환 과정을 찾으려고 합니다.

```
1. 한 번에 한 개의 알파벳만 바꿀 수 있습니다.
2. words에 있는 단어로만 변환할 수 있습니다.
```

예를 들어 begin이 hit, target가 cog, words가 [hot,dot,dog,lot,log,cog]라면 hit -> hot -> dot -> dog -> cog와 같이 4단계를 거쳐 변환할 수 있습니다.

두 개의 단어 begin, target과 단어의 집합 words가 매개변수로 주어질 때, 최소 몇 단계의 과정을 거쳐 begin을 target으로 변환할 수 있는지 return 하도록 solution 함수를 작성해주세요.

##### 제한사항

- 각 단어는 알파벳 소문자로만 이루어져 있습니다.
- 각 단어의 길이는 3 이상 10 이하이며 모든 단어의 길이는 같습니다.
- words에는 3개 이상 50개 이하의 단어가 있으며 중복되는 단어는 없습니다.
- begin과 target은 같지 않습니다.
- 변환할 수 없는 경우에는 0를 return 합니다.

##### 입출력 예

| begin | target | words                          | return |
| ----- | ------ | ------------------------------ | ------ |
| hit   | cog    | [hot, dot, dog, lot, log, cog] | 4      |
| hit   | cog    | [hot, dot, dog, lot, log]      | 0      |

##### 입출력 예 설명

예제 #1
문제에 나온 예와 같습니다.

예제 #2
target인 cog는 words 안에 없기 때문에 변환할 수 없습니다.

___

```
#include <string>
#include <vector>
#include <algorithm>
#include <iostream>


using namespace std;
int answer = 0;//몇 단계의 과정을 거쳐 변화 할 수 있는지 확인
//1개의 알파벳만 바꿀 수 있음. word에 있는 단어로만
int DFS(string b, vector<string>w, string t, int n)//begin, 단어집합, target ,위치 순
{
	int count = 0;//각 단어에서 몇글자가 다른지 확인
	int check = 0;
	if (b == t)//시작 단어가 타겟과 동일하면 탈출
		return answer;
	for (int x = 0; x < b.length(); x++)
	{
		if (b[x] != t[x])
		{
			check++;
		}
	}
	if (check == 1) {
		answer++;
		return answer;
	}
		
	for (int i = 0; i < b.length(); i++)//모든 단어의 길이는 똑같으므로
	{
		string temp = w[n];
		if (b[i] != temp[i])
		{
			count++;
		}
	}
	if (count > 1)
		DFS(b, w, t, n + 1);
	else if (count == 1)
	{
		b.clear();
		b = w[n];//1개만 다른 단어로 변경
		answer++;//1번 증가
		cout << b<<" "<<answer<<endl;//변경된 단어들 확인
		DFS(b, w, t, n + 1);
	}


	return answer;
}


int solution(string begin, string target, vector<string> words) {

	int check = false;
	string temp = "";

	for (int i = 0; i < words.size(); i++)
	{
		if (words[i] == target)//타겟이 단어 집합에 있으면 진행해도됨
			check = true;
	}
	if (check == false)
		answer = 0;
	else {
		DFS(begin, words, target, 0);
	}

	return answer;
}
```

___

문제설명: 

1. 먼저, 문제에서 주어진 조건인 단어집합인 words에서 target이 없으면 '0'을 반환해줍니다.
2. 찾고자하는 target이 있으면 탐색을 시작합니다.
3. 현재 진행되고있는 단어가 target과의 알파벳 개수가 1개 차이면 현재까지 계산된 answer에서 1을 더해주고 반환합니다.
4. 아닐경우 단어집합에서 알파벳이 1개만 차이가 나는 단어로 바꿔주며 word인덱스를 증가시켜줍니다. 이때 알파벳이 2개가 차이나면 바로 word인덱스를 증가시켜주며 위의 3번 과정을 반복합니다.



사용언어: c++

출처: https://programmers.co.kr/learn/courses/30/lessons/43163