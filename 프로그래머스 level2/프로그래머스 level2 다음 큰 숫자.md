## 프로그래머스 level2 다음 큰 숫자

###### 문제 설명

자연수 n이 주어졌을 때, n의 다음 큰 숫자는 다음과 같이 정의 합니다.

- 조건 1. n의 다음 큰 숫자는 n보다 큰 자연수 입니다.
- 조건 2. n의 다음 큰 숫자와 n은 2진수로 변환했을 때 1의 갯수가 같습니다.
- 조건 3. n의 다음 큰 숫자는 조건 1, 2를 만족하는 수 중 가장 작은 수 입니다.

예를 들어서 78(1001110)의 다음 큰 숫자는 83(1010011)입니다.

자연수 n이 매개변수로 주어질 때, n의 다음 큰 숫자를 return 하는 solution 함수를 완성해주세요.

##### 제한 사항

- n은 1,000,000 이하의 자연수 입니다.

------

##### 입출력 예

| n    | result |
| ---- | ------ |
| 78   | 83     |
| 15   | 23     |

##### 입출력 예 설명

입출력 예#1
문제 예시와 같습니다.
입출력 예#2
15(1111)의 다음 큰 숫자는 23(10111)입니다.

___

```
#include <string>
#include <vector>
#include <iostream>
#include <algorithm>

using namespace std;

int countN(int num) {//1의 개수만 파악하는 함수
	int c = 0;
	
	while (num > 1)
	{
		int t = 0;
		t = num % 2;//나머지를 
		if (t == 1)
			c++;//1의 개수 증가
		if (num / 2 == 1)//마지막일때 1추가
		{
			c++;
		}
		num = num / 2;
	}
	return c;
}


int solution(int n) {
	int answer = 0;
	int count = 0;//1의개수
	int n_count = 0;//다음 큰 숫자의 1의 수
	int temp_length;
	string temp = "";//주어진 수를 이진법으로 저장할 문자열

	int sub = n;//n을 저장

	while (n > 1)
	{
		int t=0;
		t= n % 2;//나머지를 
		if (t == 1)
			count++;//1의 개수 증가
		temp += to_string(t);//나머지를 문자열로 변환

		if (n / 2 == 1)//마지막일때 1추가
		{
			temp += '1';
			count++;
		}
		n = n / 2;
	}

	reverse(temp.begin(), temp.end());//이진법으로 올바르게 변환
	cout << temp<<endl;
	
	
	if (temp.length() == count)//만약 2진법이 전부 1로 이루어져 있다면
	{
		string n_temp = "10";
		int e = 1;
		
		for (int i = 0; i < count-1; i++)
		{
			n_temp += '1';//
		}
		
		for (int x = n_temp.length() - 1; x >= 0; x--)//2진법을 10진법으로
		{
			for (int y = 0; y < n_temp.length() - x - 1; y++)
			{
				e *= 2;//각 이진법의 자리수계산
			}
			if (n_temp[x] == '1')
				answer += e;
			e = 1;
		}
	}
	else{//2진법의 길이보다 1의 수가 적을경우 
		int n_find = sub + 1;//찾아야할 수 최소 n보다 1은 더 커야하므로
		for (int i = n_find; i <= 1000000; i++)
		{
			if (count == countN(i)) {
				answer = i;//1의 개수가 같은 주어진 수보다 바로 다음 큰 수
				break;
			}
		}
	}
	
	return answer;
}

```

이렇게 풀었을때 효율성테스트에서 실패가 나왔습니다...

자세히 보니 코드에서 1의 개수하고 문자열의 길이가 같을 경우를 굳이 생각하지 않아도 된다는 것을 알고 다시 해보았습니다.

```
#include <string>
#include <vector>
#include <iostream>
#include <algorithm>

using namespace std;

int countN(int num) {//1의 개수만 파악하는 함수
	int c = 0;

	while (num > 1)
	{
		int t = 0;
		t = num % 2;//나머지를 
		if (t == 1)
			c++;//1의 개수 증가
		if (num / 2 == 1)//마지막일때 1추가
		{
			c++;
		}
		num = num / 2;
	}
	return c;
}


int solution(int n) {
	int answer = 0;
	int count = 0;//1의개수
	int n_count = 0;//다음 큰 숫자의 1의 수

	int sub = n;//n을 저장

	while (n > 1)
	{
		int t = 0;
		t = n % 2;//나머지를 
		if (t == 1)
			count++;//1의 개수 증가

		if (n / 2 == 1)//마지막일때 1추가
		{
			count++;
		}
		n = n / 2;
	}

	int n_find = sub + 1;//찾아야할 수 최소 n보다 1은 더 커야하므로
	for (int i = n_find; i <= 1000000; i++)
	{
		if (count == countN(i)) {
			answer = i;//1의 개수가 같은 주어진 수보다 바로 다음 큰 수
			break;
		}
	}


	return answer;
}
```

위처럼 2진법으로 변환하는 과정도 제외하고 단순히 2진법에서 1의 개수만을 확인하여 찾고자하는 수의 2진법의 1의 개수만 맞는 경우를 확인하였더니 효율성이 통과가 되었습니다...



사용언어: c++

출처: https://programmers.co.kr/learn/courses/30/lessons/12911