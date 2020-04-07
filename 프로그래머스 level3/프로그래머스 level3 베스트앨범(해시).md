## 프로그래머스 level3 베스트앨범(해시)

###### 문제 설명

스트리밍 사이트에서 장르 별로 가장 많이 재생된 노래를 두 개씩 모아 베스트 앨범을 출시하려 합니다. 노래는 고유 번호로 구분하며, 노래를 수록하는 기준은 다음과 같습니다.

1. 속한 노래가 많이 재생된 장르를 먼저 수록합니다.
2. 장르 내에서 많이 재생된 노래를 먼저 수록합니다.
3. 장르 내에서 재생 횟수가 같은 노래 중에서는 고유 번호가 낮은 노래를 먼저 수록합니다.

노래의 장르를 나타내는 문자열 배열 genres와 노래별 재생 횟수를 나타내는 정수 배열 plays가 주어질 때, 베스트 앨범에 들어갈 노래의 고유 번호를 순서대로 return 하도록 solution 함수를 완성하세요.

##### 제한사항

- genres[i]는 고유번호가 i인 노래의 장르입니다.
- plays[i]는 고유번호가 i인 노래가 재생된 횟수입니다.
- genres와 plays의 길이는 같으며, 이는 1 이상 10,000 이하입니다.
- 장르 종류는 100개 미만입니다.
- 장르에 속한 곡이 하나라면, 하나의 곡만 선택합니다.
- 모든 장르는 재생된 횟수가 다릅니다.

##### 입출력 예

| genres                                | plays                      | return       |
| ------------------------------------- | -------------------------- | ------------ |
| [classic, pop, classic, classic, pop] | [500, 600, 150, 800, 2500] | [4, 1, 3, 0] |

##### 입출력 예 설명

classic 장르는 1,450회 재생되었으며, classic 노래는 다음과 같습니다.

- 고유 번호 3: 800회 재생
- 고유 번호 0: 500회 재생
- 고유 번호 2: 150회 재생

pop 장르는 3,100회 재생되었으며, pop 노래는 다음과 같습니다.

- 고유 번호 4: 2,500회 재생
- 고유 번호 1: 600회 재생

따라서 pop 장르의 [4, 1]번 노래를 먼저, classic 장르의 [3, 0]번 노래를 그다음에 수록합니다.

___

```
#include <string>
#include <vector>
#include <map>
#include <algorithm>
#include <queue>
#include <iostream>
using namespace std;

vector<int> solution(vector<string> genres, vector<int> plays) {
	vector<int> answer;
	vector<string>g(genres);//장르 벡터를 복사
	multimap<int, string,greater<int>> album;//multi map은 key값이 중복이 가능함
	multimap<int, string>::iterator iter;
	queue<int>q;
	vector<pair<int, int>>t;//해당 횟수와 고유번호 저장
	for (int i = 0; i < g.size(); i++)
	{
		int sum = 0;
		int check = false;
		string temp = genres[i];
		for (int j = 0; j <g.size(); j++)
		{
			if (temp == g[j])
			{
				sum += plays[j];
				g[j] = j;//앞으로 안겹치게
				check = true;
			}
		}
		if (check == true) {
			album.insert(make_pair(sum, temp));//장르별 총 합계를 넣음
		}
	}

	for ( iter = album.begin(); iter != album.end(); iter++)
	{
		int count = 0;
		for (int j = 0; j < genres.size(); j++)
		{
			if (iter->second == genres[j])
			{
				t.push_back(pair<int, int>(plays[j], j));
			}
		}
		sort(t.begin(), t.end());//재생횟수로 정렬
		reverse(t.begin(), t.end());
		for (int i = 0; i < 2; i++)
			q.push(t[i].second);//고유번호만 입력
		t.clear();
	}
	
	while (!q.empty())
	{
		int result = q.front();
		q.pop();
		answer.push_back(result);
	}

	return answer;
}
```



___

문제설명:

1. multimap을 이용해 장르와 장르별 재생횟수 총 합을 저장합니다.
2. multimap은 내림차순으로 정의를 하여 조건에나온데로 횟수 많이 재생한 장르부터 대입을하므로 첫번째 인자와 같은 장르를 가진 플레이 횟수와 고유번호를 t라는 벡터에 넣어줍니다. 
3. 위를 multimap에 들어간 인자만큼 진행한후 t를 정렬한후 다시 역순으로 하여 각 장르별로 재생회수에따른 고유번호를 큐에 넣어서 answer에 순서대로 넣어주면 완료가됩니다.



사용언어:c++

출처:https://programmers.co.kr/learn/courses/30/lessons/42579#qna