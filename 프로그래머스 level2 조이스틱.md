## 프로그래머스 level2 조이스틱(탐욕법)

###### 문제 설명

조이스틱으로 알파벳 이름을 완성하세요. 맨 처음엔 A로만 이루어져 있습니다.
ex) 완성해야 하는 이름이 세 글자면 AAA, 네 글자면 AAAA

조이스틱을 각 방향으로 움직이면 아래와 같습니다.

```
▲ - 다음 알파벳
▼ - 이전 알파벳 (A에서 아래쪽으로 이동하면 Z로)
◀ - 커서를 왼쪽으로 이동 (첫 번째 위치에서 왼쪽으로 이동하면 마지막 문자에 커서)
▶ - 커서를 오른쪽으로 이동
```

예를 들어 아래의 방법으로 JAZ를 만들 수 있습니다.

```
- 첫 번째 위치에서 조이스틱을 위로 9번 조작하여 J를 완성합니다.
- 조이스틱을 왼쪽으로 1번 조작하여 커서를 마지막 문자 위치로 이동시킵니다.
- 마지막 위치에서 조이스틱을 아래로 1번 조작하여 Z를 완성합니다.
따라서 11번 이동시켜 "JAZ"를 만들 수 있고, 이때가 최소 이동입니다.
```

만들고자 하는 이름 name이 매개변수로 주어질 때, 이름에 대해 조이스틱 조작 횟수의 최솟값을 return 하도록 solution 함수를 만드세요.

##### 제한 사항

- name은 알파벳 대문자로만 이루어져 있습니다.
- name의 길이는 1 이상 20 이하입니다.

##### 입출력 예

| name   | return |
| ------ | ------ |
| JEROEN | 56     |
| JAN    | 23     |

___

다음은 코드입니다.

```
#include <string>
#include <vector>
#include <deque>

using namespace std;

int compare(int x, int y)
{
	if (x > y)
		return y;
	else
		return x;
}
int solution(string name) {
	int answer = 0;

	string temp(name.length(), 'A');//입력받은 알파벳의 길이만큼 A로 초기화
	//deque<bool>check(name.length(), true);//어느 위치의 알파벳이 다른지 미리 판단

	int count = 0;//몇번 이동했는지 횟수 비교를 위한 변수
	int i = 0;
	while (true) {
		if (temp == name)//문자열이 동일하면 종료
			break;
		int a, b = 0;
		count = 0;//매번 초기화
		for (int m = 0; m < name.length(); m++)
		{
			if (name[(i + m) % name.length()] != temp[(i + m) % name.length()])//오른쪽이동할경우
			{
				i = (i + m) % name.length();
				answer += m;//이동한 만큼 증가 시킨다.
				break;
			}
			else if (name[(i + name.length() - m) % name.length()] !=
				temp[(i + name.length() - m) % name.length()])//왼쪽으로 이동할경우
			{
				i = (i + name.length() - m) % name.length();
				answer += m;
				break;
			}
		}
		//위치 이동후에 이제 알파벳이 끝쪽에서 가까운지 앞쪽에서 가까운지를 판단
		a = 'Z' + 1 - name[i];//알파벳 끝쪽에서 가까운지 앞쪽에서 가까운지를 판단
		b = name[i] - 'A';//앞쪽에서 가까운지 판단
		count = compare(a, b);//둘중에 어느곳이 최소 이동인지
		answer += count;//이동 횟수 만큼 증가
		temp[i] = name[i];//같은 문자로 변경
	}
	return answer;
}
```

이 문제는 탐욕법에 기반한 문제로 최소의 경우를 구하는 문제인데요. level2의 문제중에서는 많이 까도로운 문제였던것 같습니다. 

처음에 문제를 읽어보았을때는 이게 무슨 말인가 싶었습니다....그래서 문제를 충족시킬 조건들을 먼저

나열해보면서 어떤 방식으로 접근을 할지 생각했습니다. 다음은 제가 생각한 조건을 충족시킬 순서입니다.

1. 주어진 name문자열과 같은 길이인 A로 이루어진 temp문자열을 만들어준다.
2. 왼쪽으로 이동했을때와 오른쪽으로 이동했을때 어느 경우가 먼저 다른 문자를 찾을 수 있는지 검사한다.(이 방법을 생각하는데 시간이 가장 많이 들었습니다.)
3. 먼저 도달한 위치의 알파벳에서 다시 Z에서 바꾸는게 가까운지 아니면 A에서 바꾸는 것이 가까운지 검사하여 그 횟수를 추가합니다.
4. 이를 name과 제가 생성한 temp 문자열이 같아질때까지 반복합니다.

이 순서들을 생각하기까지 deque를 써서 같은 유무를 판단하려고 false,true로 해서 접근을 했다가 시간 효율성만 떨어지고 막상 다풀고나니 필요가 없다는 것을 깨닫고 지워버렸습니다...

다음부턴 탐욕법관련 문제를 풀때는 조건들을 어떻게 풀어나갈지 알고리즘을 작성해두고 그거에 따라서 코드로 바꿔나가는 방식을 사용하도록 노력하겠습니다.



사용언어: c++

출처: https://programmers.co.kr/learn/courses/30/lessons/42860