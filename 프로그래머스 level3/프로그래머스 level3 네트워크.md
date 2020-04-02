## 프로그래머스 level3 네트워크

###### 문제 설명

네트워크란 컴퓨터 상호 간에 정보를 교환할 수 있도록 연결된 형태를 의미합니다. 예를 들어, 컴퓨터 A와 컴퓨터 B가 직접적으로 연결되어있고, 컴퓨터 B와 컴퓨터 C가 직접적으로 연결되어 있을 때 컴퓨터 A와 컴퓨터 C도 간접적으로 연결되어 정보를 교환할 수 있습니다. 따라서 컴퓨터 A, B, C는 모두 같은 네트워크 상에 있다고 할 수 있습니다.

컴퓨터의 개수 n, 연결에 대한 정보가 담긴 2차원 배열 computers가 매개변수로 주어질 때, 네트워크의 개수를 return 하도록 solution 함수를 작성하시오.

##### 제한사항

- 컴퓨터의 개수 n은 1 이상 200 이하인 자연수입니다.
- 각 컴퓨터는 0부터 `n-1`인 정수로 표현합니다.
- i번 컴퓨터와 j번 컴퓨터가 연결되어 있으면 computers[i][j]를 1로 표현합니다.
- computer[i][i]는 항상 1입니다.

##### 입출력 예

| n    | computers                         | return |
| ---- | --------------------------------- | ------ |
| 3    | [[1, 1, 0], [1, 1, 0], [0, 0, 1]] | 2      |
| 3    | [[1, 1, 0], [1, 1, 1], [0, 1, 1]] | 1      |

##### 입출력 예 설명

예제 #1
아래와 같이 2개의 네트워크가 있습니다.
![image0.png](https://grepp-programmers.s3.amazonaws.com/files/ybm/5b61d6ca97/cc1e7816-b6d7-4649-98e0-e95ea2007fd7.png)

예제 #2
아래와 같이 1개의 네트워크가 있습니다.
![image1.png](https://grepp-programmers.s3.amazonaws.com/files/ybm/7554746da2/edb61632-59f4-4799-9154-de9ca98c9e55.png)

___

```
#include <string>
#include <vector>
#include <algorithm>
#include <iostream>

using namespace std;


bool check_com(vector<vector<int>>&computers,int x)
{
	if (!computers[x][x])
		return false;
	computers[x][x] = 0;
	for (int i = 0; i < computers.size(); i++)
	{
		if(computers[x][i]==1)
			check_com(computers, i);
	}
	return true;
}

int solution(int n, vector<vector<int>> computers) {
	int answer = 0;

	for (int i = 0; i < n; i++)
	{
		if (computers[i][i] && check_com(computers, i))
			answer++;
	}



	return answer;
}
```

___

```
#include <string>
#include <vector>
#include <algorithm>
#include <iostream>

using namespace std;

//네트워크상에서 하나가 연결되면 그 반대도 연결된 경우

bool check_com(vector<int>t,int x)
{
	vector<int>::iterator iter, iter2;
	bool chk = false;
	iter = find(t.begin(), t.end(), x);
	if (iter != t.end())//앞에서 연결된거와 연관이 있으면
	{
		chk = true;
		t.push_back(x);
	}

	return chk;
}

int solution(int n, vector<vector<int>> computers) {
	int answer = 0;
	int count = 0;//
	int overlap = 0;//두번 체크된경우
	vector<int>temp;//지나간 점들을 넣음
	vector<int>::iterator iter, iter2;
	bool check = false;
	for (int i = 0; i < computers.size(); i++)
	{
		for (int j = 0; j < computers.size(); j++)
		{
			if (computers[i][j] == 1 && i!=j)//i와 j가 같은 경우는 무조건 1이므로 
			{
				count++;
				check=check_com(temp, i);
				if (check != true)
				{

					check = check_com(temp, j);
					if (check == true)
						count--;
				}
				else count--;
				
				iter = find(temp.begin(), temp.end(), i);
				iter2 = find(temp.begin(), temp.end(), j);
				if (iter != temp.end() && iter2 != temp.end())
				{
					count++;
				}
			}
		}
		check = false;
	}
	answer = count;

	return answer;
}
```

___

문제설명: 첫번째 코드는 dfs로 직접 탐색을 하면서 검사하고 지나간 곳은 1->0으로 바꿔서 두번 검사하지 않도록 반복하며 탐색이 끝나면 answer값을 증가하는 방식으로 구현했습니다.

두번째 코드는 dfs로 직접 탐색을 하지않고 경우를 따져가면서 작성한 코드인데 완벽하지않습니다..

일부에서 제한이 걸리지만 제가 생각한 부분들을 간단히 적어보겠습니다.

   1.임시 벡터 temp에 지나간 점들을 입력합니다.

2. 연결된 점에서 이미 지나간 점들을 포함하고 있다면 트리처럼 연결된 좌표임으로 늘려준 카운트를 감소합니다. 
3. i,j와 j,i 처럼 연결된 곳을 위에서 걸러지게 되므로 독립적으로 연결된 경우를 위해 count를 증가시킵니다.



이런 문제는 dfs를 이용하여서 간결하고 효율성있게 푸는 것이 더 효율적이라고 생각되는 문제였습니다.



사용언어: c++

출처: https://programmers.co.kr/learn/courses/30/lessons/43162



