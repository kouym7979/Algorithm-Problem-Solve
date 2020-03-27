## 프로그래머스 level2 큰 수 만들기(탐욕법)

문제설명:

어떤 숫자에서 k개의 수를 제거했을 때 얻을 수 있는 가장 큰 숫자를 구하려 합니다.

예를 들어, 숫자 1924에서 수 두 개를 제거하면 [19, 12, 14, 92, 94, 24] 를 만들 수 있습니다. 이 중 가장 큰 숫자는 94 입니다.

문자열 형식으로 숫자 number와 제거할 수의 개수 k가 solution 함수의 매개변수로 주어집니다. number에서 k 개의 수를 제거했을 때 만들 수 있는 수 중 가장 큰 숫자를 문자열 형태로 return 하도록 solution 함수를 완성하세요.

##### 제한 조건

- number는 1자리 이상, 1,000,000자리 이하인 숫자입니다.
- k는 1 이상 `number의 자릿수` 미만인 자연수입니다.

##### 입출력 예

| number     | k    | return |
| ---------- | ---- | ------ |
| 1924       | 2    | 94     |
| 1231234    | 3    | 3234   |
| 4177252841 | 4    | 775841 |

___

다음은 제가 처음에 풀었던 코드입니다.

```
#include <string>
#include <vector>

using namespace std;
string solution(string number, int k) {
	string answer = "";
	vector<pair<string, int>>q;//문자열로 만든 숫자를 잘라서입력(단, 기존의 위치값도 입력)
	int count = 0;
	priority_queue<int, vector<int>, less<int>>q2;//만들어진 숫자들 조합을 저장
	//substr(pos,len) -> pos 추출할 문자열의 시작위치, len 그 위치로 부터 문자 몇개까지 추출할지
	for (int i = 0; i < number.length(); i++)
	{
		q.push_back(pair<string, int>(number.substr(i, 1), i));//자른 문자열과 문자열의 위치를 입력
	}

	for (int i = 0; i < number.length(); i++)
	{
		count = 1;
		string temp = "";//합친 문자열을 보관할 변수
		temp = q[i].first;
		for (int j = i + 1; j < number.length(); j++)
		{
			temp += q[j].first;
			count++;
			if (temp.length() == number.length() - k)
			{
				q2.push(stoi(temp));//만들어진 숫자를 우선순위 큐에 int형으로 대입
				temp.erase(number.length() - k - 1);//직전 1개를 없애준다.
			}
		}
	}

	answer = to_string(q2.top());

	return answer;
}
```

위의 코드는 비효율적으로 작성된 코드이고 경우에 따라 안되는 경우도 있어서 

다른 방식으로 풀어보았습니다.

```
#include <string>
#include <vector>
#include <queue>

using namespace std;
string solution(string number, int k) {
	string answer = "";
	
	//substr(pos,len) -> pos 추출할 문자열의 시작위치, len 그 위치로 부터 문자 몇개까지 추출할지
	
	int size = number.size();
	
	for (int i = 0; i < size-k; i++)
	{
		string max = "0";
		int position = 0;
		for (int j = 0; j < number.size() -size+k+i+1; j++)
		{
			if (max < number.substr(j, 1))//잘라낸 다음 숫자보다 작을경우 교체
			{
				max = number.substr(j, 1);
				position = j;
				if (max == "9")
					break;
			}
		}
		answer += max;//최대값을 기입해준다.
		number = number.substr(position + 1);//사용한 숫자 이후부터 다시 사용 
	}


	return answer;
}
```

 이번 문제에서는 주어진 문자열을 1의 길이씩 잘라서 그 숫자를 비교해서 큰 값을 string 형태로 계속 answer값에 붙여주면서 큰수를 만들어 나갔습니다. 하지만 주어진 길이가 999999...99처럼 주어진 경우에는 비교할 우위를 비교할 수가 없어서 런타임에러가 발생했었습니다. 처음에는 왜 이 테스트 케이스만 통과되지않아서 답답했었는데 직접 해보니  break를 걸어줄 조건이 없어서 무한루프에 빠진것이라 판단이되어 max값이 9가 되면 break하는 조건을 걸어주었더니 잘 해결이 되었습니다. 

알고리즘을 잘 짜는것도 중요하지만 한가지의 경우만 고려하지말고 여러가지를 고려해서 생각하는 습관을 들여야겠습니다.



사용언어: c++

출처: https://programmers.co.kr/learn/courses/30/lessons/42883