## 프로그래머스 level3 종이접기(Summer/Winter Coding)

###### 문제 설명

직사각형 종이를 n번 접으려고 합니다. 이때, 항상 오른쪽 절반을 왼쪽으로 접어 나갑니다. 다음은 n = 2인 경우의 예시입니다.

![image](https://res.cloudinary.com/dpxurmkij/image/upload/c_scale,w_390/v1500952547/%EC%A2%85%EC%9D%B4%EC%A0%91%EA%B8%B01_swcvrz.png)

먼저 오른쪽 절반을 왼쪽으로 접습니다.

![image](https://res.cloudinary.com/dpxurmkij/image/upload/c_scale,w_195/v1500952547/%EC%A2%85%EC%9D%B4%EC%A0%91%EA%B8%B02_e49oe3.png)

다시 오른쪽 절반을 왼쪽으로 접습니다.

![image](https://res.cloudinary.com/dpxurmkij/image/upload/c_scale,w_95/v1500952178/%EC%A2%85%EC%9D%B4%EC%A0%91%EA%B8%B03_nqdurc.png)

종이를 모두 접은 후에는 종이를 전부 펼칩니다. 종이를 펼칠 때는 종이를 접은 방법의 역순으로 펼쳐서 처음 놓여있던 때와 같은 상태가 되도록 합니다. 위와 같이 두 번 접은 후 종이를 펼치면 아래 그림과 같이 종이에 접은 흔적이 생기게 됩니다.

![image](https://res.cloudinary.com/dpxurmkij/image/upload/c_scale,w_390/v1500952178/%EC%A2%85%EC%9D%B4%EC%A0%91%EA%B8%B04_qxfoxr.png)

위 그림에서 ∨ 모양이 생긴 부분은 점선(0)으로, ∧ 모양이 생긴 부분은 실선(1)으로 표시했습니다.

종이를 접은 횟수 n이 매개변수로 주어질 때, 종이를 절반씩 n번 접은 후 모두 펼쳤을 때 생기는 접힌 부분의 모양을 배열에 담아 return 하도록 solution 함수를 완성해주세요.

##### 제한사항

- 종이를 접는 횟수 n은 1 이상 20 이하의 자연수입니다.
- 종이를 접었다 편 후 생긴 굴곡이 ∨ 모양이면 0, ∧ 모양이면 1로 나타냅니다.
- 가장 왼쪽의 굴곡 모양부터 순서대로 배열에 담아 return 해주세요.

------

##### 입출력 예

| n    | result          |
| ---- | --------------- |
| 1    | [0]             |
| 2    | [0,0,1]         |
| 3    | [0,0,1,0,0,1,1] |

##### 입출력 예 설명

입출력 예 #1
종이의 오른쪽 절반을 왼쪽으로 한번 접었다 펴면 아래 그림과 같이 굴곡이 생깁니다.

![image](https://res.cloudinary.com/dpxurmkij/image/upload/c_scale,w_390/v1500952178/%EC%A2%85%EC%9D%B4%EC%A0%91%EA%B8%B05_fpgzni.png)

따라서 [0]을 return 하면 됩니다.

입출력 예 #2
문제의 예시와 같습니다.

입출력 예 #3
종이를 절반씩 세 번 접은 후 다시 펼치면 아래 그림과 같이 굴곡이 생깁니다.

![image](https://res.cloudinary.com/dpxurmkij/image/upload/c_scale,w_390/v1500952178/%EC%A2%85%EC%9D%B4%EC%A0%91%EA%B8%B06_sbn7li.png)

따라서 [0,0,1,0,0,1,1]을 return 하면 됩니다.

___

```
#include <string>
#include <vector>
#include <algorithm>


using namespace std;

//종이를 접었을때 나타나는 흔적을 0 또는 1로 리턴 
//2번 이상부터는 2^n-1번의 흔적이 나타남
//시작은 무조건 0 끝은 무조건 1 로 끝난다.-> 접었을때 대칭을 이루므로


vector<int> solution(int n) {

	vector<int> answer;
	vector<int>temp;
	int k = 0;
	int size = 0;
	for (int i = 0; i < n; i++)
	{
		if (i == 0)
		{
			answer.push_back(0);//1번접을경우 0
		}
		else {
			temp.clear();
			size = answer.size();//본래의 크기를 매번 갱신한다. 
			for (int j = 0; j < size; j++)
			{
				temp.push_back(j % 2);//0 인자리 앞에 0을 추가
				temp.push_back(answer[j]);// 기존값 추가
				if (j == size - 1 || size == 1)//마지막은 항상 1로 끝난다
				{
					temp.push_back(1);
				}

			}
			answer = temp;
		}
	}



	return answer;
}
```

___

이제 level3를 시작했는데 확실히 level2보다는 접근하는것이 어려웠습니다. 

직접 종이를 접어가면서 어떻게 나오는지 생각을 해보면서 풀어보았는데요..

하나의 규칙을 찾게되면 쉽게 풀 수 있던 문제인 것 같습니다. 다름아닌 접힌 굴곡 V 즉 0이 나온 부분 앞뒤로 0과 1 이 추가적으로 나타나는 규칙입니다.

그리고 총 접힌 개수는 2의 n승 -1번 나타나므로 이를 2중포문을 이용하여 표현했습니다.

접어가는 진행상황에 맞게 추가하기 위해 temp라는 임시 배열은 매번 clear해줌으로써 엉키는 경우가 없게하는 것이 중요한 것 같습니다.





사용언어: c++

출처: https://programmers.co.kr/learn/courses/30/lessons/62049