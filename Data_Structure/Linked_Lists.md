# 연결 리스트(Linked Lists)

## 목차

- [연결 리스트는 무엇인가?(What is Linked List)](#연결-리스트는-무엇인가what-is-linked-list)
  - [연결 리스트의 특징](#연결-리스트의-특징)
  - [노드 구조](#노드-구조)
  - [연결 리스트의 장점](#연결-리스트의-장점)
  - [연결 리스트의 단점](#연결-리스트의-단점)
- [동치 클래스(Equivalence Classes)](#동치-클래스equivalence-classes)
  - [실습 - 리스트로 동치 클래스 구현하기](#실습---리스트로-동치-클래스-구현하기)

## 연결 리스트는 무엇인가?(What is Linked List)

연결 리스트(Linked List)는 여러 개의 노드(Node)가 포인터를 통해 서로 연결되어 있는 선형 자료구조이다.\
배열과 달리 데이터가 메모리에 연속적으로 저장될 필요가 없으며, 각 노드가 다음 노드의 주소를 저장하여 논리적인 순서를 유지한다.\
노드의 구조 및 연결 구조에 따라 단일 연결 리스트, 원형 연결 리스트, 이중 연결 리스트 등이 있다.\
저번 문서에서 설명 했듯이 스택, 큐 등의 자료구조를 구현하는데 활용할 수 있다.

### 연결 리스트의 특징

- 데이터와 다음 노드의 주소를 저장하는 노드(Node)로 구성된다.

- 각 노드는 포인터를 통해 다음 노드를 가리킨다.

- 노드들이 메모리에 연속적으로 배치될 필요가 없다.

- 리스트의 첫 번째 노드를 가리키는 포인터를 일반적으로 Head라고 한다.

- 일반적으로 마지막 노드의 다음 포인터는 NULL을 가리킨다.

- 동적 메모리 할당을 이용하여 실행 중에 리스트의 크기를 변경할 수 있다.

### 노드 구조

일반적으로 연결 리스트의 노드 구조는 다음과 같다.

```c
struct Node
{
    int data;
    Node* next;
};
```

여기서 이중 연결 리스트의 경우 이전 노드를 가리키는 포인터가 추가 되어 다음과 같다.

```c
struct Node
{
    int data;
    Node* prev;
    Node* next;
};
```

### 연결 리스트의 장점

- 크기를 동적으로 변경 가능하다.

- 노드의 위치를 알고 있다면 기존 데이터를 이동시키지 않고 포인터만 변경하면 되므로 삽입과 삭제가 효율적이다.

### 연결 리스트의 단점

- 임의 접근이 불가능하고 Head부터 시작해서 하나씩 이동해야 한다. 그러므로 탐색 시간은 O(n)이다.

- 각 노드가 다음 노드의 주소를 저장해야 하므로 포인터를 위한 추가 메모리가 필요하다.

- 연결 리스트의 노드는 메모리의 여러 위치에 분산될 수 있기 때문에 배열보다 순차 접근 성능이 떨어질 수 있다.

## 동치 클래스(Equivalence Classes)

동치 클래스는 어떤 동치 관계(Equivalence Relation)을 기준으로 서로 같은 것으로 취급되는 원소들을 하나의 그룹으로 묶은 것이다.

집합 S에 정의된 관계 R이 다음 세 가지 성질을 만족하면 동치 관계라고 한다.

1. 반사성(Reflexivity)\
    모든 원소 a에 대해 aRa가 성립해야 한다.
    > **A ≡ A**

2. 대칭성(Symmetry)\
    aRb이면 bRa도 성립해야 한다.
    > **A ≡ B 라면 B ≡ A**

3. 추이성(Transivity)\
    aRb이고 bRc이면 aRc가 성립해야 한다.
    > **A ≡ B, B ≡ C 라면 A ≡ C**

동치 관계가 정의되면 서로 동치인 원소들을 하나의 집합으로 묵을 수 있다.\
하나의 원소는 정확히 하나의 동치 클래스에 속한다.

### 실습 - 리스트로 동치 클래스 구현하기

```c
typedef struct ListNode
{
	int data;
	struct ListNode *link;
} ListNode;

int main()
{
	FILE *fp_r, *fp_w;
	int size = 0;
	fp_r = fopen("input.txt", "r");
	fscanf(fp_r, "%d", &size);
	short int out[50];
	ListNode *seq[50];
	int num_list[50];
	memset(num_list, -1, 50);
	int e_class[50][50];
	memset(e_class, -1, (50 * 50));
	for (int i = 0; i < 50; i++)
	{
		out[i] = 1;
		seq[i] = NULL;
	}
	int p = 0, q = 0, k = 0;
	ListNode *x, *y, *top;
	char equal;
	for (int j = 0; j < size; j++)
	{
		fscanf(fp_r, "%d %c %d", &p, &equal, &q);
		num_list[k++] = p;
		num_list[k++] = q;
		x = (ListNode *)malloc(sizeof(ListNode));
		x->data = q;
		x->link = seq[p];
		seq[p] = x;
		x = (ListNode *)malloc(sizeof(ListNode));
		x->data = p;
		x->link = seq[q];
		seq[q] = x;
	}
	fclose(fp_r);
	int max_num = 0;
	for (int s = 0; s < k; s++)
	{
		if (max_num < num_list[s])
		{
			max_num = num_list[s];
		}
	}
	for (int s = 0; s <= max_num; s++)
	{
		int count = 0;
		for (int u = 0; num_list[u] != -1; u++)
		{
			if (s == num_list[u])
			{
				count++;
				break;
			}
		}
		if (count == 0)
		{
			out[s] = 0;
		}
	}
	int row = 0;
	for (int r = 0; r <= max_num; r++)
	{
		int col = 0;
		if (out[r])
		{
			e_class[row][col++] = r;
			out[r] = 0;
			x = seq[r];
			top = NULL;
			for (;;)
			{
				while (x)
				{
					p = x->data;
					if (out[p])
					{
						e_class[row][col++] = p;
						out[p] = 0;
						y = x->link;
						x->link = top;
						top = x;
						x = y;
					}
					else
					{
						x = x->link;
					}
				}
				if (!top)
					break;
				x = seq[top->data];
				top = top->link;
			}
			row++;
		}
	}

	return 0;
}
```
