## 자료구조 Deque 복습

```
#include <stdio.h>
#include <stdlib.h>
#include <malloc.h>
#include <string.h>

typedef struct Dq {
	int elem;
	struct Dq *left;
	struct Dq *right;
}Dq;

int empty(Dq *front, Dq *rear)
{
	Dq *temp = front->right;
	if (temp == rear)//Deque가 비어있는 경우
		return 1;
	return 0;
}


void add_front(Dq *front, int elem)//AF
{
	Dq *newNode = (Dq*)malloc(sizeof(Dq));
	newNode->elem = elem;
	newNode->left = NULL;
	newNode->right = front->right;

	newNode->right->left = newNode;
	front->right = newNode;

}
void add_rear(Dq *rear, int elem)//AR
{
	Dq *newNode = (Dq*)malloc(sizeof(Dq));
	newNode->elem = elem;
	newNode->right = NULL;

	newNode->left = rear->left;//front 노드와 rear노드는 더미 노드 항상 시작과 끝에 위치
	newNode->left->right = newNode;
	rear->left = newNode;
}

void delete_front(Dq *front, Dq *rear, int *flag)//DF
{
	if (empty(front, rear) == 1)
	{
		printf("underflow\n");
		*flag = 1;
	}
	else {
		front->right->right->left = front;
		front->right = front->right->right;
	}
}

void delete_rear(Dq *front, Dq *rear, int *flag)//DR
{
	if (empty(front, rear) == 1)
	{
		printf("underflow\n");
		*flag = 1;
	}
	else {
		rear->left->left->right = rear;
		rear->left = rear->left->left;
	}
}

void print(Dq *t, Dq *rear)
{
	Dq *temp = t->right;
	if (temp== rear)
		return;

	while (temp != rear)
	{
		printf(" %d", temp->elem);
		if (temp->right == NULL)
			break;
		temp = temp->right;
	}
	printf("\n");

}

int main()
{
	Dq *front = (Dq*)malloc(sizeof(Dq));
	Dq *rear = (Dq*)malloc(sizeof(Dq));
	int n, x;//연산의 개수
	int flag = 0;
	char a[3];
	front->right = rear;
	front->left = NULL;

	rear->right = NULL;
	rear->left = front;
	scanf("%d", &n);
	getchar();
	for (int i = 0; i < n; i++)
	{
		scanf("%s", a);
		if (strcmp(a, "AF") == 0)
		{
			scanf("%d", &x);
			getchar();
			add_front(front, x);
		}
		else if (strcmp(a, "AR") == 0)
		{
			scanf("%d", &x);
			getchar();
			add_rear(rear, x);
		}
		else if (strcmp(a, "DF") == 0)
		{
			delete_front(front, rear, &flag);

			if (flag == 1)
				break;
		}
		else if (strcmp(a, "DR") == 0)
		{
			delete_rear(front, rear, &flag);
			if (flag == 1)
				break;
		}
		else if (strcmp(a, "P") == 0)
			print(front, rear);
	}

	free(front);
	free(rear);


	return 0;
}
```

___

사용언어:  c언어

