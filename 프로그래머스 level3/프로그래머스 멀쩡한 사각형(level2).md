## 프로그래머스 멀쩡한 사각형(level2)

오늘 풀어본 문제는 level2에서 멀쩡한 사각형의 개수를 구하는 문제입니다.

다음은 문제설명입니다.

###### 문제 설명

가로 길이가 Wcm, 세로 길이가 Hcm인 직사각형 종이가 있습니다. 종이에는 가로, 세로 방향과 평행하게 격자 형태로 선이 그어져 있으며, 모든 격자칸은 1cm x 1cm 크기입니다. 이 종이를 격자 선을 따라 1cm × 1cm의 정사각형으로 잘라 사용할 예정이었는데, 누군가가 이 종이를 대각선 꼭지점 2개를 잇는 방향으로 잘라 놓았습니다. 그러므로 현재 직사각형 종이는 크기가 같은 직각삼각형 2개로 나누어진 상태입니다. 새로운 종이를 구할 수 없는 상태이기 때문에, 이 종이에서 원래 종이의 가로, 세로 방향과 평행하게 1cm × 1cm로 잘라 사용할 수 있는 만큼만 사용하기로 하였습니다.
가로의 길이 W와 세로의 길이 H가 주어질 때, 사용할 수 있는 정사각형의 개수를 구하는 solution 함수를 완성해 주세요.(아래 그림과 같은 사각형입니다.)

##### 제한사항

- W, H : 1억 이하의 자연수

___

![그림예시2](https://user-images.githubusercontent.com/52284829/75132408-26351280-571a-11ea-87eb-8bf75433e880.png)

```
#include <algorithm>
#include <cmath>
#include <iostream>
#include <vector>

using namespace std;

long long solution(int w, int h)
{
	long long answer = 1;
	long long square = (long long)w * (long long)h;//총 정사각형의 개수
	int gcd;
	for (int i = (w<h)?w:h; i >0; i--)
	{
		if ((w%i == 0) && (h%i == 0))
		{
			gcd = i;//최대공약수를 넣어줌
			break;
		}
	}
	answer = square - gcd * ((w / gcd) + (h / gcd) - 1);
	return answer;
}
```

이 문제는 최대공약수를 이용해서 그려낼수 있는 작은 패턴들을 알아볼 수 있는지가 중요한 문제였던것 같습니다. 최대공약수에 따라 위의 그림에서 4번의 동일한 패턴이 나타남을 알 수 있습니다.

사용언어:c,c++