## 자료구조 큐(Queue) 공부

```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <malloc.h>


typedef struct Q {
	int front;
	int rear;
	int *data;
}Q;

int isFull(Q *q,int size)
{
	if((q->rear+1)%size==(q->front)%size)
		return 0;

	else return 1;
}
int isEmpty(Q *q)
{
	if (q->front == q->rear)
		return 0;
	else return 1;
}

void push(Q *q, int elem,int size,int *flag)
{
	if (isFull(q, size) != 0) {
		q->rear = ((q->rear) + 1) % size;
		q->data[q->rear] = elem;
		return;
	}
	else {
		printf("overflow ");
		for (int i = 0;i<size; i++)
		{
			printf("%d ", q->data[i]);
		}
		*flag = 1;
	}
}
void _delete(Q *q,int size,int *flag)
{
	if (isEmpty(q) == 0)
	{
		printf("underflow\n");
		*flag = 1;
		
	}
	else {
		q->front = ((q->front) + 1) % size;
		q->data[q->front] = 0;
		
	}
}
void print(Q *q,int size)
{
	for (int i = 0; i < size; i++)
	{
		printf(" %d", q->data[i]);
	}
	printf("\n");
	
}
int main()
{
	Q *q = NULL;
	
	char temp;
	int flag = 0;
	int size,n,x;//n은 연산의 수
	scanf("%d", &size);
	q = (Q*)malloc(sizeof(Q));
	q->front = 0;
	q->rear = 0;
	q->data = (int *)malloc(sizeof(int)*size);//q동적할당

	for (int i = 0; i < size; i++)
	{
		q->data[i] = 0;
	}

	scanf("%d", &n);
	getchar();
	for (int i = 0; i < n; i++)
	{
		scanf("%c", &temp);
		getchar();

		if (temp == 'I')
		{
			scanf("%d", &x);
			getchar();
			push(q, x, size,&flag);
			if (flag == 1)
				break;
		}
		else if (temp == 'P')
		{
			print(q,size);
		}
		else if (temp == 'D')
		{
			_delete(q,size,&flag);
			if (flag == 1)
			{
				printf("%d", flag);
				break;
			}
		}
	}

	return 0;
}
```

___

 I 10 : 원형 큐에 원소 10을 삽입 큐 원소는 양의 정수 ( ).

- D : 원형 큐에서 원소를 삭제한 후 해당 배열 원소 값을 0으로 치환. 
- - P : 배열 원소 전체를 차례로 화면에 출력 입출력 예시 참조 ( ).
  -  ※ overflow 발생 시 ( , ), 즉 포화 상태에서 삽입을 시도한 경우 overflow . 화면에 와 배열 값들을 모두 출력하고 프로그램 종료
  - ※ underflow 발생 시 ( , ), 즉 공백 상태에서 삭제를 시도한 경우 underflow . 화면에 를 출력하고 프로그램 종료

사용언어:c언어



