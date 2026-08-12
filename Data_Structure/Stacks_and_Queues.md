# 스택과 큐(Stacks_and_Queues)

## 목차

- [스택(Stack)](#스택stack)
  - [스택의 특징](#스택의-특징)
  - [스택의 장점](#스택의-장점)
  - [스택의 단점](#스택의-단점)
  - [배열을 이용한 스택 구현](#배열을-이용한-스택-구현)
    - [배열을 이용한 구현의 장점](#배열을-이용한-구현의-장점)
    - [배열을 이용한 구현의 단점](#배열을-이용한-구현의-단점)
  - [연결 리스트(Linked List)를 이용한 스택 구현](#연결-리스트linked-list를-이용한-스택-구현)
    - [연결 리스트를 이용한 구현의 장점](#연결-리스트를-이용한-구현의-장점)
    - [연결 리스트를 이용한 구현의 단점](#연결-리스트를-이용한-구현의-단점)
- [큐(Queue)](#큐queue)
  - [큐의 특징](#큐의-특징)
  - [큐의 장점](#큐의-장점)
  - [큐의 단점](#큐의-단점)
  - [배열을 이용한 큐 구현](#배열을-이용한-큐-구현)
    - [배열을 이용한 구현의 장점](#배열을-이용한-구현의-장점)
    - [배열을 이용한 구현의 단점](#배열을-이용한-구현의-단점)
  - [연결 리스트를 이용한 큐 구현](#연결-리스트를-이용한-큐-구현)
    - [연결 리스트를 이용한 구현의 장점](#연결-리스트를-이용한-구현의-장점)
    - [연결 리스트를 이용한 구현의 단점](#연결-리스트를-이용한-구현의-단점)
- [중위 표기법(Infix)과 후위 표기법(Postfix)](#중위-표기법infix과-후위-표기법postfix)
  - [실습 - 스택을 이용하여 중위 표기법을 후위 표기법으로 변환](#실습---스택을-이용하여-중위-표기법을-후위-표기법으로-변환)

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

```c++
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

### 큐의 특징

- 데이터의 삽입(Enqueue)은 항상 큐의 뒤쪽(rear)에서 이루어진다.

- 데이터의 삭제(Dequeue)은 항상 큐의 앞쪽(front)에서 이루어진다.

- 먼저 저장된 데이터가 먼저 처리된다.

- 배열이나 연결 리스트를 이용하여 구현할 수 있다.

### 큐의 장점

- 입력된 순서대로 데이터를 처리할 수 있다.

- 삽입과 삭제 연산을 모두 O(1)에 수행할 수 있다.

- 순차적인 작업 처리에 적합하다.

### 큐의 단점

- 중간 원소에 직접 접근하거나 삽입, 삭제하기 어렵다.

- 배열 기반 구현에서는 원형 큐를 사용하지 않으면 공간을 비효율적으로 사용할 수 있다.

- 연결 리스트 기반 구현은 포인터를 저장하기 위한 추가 메모리가 필요하다.

### 배열을 이용한 큐 구현

```c
const int MAX_SIZE = 100;
int rear = -1;
int front = -1;
int queue[MAX_SIZE];

void EnQueue(int value)
{
	if (front == MAX_SIZE - 1) return;

	queue[++front] = value;
}

int DeQueue()
{
	if (front == rear) return -1;
	return queue[++rear];
}
```

#### 배열을 이용한 구현의 장점

- 구현이 간단하다.

- 메모리가 연속적으로 배치되어 접근 속도가 빠르다.

#### 배열을 이용한 구현의 단점

- 단순 배열로 구현하면 앞쪽 공간이 비어도 재사용하지 못하는 문제가 발생한다.

### 연결 리스트를 이용한 큐 구현

```c++
struct SNode {
	int nData;
	SNode* pNext;
};

SNode* CreateNode(SNode* pNode, int data)
{
	SNode* pTemp = NULL;

	pTemp = new SNode();
	pTemp->nData = data;
	pTemp->pNext = NULL;
	if (pNode != NULL) pNode->pNext = pTemp;

	return  pTemp;
}

SNode* pRear = NULL;
SNode* pFront = NULL;

pFront = CreateNode(pFront, 10);
pRear = pFront;

pFront = CreateNode(pFront, 20);
pFront = CreateNode(pFront, 30);
pFront = CreateNode(pFront, 40);
pFront = CreateNode(pFront, 50);

while (pRear != pFront)
{
    printf("%d\n", pRear->nData);
    SNode* pDel = pRear;
    pRear = pRear->pNext;
    delete pDel;
}
printf("%d\n", pRear->nData);
delete pRear;
```

#### 연결 리스트를 이용한 구현의 장점

- 큐의 크기를 동적으로 늘릴 수 있다.

- 삽입과 삭제를 모두 O(1)에 수행할 수 있다.

#### 연결 리스트를 이용한 구현의 단점

- 노드를 위한 포인터 공간이 추가로 필요하다.

- 배열보다 구현이 다소 복잡하다.

## 중위 표기법(Infix)과 후위 표기법(Postfix)

중위 표기법과 후위 표기법은 수식에서 연산자와 피연산자를 배치하는 방식들 중 하나이다.

우리가 일반적으로 사용하는 수식 표기 방식은 중위 표기법(Infix)이다.\
예) A + B, (A + B) * C

후위 표기법(Postfix)은 연산자가 피연산자의 뒤에 위치하는 표기법이다.\
예) A B +, A B + C *

Postfix는 연산자의 우선순위와 괄호를 별도로 고려하지 않아도 된다.\
즉 수식 자체에 연산 순서가 표현되어 있기 때문에 컴퓨터가 수식의 연산 순서를 처리하는 데 유리하다.

Infix -> Postfix 변환과 Postfix 수식 계산은 스택을 사용해 쉽게 구현할 수 있다.

### 실습 - 스택을 이용하여 중위 표기법을 후위 표기법으로 변환

```c
int precedence(char op) {
    if (op == '+' || op == '-')
        return 1;
    if (op == '*' || op == '/' || op == '%')
        return 2;
    return 0;
}

int isOperator(char ch) {
    return ch == '+' || ch == '-' || ch == '*' || ch == '/' || ch == '%';
}

void infixToPostfix(char* infix, char* postfix) {
    int i, j, top = -1;
    char stack[MAX_SIZE], ch;

    for (i = 0, j = 0; infix[i] != '\0'; i++) {
        ch = infix[i];

        if (isalnum(ch)) {
            postfix[j++] = ch;
        }
        else if (ch == '(') {
            stack[++top] = ch;
        }
        else if (ch == ')') {
            while (top != -1 && stack[top] != '(') {
                postfix[j++] = stack[top--];
            }
            top--; // remove the '(' from the stack
        }
        else if (isOperator(ch)) {
            while (top != -1 && precedence(ch) <= precedence(stack[top])) {
                postfix[j++] = stack[top--];
            }
            stack[++top] = ch;
        }
        else if (ch == ' ')
        {

        }
        else {
            printf("Error: Invalid character '%c'\n", ch);
            exit(1);
        }
    }

    while (top != -1) {
        if (stack[top] == '(') {
            printf("Error: Unmatched parentheses\n");
            exit(1);
        }
        postfix[j++] = stack[top--];
    }

    postfix[j] = '\0';
}
```
