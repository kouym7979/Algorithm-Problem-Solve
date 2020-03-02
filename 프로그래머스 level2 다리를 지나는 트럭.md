## 프로그래머스 level2 다리를 지나는 트럭

문제설명 : 

트럭 여러 대가 강을 가로지르는 일 차선 다리를 정해진 순으로 건너려 합니다. 모든 트럭이 다리를 건너려면 최소 몇 초가 걸리는지 알아내야 합니다. 트럭은 1초에 1만큼 움직이며, 다리 길이는 bridge_length이고 다리는 무게 weight까지 견딥니다.
※ 트럭이 다리에 완전히 오르지 않은 경우, 이 트럭의 무게는 고려하지 않습니다.

예를 들어, 길이가 2이고 10kg 무게를 견디는 다리가 있습니다. 무게가 [7, 4, 5, 6]kg인 트럭이 순서대로 최단 시간 안에 다리를 건너려면 다음과 같이 건너야 합니다.

| 경과 시간 | 다리를 지난 트럭 | 다리를 건너는 트럭 | 대기 트럭 |
| --------- | ---------------- | ------------------ | --------- |
| 0         | []               | []                 | [7,4,5,6] |
| 1~2       | []               | [7]                | [4,5,6]   |
| 3         | [7]              | [4]                | [5,6]     |
| 4         | [7]              | [4,5]              | [6]       |
| 5         | [7,4]            | [5]                | [6]       |
| 6~7       | [7,4,5]          | [6]                | []        |
| 8         | [7,4,5,6]        | []                 | []        |

따라서, 모든 트럭이 다리를 지나려면 최소 8초가 걸립니다.

solution 함수의 매개변수로 다리 길이 bridge_length, 다리가 견딜 수 있는 무게 weight, 트럭별 무게 truck_weights가 주어집니다. 이때 모든 트럭이 다리를 건너려면 최소 몇 초가 걸리는지 return 하도록 solution 함수를 완성하세요.

다음은 문제 코드입니다.

___

처음은 큐를 이용해서 풀어보았습니다.

```
#include <string>
#include <vector>
#include <queue>
using namespace std;

int solution(int bridge_length, int weight, vector<int> truck_weights) {
	int answer = 0;//총 경과시간
	queue<int> truck;//현재 지나가고있는 트럭
	int sum_weight=0;//현재 다리에 있는 트럭들의 무게 합
	int current_weight = 0;//첫번째 트럭은 넣고 시작하므로
	int count=0;
	//truck.push_back(truck_weights.at(0));
	for (int x = 0; x < truck_weights.size(); x++) {
		current_weight = truck_weights[x];
		while (1)
		{
			if (truck.empty())
			{
				truck.push(current_weight);
				sum_weight += current_weight;
				answer++;
				break;
			}
			else if (truck.size() == bridge_length)
			{
				sum_weight -= truck.front();
				truck.pop();//첫번째 원소 제거
			}
			else {
				if (sum_weight + current_weight > weight)//수용무게보다 크면 
				{
					truck.push(0);
					answer++;
				}
				else//수용무게보다 작으면
				{
					
					truck.push(current_weight);//다음 트럭을 진행시킨다.
					sum_weight += current_weight;//현재 다리를 지나는 트럭의 무게를 더해줌
					answer++;
					break;
				}
			}
		}
	}


	return answer+bridge_length;
}
```

다음은 벡터를 이용해서 풀어보았습니다.

```
#include <string>
#include <vector>

using namespace std;

int solution(int bridge_length, int weight, vector<int> truck_weights) {
	int answer = 0;//총 경과시간
	vector<int> truck;//현재 다리를 지나고있는 트럭들
	vector<int> v;//결과
	int sum_weight=0;//현재 다리에 있는 트럭들의 무게 합
	int current_weight = 0;//첫번째 트럭은 넣고 시작하므로
	int count=0;
	//truck.push_back(truck_weights.at(0));
	for (int x = 0; x < truck_weights.size(); x++) {
		current_weight = truck_weights[x];
		while (1)
		{
			if (truck.empty())
			{
				sum_weight += current_weight;
				answer++;
				truck.push_back(current_weight);
				break;
			}
			else if (truck.size() == bridge_length)
			{
				sum_weight -= truck.front();
				//v.push_back(truck_weights.at(count));//지나간 차량을 배열에 저장
				truck.erase(truck.begin());//첫번째 원소 제거
				//count++;
			}
			else {
				if (sum_weight + current_weight < weight)//수용무게보다 작고 
				{
					truck.push_back(current_weight);//다음 트럭을 진행시킨다.
					sum_weight += current_weight;//현재 다리를 지나는 트럭의 무게를 더해줌
					answer++;
					break;
				}
				else//수용무게보다 크면
				{
					truck.push_back(0);
					answer++;
				}
			}
			//if (v.size() == truck_weights.size())//이미 지나간 트럭들이 주어진 트럭들과 같으면 종료
				//break;
		}
		
	}


	return answer+bridge_length;
}
```

큐를 이용해서 한번 풀어 보았습니다. 이 문제에서는 현재 다리를 지나고 있는 트럭들의 무게에 대한 체크를 잘 해주는것이 중요하게 생각합니다. 지나갈때 제한 무게를 넘어가면 0을 넣어줘서 진행상황을 알 수 있게 나타내는것이 포인트라고 생각합니다. 