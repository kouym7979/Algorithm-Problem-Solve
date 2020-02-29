## 프로그래머스 level2 탑

문제설명입니다.

수평 직선에 탑 N대를 세웠습니다. 모든 탑의 꼭대기에는 신호를 송/수신하는 장치를 설치했습니다. 발사한 신호는 신호를 보낸 탑보다 높은 탑에서만 수신합니다. 또한, 한 번 수신된 신호는 다른 탑으로 송신되지 않습니다.

예를 들어 높이가 6, 9, 5, 7, 4인 다섯 탑이 왼쪽으로 동시에 레이저 신호를 발사합니다. 그러면, 탑은 다음과 같이 신호를 주고받습니다. 높이가 4인 다섯 번째 탑에서 발사한 신호는 높이가 7인 네 번째 탑이 수신하고, 높이가 7인 네 번째 탑의 신호는 높이가 9인 두 번째 탑이, 높이가 5인 세 번째 탑의 신호도 높이가 9인 두 번째 탑이 수신합니다. 높이가 9인 두 번째 탑과 높이가 6인 첫 번째 탑이 보낸 레이저 신호는 어떤 탑에서도 수신할 수 없습니다.



다음은 코드입니다.

___

```
#include <algorithm>
#include <cmath>
#include <iostream>
#include <vector>
#include <string>

using namespace std;

vector<int> solution(vector<int> heights) {
	vector<int> answer;//송신한 위치
	vector<pair<int, int>> location;
	vector<int> v(heights);//heights를 복사

	int tower = heights.size();
	
	for (int i = 0; i < heights.size(); i++)
	{
		location.push_back(pair<int,int>(i + 1,heights[i]));//위치와 높이를 넣어줌
	}

	answer.push_back(0);
	for (int i = 0; i < v.size(); i++)
	{
		for (int j=i-1;j>=0;j--)
		{
			if (v[i] < location[j].second)//높이 값
			{
				answer.push_back(location[j].first);//수신받은 탑의 위치를 넣어줌
				break;
			}
			else if(j==0)//더이상 비교 대상이 없을경우
			{
				answer.push_back(0);
			}
		}
	}
	
	return answer;
}
```

문제를 풀때 위치와 높이를 모두 고려하려해서 vector의 pair 특성을 이용해서 접근했습니다.

막상 문제를 풀고 보니 굳이 pair를 사용하지 않고 더 간단히 풀 수 있을 것 같다는 생각이 드네요... 다음에는 문제를 풀기전에 기본적인 구조를 좀더 생각해보고 알고리즘을 풀어나가도록 해야겠다는 생각이 듭니다.