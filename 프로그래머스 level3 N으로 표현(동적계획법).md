## 프로그래머스 level3 N으로 표현(동적계획법)

###### 문제 설명

아래와 같이 5와 사칙연산만으로 12를 표현할 수 있습니다.

12 = 5 + 5 + (5 / 5) + (5 / 5)
12 = 55 / 5 + 5 / 5
12 = (55 + 5) / 5

5를 사용한 횟수는 각각 6,5,4 입니다. 그리고 이중 가장 작은 경우는 4입니다.
이처럼 숫자 N과 number가 주어질 때, N과 사칙연산만 사용해서 표현 할 수 있는 방법 중 N 사용횟수의 최솟값을 return 하도록 solution 함수를 작성하세요.

##### 제한사항

- N은 1 이상 9 이하입니다.
- number는 1 이상 32,000 이하입니다.
- 수식에는 괄호와 사칙연산만 가능하며 나누기 연산에서 나머지는 무시합니다.
- 최솟값이 8보다 크면 -1을 return 합니다.

##### 입출력 예

| N    | number | return |
| ---- | ------ | ------ |
| 5    | 12     | 4      |
| 2    | 11     | 3      |

##### 입출력 예 설명

예제 #1
문제에 나온 예와 같습니다.

예제 #2
`11 = 22 / 2`와 같이 2를 3번만 사용하여 표현할 수 있습니다.

___

다음은 동적계획법으로 접근하기 전에 경우의 수를 생각하며 작성한 코드입니다..

테스트케이스는 통과했지만 예외인 경우가 있어 전체적인 통과는 하지 못했습니다.

다음 코드는 재귀 DFS를 활용하여 작성해본 코드입니다.

```
#include <string>
#include <vector>
#include <algorithm>
#include <iostream>

using namespace std;


int check(int n, int number);
int string_check(string t, int number, int n);
int cmp(int a, int b);

int solution(int N, int number) {
	int answer = 0;
	string temp = "";
	string sub = to_string(N);
	int c1, c2;
	int length = to_string(number).length();
	//cout << length;
	for (int i = 0; i < length; i++)
	{
		temp += sub;
	}
	//cout << temp;
	c1 = string_check(temp, number, N);
	c2 = check(N, number);
	cout << c2 << " " << c1 << endl;

	answer = cmp(c1, c2);
	cout << answer;

	if (answer > 8)
		answer = -1;

	return answer;
}

int check(int n, int number)
{
	string temp = "";
	int sum = 0;
	int count = 0;
	while (sum <= number)
	{
		if (number < (sum + n))
		{
			int x = number - sum;//x는 표현할 수 없는 차이 1로 그만큼 더해가야함
			//1을 만들때 최소 n을 자기 자신으로 나누므로 2번필요
			count = count + x * 2;
			break;
		}

		sum += n;
		count++;//N의 사용횟수

	}

	return count;
}
int string_check(string t, int number, int n)
{
	int count2 = 2;//기본 n을 2번 이어 붙인 2자리수를 이용하므로 2부터시작
	int count3 = 2;
	int idx = stoi(t);
	int sum = 0;
	while (1)
	{
		sum = idx / n;//먼저 나눠보기
		count2++;
		if (sum > number)//넘은 만큼 빼야하므로
		{
			int x = sum - number;
			if (x == n)
			{
				count2++;
				if (count2 > 8)
				{
					count2 = 9;
					break;
				}
				break;
			}
			count2 = count2 + x * 2;
			if (count2 > 8)
			{
				count2 = 9;
				break;
			}
			break;
		}
		else {//나눈 합이 더 적을경우
			int x = number - sum;
			if (x == n)
			{
				count2++;
				if (count2 > 8)
				{
					count2 = 9;
					break;
				}
				break;
			}
			else
			{
				count2 = count2 + x * 2;
				if (count2 > 8)
				{
					count2 = 9;
					break;
				}
			}
		}
	}
	sum = 0;
	sum = idx + n;
	count3++;
	while (1)//바로 더해보기
	{
		sum /= n;
		count3++;
		if (sum == number)
			break;
		else if (sum < number)
		{
			int y = number - sum;
			count3 = count3 + 2 * y;
			break;
		}
	}

	return cmp(count2, count3);;
}
int cmp(int a, int b)//최소값 찾기 위한 비교함수
{
	if (a > b)
		return b;
	else
		return a;
}
```

```
#include <string>
#include <vector>
#include <algorithm>
#include <iostream>

using namespace std;

int answer = 9;//최소값 비교를 위해 MAX값 보다큰 9를 넣어둠 

void DFS(int n, int number, int count,int cur)
{
	if (count >= 9)
		return;
	if (cur == number)
	{
		answer = min(answer, count);
		return;
	}

	int temp = 0;
	for (int i = 0; i + count< 9; i++)//최대 사용이 9번이므로
	{
		temp = temp * 10 + n;
		DFS(n, number, count + i + 1, cur + temp);//사칙연산 시행
		DFS(n, number, count + i + 1, cur - temp);
		DFS(n, number, count + i + 1, cur * temp);
		DFS(n, number, count + i + 1, cur / temp);
	}
}

int solution(int N, int number) {
	
	DFS(N, number, 0, 0);

	if (answer==9 )
		return -1;

	return answer;
}


```

___

문제 해설: 탐색횟수가 9를 넘지않게 제한이 되어있어서 DFS로 접근해서 풀어볼 수 있었습니다.

1. 문제에서 주어진 N의 사용횟수가 최소가 되면서 number를 만족하는 수식을 만들기위해 사칙연산을 종류별로 실행합니다.
2. 문제설명에서 나와있듯이 주어진 N, NN, NNN이런식으로 표현되어 나타날 수 있으니 계속해서 자릿수를 늘려갑니다.
3. 현재값이 요구된 number값과 같으면 answer값과 비교하여 둘중의 최소값을 리턴하고 만약 answer의 초기값인 9 가 리턴되면 -1을 출력하도록 합니다.



동적계획법으로 분류된 문제인만큼 점화식을 파악하고 문제를 접근해야하나 DP방식으로는 표현하기가 어려워서 최소한의 조건이 있는만큼 DFS로 접근해서 풀어보았습니다. 풀이 방식을 다양하게 접근할 수 있는 경험이 중요하다고 생각되는 문제였습니다.



사용언어: c++

출처: https://programmers.co.kr/learn/courses/30/lessons/42895#

