## 프로그래머스 level2 소수찾기

문제설명: 

###### 문제 설명

한자리 숫자가 적힌 종이 조각이 흩어져있습니다. 흩어진 종이 조각을 붙여 소수를 몇 개 만들 수 있는지 알아내려 합니다.

각 종이 조각에 적힌 숫자가 적힌 문자열 numbers가 주어졌을 때, 종이 조각으로 만들 수 있는 소수가 몇 개인지 return 하도록 solution 함수를 완성해주세요.

##### 제한사항

- numbers는 길이 1 이상 7 이하인 문자열입니다.
- numbers는 0~9까지 숫자만으로 이루어져 있습니다.
- 013은 0, 1, 3 숫자가 적힌 종이 조각이 흩어져있다는 의미입니다.

##### 입출력 예

| numbers | return |
| ------- | ------ |
| 17      | 3      |
| 011     | 2      |

##### 입출력 예 설명

예제 #1
[1, 7]으로는 소수 [7, 17, 71]를 만들 수 있습니다.

예제 #2
[0, 1, 1]으로는 소수 [11, 101]를 만들 수 있습니다.

- 11과 011은 같은 숫자로 취급합니다.

___

```
#include <string>
#include <vector>
#include <algorithm>
#include <iostream>
#include <memory.h>
#include <cmath>

using namespace std;

//완전 탐색에 기초해서 주어진 숫자들을 이용해서 모든 경우의 수를 만든다
//만들어진 수들이 소수인지 검사하여 해당하는 수들을 따로 저장한다.
//소수 검사는 isPrime 함수를 이용한 에라토스테네스의 체 알고리즘을 사용한다.
//2부터 N까지 숫자들의 소수 여부를 판단하기 위해서 체라는 개념을 도입합니다.

//에라토스테네스 체 알고리즘 
//크기가 N + 1이고 모두 true로 초기화 되어있으며 이름이 isPrime인 벡터가 존재했을 때, for문 내부 변수인 i를 2부터 N까지 1씩 증가시키며 for문을 돕니다.
//만약 isPrime[i]가 true이면 i를 소수라고 판단하고 i의 모든 배수의 isPrime값을 false로 만듭니다.
//만약 isPrime[i]가 false이면 i를 소수라고 판단하지 않고 i를 1 증가시켜 다음 숫자의 소수 판별로 넘어갑니다.
//이 과정을 반복하면 2부터 N까지 소수들의 isPrime 값은 true이고 소수가 아닌 수의 isPrime 값은 false가 됩니다.

vector<int> n;//numbers를 잘라서 조합할 숫자들을 넣어둘 공간
vector<int> result;//자른 숫자들을 합쳐서 만든 새로운 숫자들을 넣을 공간
string re;

bool check(int i, string numbers) {
	re = to_string(i);
	vector<bool>visit(n.size(), false);

	for (int j = 0; j < re.size(); j++)
	{
		int idx = numbers.find(re.substr(j,1));//중복되는 숫자가 있는지 검사
		
		if (idx >= numbers.size()) {//해당 숫자가 없으면 false
			return false;
		}
		else {
			numbers = numbers.substr(0, idx) + numbers.substr(idx + 1);
		}
	}
	return true;
}

int solution(string numbers) {
	int answer = 0;
	int num_length = numbers.length();
	int max = 0;
	
	
	for (int i = 0; i < numbers.length(); i++)
	{
		n.push_back(stoi(numbers.substr(i,1)));//string을 int형으로 변환해서 저장
	}

	sort(n.begin(), n.end(),greater<int>());//넣어준 숫자들을 내림차순으로 정리
	for (int i = 0; i < n.size(); i++) {
		max = max + (n[i] * pow(10, n.size() - 1 - i));
	}

	vector<bool> prime(max+1, true);//숫자들이 소수인지 구분할 공간
	//초기값은 전부 true로 설정한다.


	for (int i = 2; i <= max; i++)
	{
		if (prime[i])
		{
			if (check(i, numbers)) {
				answer++;
			}

			for (int j = 2; j*i <= max; j ++)
			{
				prime[j*i] = false;
			}
		}
		
	}

	return answer;
}
```

이번 문제는 전체의 경우의 수를 구하고 그 중에 조건이 맞는 경우를 찾는 완전탐색을 기반으로 만들어진 문제같습니다. 주어진 조건은 조합되어 만들어진 수 중에 소수를 판별하는 것으로써 판별하는 방식은 에라토스테네스의 체 알고리즘을 활용하여 풀었습니다. 아직 미숙한 부분이 많은 만큼 관련된 문제를 좀더 풀어서 익숙해지도록 하겠습니다. 

에라토스테네스의 체 관련 알고리즘은 위의 코드에 주석으로 설명을 달았습니다.(아래는 참고 자료입니다.)

![에라토스 테네스의 체](https://user-images.githubusercontent.com/52284829/75896616-b1c94480-5e7a-11ea-813f-1d9a68ea0829.gif)

사용언어: c++

출처:https://programmers.co.kr/learn/courses/30/lessons/42839