## 프로그래머스 level3 여행경로(DFS/BFS)

###### 문제 설명

주어진 항공권을 모두 이용하여 여행경로를 짜려고 합니다. 항상 ICN 공항에서 출발합니다.

항공권 정보가 담긴 2차원 배열 tickets가 매개변수로 주어질 때, 방문하는 공항 경로를 배열에 담아 return 하도록 solution 함수를 작성해주세요.

##### 제한사항

- 모든 공항은 알파벳 대문자 3글자로 이루어집니다.
- 주어진 공항 수는 3개 이상 10,000개 이하입니다.
- tickets의 각 행 [a, b]는 a 공항에서 b 공항으로 가는 항공권이 있다는 의미입니다.
- 주어진 항공권은 모두 사용해야 합니다.
- 만일 가능한 경로가 2개 이상일 경우 알파벳 순서가 앞서는 경로를 return 합니다.
- 모든 도시를 방문할 수 없는 경우는 주어지지 않습니다.

##### 입출력 예

| tickets                                                     | return                         |
| ----------------------------------------------------------- | ------------------------------ |
| [[ICN, JFK], [HND, IAD], [JFK, HND]]                        | [ICN, JFK, HND, IAD]           |
| [[ICN, SFO], [ICN, ATL], [SFO, ATL], [ATL, ICN], [ATL,SFO]] | [ICN, ATL, ICN, SFO, ATL, SFO] |

##### 입출력 예 설명

예제 #1

[ICN, JFK, HND, IAD] 순으로 방문할 수 있습니다.

예제 #2

[ICN, SFO, ATL, ICN, ATL, SFO] 순으로 방문할 수도 있지만 [ICN, ATL, ICN, SFO, ATL, SFO] 가 알파벳 순으로 앞섭니다.

___

```
#include <string>
#include <vector>
#include <algorithm>
#include <iostream>


using namespace std;
vector<string> answer;
int depth = 0;
void DFS(vector<vector<string>> t, string s,vector<bool> check,vector<string>temp,int n)
{
	temp.push_back(s);
	if (depth< n)
	{
		depth = n;
		answer = temp;
	}


	for (int j = 0; j < t.size(); j++)
	{
		if (s == t[j][0] && check[j]==false)//출발지가 동일한게 있을경우
		{
			check[j] = true;
			DFS(t, t[j][1], check,temp,n+1);
			check[j] = false;
		}
	}
	temp.pop_back();
}

vector<string> solution(vector<vector<string>> tickets) {
	//티켓은 출발지, 도착지로 구성됨
	vector<string> temp;
	string start = "ICN";//출발지와 
	string arrive = "";//도착지
	vector<bool>check(tickets.size(), false);//방문했는지 확인
	
	sort(tickets.begin(), tickets.end());//알파벳 순서가 앞서는 경로를 먼저 가야하므로
	
	DFS(tickets, start,check,temp,0);

	return answer;
}
```

___

문제설명:

1. 출발지는 'ICN'으로 고정되어 있기때문에 출발지를 미리 저장합니다.
2. 출발지가 같은 티켓의 경우를 위해 방문 여부를 확인하는 bool vector를 tickets만큼 false로 만들어줍니다. //방문하면 true로 바꾼후 재귀가 되면 다시 false로 바꿉니다.
3. temp라는 벡터에 출발지를 저장한 후 진행의 정도가 전체보다 작으면 출발지를 answer에 넣습니다.



이번 문제는 간단하게 생각을 했다가 출발 경로가 같은 경우에서 진행되어야 하는 것 이상으로 진행이되어서  temp라는 곳에 기록을 남겨서 하는 방식으로 진행을 했습니다. 

사용언어: c++

출처:https://programmers.co.kr/learn/courses/30/lessons/43164#