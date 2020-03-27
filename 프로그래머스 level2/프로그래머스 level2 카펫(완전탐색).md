## 프로그래머스 level2 카펫(완전탐색)

문제설명: Leo는 카펫을 사러 갔다가 아래 그림과 같이 중앙에는 빨간색으로 칠해져 있고 테두리 1줄은 갈색으로 칠해져 있는 격자 모양 카펫을 봤습니다.

![image.png](https://grepp-programmers.s3.amazonaws.com/files/ybm/7c94563a35/2ff27ac9-97d0-43a9-9cf8-a344b8e7912e.png)

Leo는 집으로 돌아와서 아까 본 카펫의 빨간색과 갈색으로 색칠된 격자의 개수는 기억했지만, 전체 카펫의 크기는 기억하지 못했습니다.

Leo가 본 카펫에서 갈색 격자의 수 brown, 빨간색 격자의 수 red가 매개변수로 주어질 때 카펫의 가로, 세로 크기를 순서대로 배열에 담아 return 하도록 solution 함수를 작성해주세요.

##### 제한사항

- 갈색 격자의 수 brown은 8 이상 5,000 이하인 자연수입니다.
- 빨간색 격자의 수 red는 1 이상 2,000,000 이하인 자연수입니다.
- 카펫의 가로 길이는 세로 길이와 같거나, 세로 길이보다 깁니다.

##### 입출력 예

| brown | red  | return |
| ----- | ---- | ------ |
| 10    | 2    | [4, 3] |
| 8     | 1    | [3, 3] |
| 24    | 24   | [8, 6] |

___

```
#include <string>
#include <vector>
#include <algorithm>
#include <cmath>
using namespace std;
//red와 brown으로 카펫 색깔 및 개수 정리 
//가로는 세로보다 같거나 크다
vector<int> solution(int brown, int red) {
	vector<int> answer;//가로길이와 세로길이
	int w, h;//가로 세로 
	int total = brown + red;//brown과 red의 카펫의 합은 총 카펫의 넓이가 된다.


	for (int i = 3; i <total; i++)//i는 높이 값 
	{
		if (total%i == 0)//가로 길이
		{
			w = total / i;//가로길이 
			h = i;//세로길이
			if ((w - 2)*(h - 2) == red)//가로길이-2 * 세로길이-2한 값이 red값과 같으면 총 가로길이와 세로길이
			{
				answer.push_back(w);//가로와 세로 길이 넣어준다.
				answer.push_back(h);
				break;
			}
		}
	}


	return answer;
}
```

이번문제는 비교적 간단하게 해결한 문제입니다. 

해결전략:

1. brown+red카펫의 합이 사각형의 넓이가 되므로 이를 전체 total값으로 설정한다.
2. total를 높이(i)를 늘려주며 나누어 떨어지는지 판단한다.
3. red카펫을 brown카펫이 둘러싸고 있는 형태이므로 가로길이 -2 ,세로길이-2의 곱이 red카펫과 같을때의 값이 가로길이와 세로길이가 된다.



사용언어: c++

출처: https://programmers.co.kr/learn/courses/30/lessons/42842

