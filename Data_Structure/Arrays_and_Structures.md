# 배열과 구조체(Arrays_and_Structures)

## 목차

- [배열(Array)](#배열array)
  - [배열의 특징](#배열의-특징)
  - [배열의 장점](#배열의-장점)
  - [배열의 단점](#배열의-단점)
- [구조체와 공용체](#구조체와-공용체)
  - [구조체(Structure)](#구조체structure)
    - [구조체의 특징](#구조체의-특징)
  - [공용체(Union)](#공용체union)
    - [공용체의 특징](#공용체의-특징)
  - [실습 - 구조체 기초](#실습---구조체-기초)
- [다항식(Polynomials)](#다항식polynomials)
  - [실습 - 다항식의 덧셈 구현](#실습---다항식의-덧셈-구현)
    - [2차원 배열로 구현](#2차원-배열로-구현)
    - [1차원 구조체 배열로 구현](#1차원-구조체-배열로-구현)
- [희소 행렬(Sparse_Matrix)](#희소-행렬sparse_matrix)
  - [실습 - 희소 행렬의 빠른 전치(Fast Transpose) 구현](#실습---희소-행렬의-빠른-전치fast-transpose-구현)

## 배열(Array)

배열은 각 인덱스(index)에 대응하는 값(value)을 저장하는 <인덱스, 값> 쌍들의 집합이다.\
인덱스는 하나 이상의 차원으로 구성된 유한한 순서 집합으로 배열의 각 원소를 식별하는 데 사용된다.

### 배열의 특징

- 배열은 같은 자료형의 여러 데이터를 연속된 메모리 공간에 저장하는 자료구조이다.

- 각 원소는 인덱스를 통해 접근하며, 인덱스는 0부터 시작한다.

- 배열 안에 배열을 저장할 수 있으며, 이를 다차원 배열이라고 한다.

- 배열 이름은 첫 번째 원소를 가리키는 포인터처럼 동작함.

### 배열의 장점

- 빠른 접근(Random Access)\
인덱스를 이용해 원하는 원소에 즉시 접근할 수 있으므로 시간 복잡도는 O(1)이다.

- 메모리 효율성\
동일한 자료형의 데이터를 연속적으로 저장하므로 메모리 관리가 효율적이다.

- 반복문과 함께 사용하기 편리\
같은 형태의 데이터를 일괄 처리하기 쉽다.

### 배열의 단점

- 크기가 고정됨\
선언 후에는 배열의 크기를 변경할 수 없다.

- 중간 삽입 및 삭제가 비효율적임\
원소를 삽입하거나 삭제하려면 나머지 원소를 이동해야 하므로 시간 복잡도는 O(n)이다.

- 자료형이 하나로 제한됨\
하나의 배열에는 하나의 자료형만 저장 가능.

## 구조체와 공용체

구조체(Structure)와 공용체(Union)는 여러 개의 데이터를 하나의 자료형으로 묶기 위해 사용하는 사용자 정의 자료형(User-defined Data Type)이다.

### 구조체(Structure)

구조체는 서로 관련 있는 여러 데이터를 하나의 단위로 묶어 관리하기 위한 자료형이다.\
C언어에서는 struct 키워드를 사용하여 선언한다.

#### 구조체의 특징

- 서로 다른 자료형을 하나로 묶을 수 있다.

- 모든 멤버를 동시에 사용할 수 있다.

- 각 멤버는 독립적인 메모리 공간을 가진다.

- 실제 크기는 멤버들의 크기의 합과 패딩(Padding)을 고려하여 결정된다.

### 공용체(Union)

공용체는 여러 멤버가 하나의 메모리 공간을 공유하는 자료형이다.

#### 공용체의 특징

- 공용체는 모든 멤버가 같은 메모리 공간을 공유한다. 즉, 한 번에 하나의 멤버만 의미 있는 값을 저장할 수 있다.

### 실습 - 구조체 기초

```c
typedef struct
{
	int accountNum;
	char name[30];
	int deposit;
	int loan;
}account;
```

## 다항식(Polynomials)

다항식은 여러 개의 항으로 구성되며, 각 항은 ax<sup>e</sup>의 형태를 가진다. 이때 x는 변수, a는 계수, e는 지수이다.\
이는 <e<sub>i</sub>, a<sub>i</sub>>의 순서쌍의 집합으로 볼 수 있다.

### 실습 - 다항식의 덧셈 구현

#### 2차원 배열로 구현

```c
int polynomial[2][20] = { 0 };

void poly_add(int start_1, int finish_1, int start_2, int finish_2, int start_3, int* finish_3)
{
	int count = 0;

	while (start_1 <= finish_1 && start_2 <= finish_2)
	{
		if (polynomial[1][start_1] < polynomial[1][start_2])
		{
			polynomial[1][start_3] = polynomial[1][start_2];
			polynomial[0][start_3] = polynomial[0][start_2];
			start_2++, start_3++;
		}
		else if (polynomial[1][start_1] == polynomial[1][start_2])
		{
			if (polynomial[1][start_1] == 0 && polynomial[0][start_1] == 0)
			{
				if (polynomial[1][start_2] == 0 && polynomial[0][start_2] == 0)
				{
					break;
				}
			}
			polynomial[0][start_3] = polynomial[0][start_1] + polynomial[0][start_2];
			polynomial[1][start_3] = polynomial[1][start_1];
			start_1++, start_2++, start_3++;
			count++;
		}
		else if (polynomial[1][start_1] > polynomial[1][start_2])
		{
			polynomial[1][start_3] = polynomial[1][start_1];
			polynomial[0][start_3] = polynomial[0][start_1];
			start_1++, start_3++;
		}

		if (start_1 > finish_1 && start_2 > finish_2)
		{
			break;
		}
		else if (start_1 > finish_1)
		{
			start_1--;
			polynomial[1][start_1] = 0;
			polynomial[0][start_1] = 0;
		}
		else if (start_2 > finish_2)
		{
			start_2--;
			polynomial[1][start_2] = 0;
			polynomial[0][start_2] = 0;
		}
	}
	*finish_3 = start_3;
}
```

#### 1차원 구조체 배열로 구현

```c
typedef struct
{
	int coef;
	int exp;
} item;
item polynomial[20];

void poly_add(int start_1, int finish_1, int start_2, int finish_2, int start_3, int* finish_3)
{
	int count = 0;

	while (start_1 <= finish_1 && start_2 <= finish_2)
	{
		if (polynomial[start_1].exp < polynomial[start_2].exp)
		{
			polynomial[start_3].exp = polynomial[start_2].exp;
			polynomial[start_3].coef = polynomial[start_2].coef;
			start_2++, start_3++;
		}
		else if (polynomial[start_1].exp == polynomial[start_2].exp)
		{
			if (polynomial[start_1].exp == 0 && polynomial[start_1].coef == 0)
			{
				if (polynomial[start_2].exp == 0 && polynomial[start_2].coef == 0)
				{
					break;
				}
			}
			polynomial[start_3].coef = polynomial[start_1].coef + polynomial[start_2].coef;
			polynomial[start_3].exp = polynomial[start_1].exp;
			start_1++, start_2++, start_3++;
			count++;
		}
		else if (polynomial[start_1].exp > polynomial[start_2].exp)
		{
			polynomial[start_3].exp = polynomial[start_1].exp;
			polynomial[start_3].coef = polynomial[start_1].coef;
			start_1++, start_3++;
		}

		if (start_1 > finish_1 && start_2 > finish_2)
		{
			break;
		}
		else if (start_1 > finish_1)
		{
			start_1--;
			polynomial[start_1].exp = 0;
			polynomial[start_1].coef = 0;
		}
		else if (start_2 > finish_2)
		{
			start_2--;
			polynomial[start_2].exp = 0;
			polynomial[start_2].coef = 0;
		}
	}
	*finish_3 = start_3;
}
```

## 희소 행렬(Sparse_Matrix)

희소 행렬은 대부분의 원소가 0인 행렬을 의미한다. \
희소 행렬을 일반 행렬처럼 2차원 배열로 저장하면 0인 원소까지 모두 저장하므로 메모리 낭비가 발생한다.\
따라서 0이 아닌 원소만 <행, 열, 값> 형태의 삼중항의 집합으로 저장한다.

### 실습 - 희소 행렬의 빠른 전치(Fast Transpose) 구현

일반적인 전치 알고리즘은 열을 하나씩 검사하기 때문에 시간 복잡도가 O(Columns x Terms)가 된다.\
Fast Tranpose는 각 열에 원소가 몇 개 있는지 먼저 계산한 뒤, 결과 배열에서 각 열이 시작되는 위치를 미리 구한다.\
따라서 시간 복잡도가 O(Columns + Terms)가 된다.

```c
typedef struct
{
	int row;
	int col;
	int value;
}matrix;

void fast_transpose(matrix arr_1[400], matrix arr_2[400], int rows, int nums)
{
	int rowterms[400] = { 0 };
	int start_pos[400] = { 0 };
	int temp = 0;
	for (int i = 0; i < nums; i++)
	{
		temp = arr_1[i].col;
		rowterms[temp]++;
	}
	for (int j = 0; j < rows - 1; j++)
	{
		start_pos[j + 1] = start_pos[j] + rowterms[j];
	}
	int col = 0, row = 0, value = 0;
	for (int k = 0; k < nums; k++)
	{
		col = arr_1[k].col;
		row = arr_1[k].row;
		value = arr_1[k].value;
		arr_2[start_pos[col]].row = col;
		arr_2[start_pos[col]].col = row;
		arr_2[start_pos[col]].value = value;
		start_pos[col]++;
	}
}
```
