# 스택과 큐(Stacks_and_Queues)

## 목차

## 스택(Stack)

스택은 삽입과 삭제가 top이라고 불리는 한쪽 끝에서 일어나는 순서 목록이다.\
가장 마지막에 삽입된 데이터가 가장 먼저 삭제된다고 하여 Last-In-First-Out(LIFO)라고도 한다.

### 스택의 특징

- 데이터의 삽입(Push)과 삭제(Pop)는 항상 스택의 맨 위(Top)에서만 이루어진다.

- 중간에 있는 원소에 직접 접근하거나 삽입, 삭제하지 않는다.

- 배열이나 연결 리스트를 이용하여 구현할 수 있다.

### 스택의 장점

- 구조가 단순하여 구현이 쉽다.

- Push와 Pop 연산이 모두 O(1)로 매우 빠르다.

- 함수 호출 관리나 DFS와 같이 LIFO 특성이 필요한 문제를 효율적으로 해결 할 수 있다.

### 스택의 단점

- 가장 위의 데이터만 접근할 수 있어 탐색이나 중간 삽입, 삭제가 비효율적이다.

- 배열 기반 구현은 크기가 고정되어 오버플로우가 발생할 수 있다.

- 연결 리스트 기반 구현은 포인터 저장을 위한 추가 메모리가 필요하다.

### 배열을 이용한 스택 구현

```c
const int MAX_SIZE = 100;
int top = -1;
int stack[MAX_SIZE];

void push(int value)
{
	if (top >= MAX_SIZE - 1) return;

	top++;
	stack[top] = value;
}

int pop()
{
	return stack[top--];
}
```

#### 배열을 이용한 구현의 장점

- 구현이 간단하다.

- Push와 Pop 연산이 빠르다.

#### 배열을 이용한 구현의 단점

- 배열의 크기가 고정된다.

- 스택이 가득 차면 더 이상 데이터를 저장할 수 없다.

### 연결 리스트(Linked List)를 이용한 스택 구현

일반적으로 단일 연결 리스트를 사용하며, 리스트의 Head를 Top으로 사용한다.

```c
struct SNode {
	int nData;
	SNode* pNext;
};

SNode* CreateNode(SNode* top, int data)
{
	SNode* pTemp = new SNode();
	pTemp->nData = data;
	if (top != NULL) pTemp->pNext = top;
	return pTemp;
}

SNode* ListPop(SNode* top)
{
	printf("%d\n", top->nData);
	return top->pNext;
}
```

#### 연결 리스트를 이용한 구현의 장점

- 필요한 만큼 메모리를 동적으로 사용할 수 있다.

- 스택의 크기에 제한이 없다.

#### 연결 리스트를 이용한 구현의 단점

- 노드를 위한 포인터 공간이 추가로 필요하다.

- 배열보다 구현이 다소 복잡하다.

## 큐(Queue)

큐는 삽입은 뒤(rear)에서 삭제는 앞(front)에서 일어나는 순서 목록이다.\
가장 먼저 삽입된 데이터가 가장 먼저 삭제된다고 하여 First-In-First-Out(FIFO)라고도 한다.