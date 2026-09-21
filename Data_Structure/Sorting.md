# 정렬(Sorting)

## 목차

- [정렬이란?](#정렬이란)
- [Insertion Sort(삽입 정렬)](#insertion-sort삽입-정렬)
- [Quick Sort(퀵 정렬)](#quick-sort퀵-정렬)
  - [퀵 정렬의 구현](#퀵-정렬의-구현)
- [Merge Sort(병합 정렬)](#merge-sort병합-정렬)
  - [반복문을 사용한 병합 정렬 구현](#반복문을-사용한-병합-정렬-구현)
  - [재귀 함수를 사용한 병합 정렬 구현](#재귀-함수를-사용한-병합-정렬-구현)
  - [Natural Merge Sort(자연 병합 정렬)](#natural-merge-sort자연-병합-정렬)
- [Heap Sort(힙 정렬)](#heap-sort힙-정렬)
- [정렬은 얼마나 빨라질 수 있는가?](#정렬은-얼마나-빨라질-수-있는가)

## 정렬이란?

정렬(Sorting)은 주어진 데이터들을 특정한 기준에 따라 순서대로 나열하는 작업을 의미한다.\
정렬은 데이터를 효율적으로 탐색하거나 관리하기 위해 사용되는 중요한 알고리즘이다.\
특히 데이터가 정렬되어 있으면 이진 탐색과 같은 알고리즘을 활용할 수 있다.

정렬은 데이터의 비교 기준에 따라 여러 방식으로 수행할 수 있다.
- 오름차순(Ascending Order): 작은 값에서 큰 값 순서로 정렬한다.
- 내림차순(Descending Order): 큰 값에서 작은 값 순서로 정렬한다.

정렬 대상은 숫자뿐 아니라 문자열, 객체 등도 될 수 있다. 객체의 경우 특정 멤버 변수나 속성을 비교 기준으로 사용할 수 있다.

정렬은 일반적으로 시간 복잡도를 기준으로 비교한다. 시간 복잡도 외 구분 가능한 기준은 다음과 같다.
- 안정 정렬(Stable Sort): 정렬 기준값이 같은 원소들의 기존 상대적 순서가 유지되는 정렬이다.
- 제자리 정렬(In-place Sort): 정렬을 수행할 때 입력한 데이터의 크기에 비례하는 별도의 저장 공간을 거의 사용하지 않는 정렬이다.

## Insertion Sort(삽입 정렬)

삽입 정렬(Insertion Sort)은 정렬된 부분에 새로운 원소를 알맞은 위치에 삽입하여 전체 데이터를 정렬하는 알고리즘이다.

배열의 첫 번째 원소는 정렬된 상태라고 가정하고, 다음 원소를 이미 정렬된 부분의 알맞은 위치에 삽입한다.\
이렇게 정렬된 원소를 하나씩 늘려가며 배열 끝까지 반복하면 정렬이 완료된다.

삽입 정렬의 시간 복잡도는 거의 정렬이 된 배열인 경우, 즉 최선의 경우 O(n)이다.\
역순으로 정렬된 배열인 경우, 즉 최악의 경우 O(n<sup>2</sup>)이며, 평균적으로 O(n<sup>2</sup>)이다.

삽입 정렬은 안전 정렬이며, 제자리 정렬이다. 또한 데이터가 이미 정렬되어 있거나 거의 정렬되어 있을수록 효율적인 적응형 정렬(Adaptive Sort)이다.

구현이 간단하고, 데이터가 적거나 거의 정렬된 경우 효율적이지만, 데이터가 많으면서 정렬이 거의 안 되있는 경우에는 성능이 좋지 않다.

## Quick Sort(퀵 정렬)

퀵 정렬(Quick Sort)은 분할 정복(Divide and Conquer)을 이용하는 정렬 알고리즘이다.

배열에서 기준이 되는 값인 피벗(Pivot)을 선택한 뒤, 피벗보다 작은 값은 왼쪽에, 큰 값은 오른쪽에 배치한다.\
이후 왼쪽과 오른쪽 부분 배열에 같은 작업을 재귀적으로 수행한다.

분할이 균등하거나 일반적인 경우에는 재귀 깊이가 약 log(n)이므로 시간 복잡도는 O(nlogn)이 된다.\
매번 한쪽으로 치우치면 재귀 깊이가 n에 가까워져 O(n<sup>2</sup>)가 된다.\
따라서 평균 시간 복잡도는 O(nlogn)으로 효율적이다.

퀵 정렬은 불안정 정렬이다. 따라서 같은 값을 가진 원소들의 상대적 순서가 바뀔 수 있다.

### 퀵 정렬의 구현

```c
void quickSort(int nums[], int left, int right)
{
	int pivot, i, j;
	int temp = 0;
	if (left < right)
	{
		i = left;
		j = right + 1;
		pivot = nums[left];
		do
		{
			do i++; while (nums[i] < pivot);
			do j--; while (nums[j] > pivot);
			if (i < j)
			{
				Swap(nums, i, j, temp);
			}
		} while (i < j);
		Swap(nums, left, j, temp);
		quickSort(nums, left, j - 1);
		quickSort(nums, j + 1, right);
	}
}
```

## Merge Sort(병합 정렬)

병합 정렬(Merge Sort)은 분할 정복(Divide and Conquer)을 이용하는 정렬 알고리즘이다.

배열을 작은 부분 배열로 계속 분할한 뒤, 각 부분 배열을 정렬하면서 하나로 병합한다.\
배열을 분할하는 과정과 정렬된 배열을 병합하는 과정으로 이루어진다.

배열을 절반씩 나누므로 분할 깊이는 약 log(n)이다. 각 깊이에서 모든 원소를 병합하는 시간 복잡도는 O(nlogn)이다.\
따라서 최선, 평균, 최악 모든 경우에 시간 복잡도가 O(nlogn)으로 동일하다.

일반적인 배열 기반 병합 정렬은 병합 과정에서 임시 배열을 사용하므로 추가 공간 O(n)이 필요하다.

병합 정렬은 안정 정렬이며 시간 복잡도가 일정하다. 하지만 일반적인 배열 구현에서는 O(n)의 추가 메모리가 필요하다.

### 반복문을 사용한 병합 정렬 구현

```c
void mergeSort(int arr[], int n)
{
	int curr_size;  
	int left_start;
	for (curr_size = 1; curr_size <= n - 1; curr_size = 2 * curr_size)
	{
		for (left_start = 0; left_start < n - 1; left_start += 2 * curr_size)
		{
			int mid = Min(left_start + curr_size - 1, n - 1);

			int right_end = Min(left_start + 2 * curr_size - 1, n - 1);

			merge(arr, left_start, mid, right_end);
		}
	}
}

void merge(int arr[], int l, int m, int r)
{
	int i, j, k;
	int n1 = m - l + 1;
	int n2 = r - m;

	int L[20], R[20];

	for (i = 0; i < n1; i++)
		L[i] = arr[l + i];
	for (j = 0; j < n2; j++)
		R[j] = arr[m + 1 + j];

	i = 0;
	j = 0;
	k = l;
	while (i < n1 && j < n2)
	{
		if (L[i] <= R[j])
		{
			arr[k] = L[i];
			i++;
		}
		else
		{
			arr[k] = R[j];
			j++;
		}
		k++;
	}

	while (i < n1)
	{
		arr[k] = L[i];
		i++;
		k++;
	}

	while (j < n2)
	{
		arr[k] = R[j];
		j++;
		k++;
	}
}
```

### 재귀 함수를 사용한 병합 정렬 구현

```c
void rec_merge(int nums[], int left, int right)
{
	int mid;
	if (left < right)
	{
		mid = (left + right) / 2;
		rec_merge(nums, left, mid);
		rec_merge(nums, mid + 1, right);
		merge(nums, left, mid, right);
	}
}

void merge(int nums[], int left, int mid, int right)
{
	int i, j, k, l;
	i = left;
	j = mid + 1;
	k = left;
	while (i <= mid && j <= right)
	{
		if (nums[i] <= nums[j])
		{
			sorted[k++] = nums[i++];
		}
		else
		{
			sorted[k++] = nums[j++];
		}
	}
	if (i > mid)
	{
		for (l = j; l <= right; l++)
		{
			sorted[k++] = nums[l];
		}
	}
	else
	{
		for (l = i; l <= mid; l++)
		{
			sorted[k++] = nums[l];
		}
	}
	for (l = left; l <= right; l++)
	{
		nums[l] = sorted[l];
	}
}
```

### Natural Merge Sort(자연 병합 정렬)

자연 병합 정렬(Natural Merge Sort)은 입력 데이터 안에 이미 정렬되어 있는 연속 구간(Run)을 찾아 병합하는 정렬 알고리즘이다.

일반적인 병합 정렬은 배열을 중간 지점에서 반으로 나누지만, 자연 병합 정렬은 데이터가 실제로 정렬되어 있는 구간을 기준으로 나눈다.\
따라서 입력 데이터가 이미 정렬되어 있거나 부분적으로 정렬되어 있다면, 일반적인 병합 정렬보다 적은 병합 단계로 정렬을 마칠 수 있다.

Run은 배열에서 연속적으로 정렬되어 있는 구간을 의미한다. 자연 병합 정렬은 이 Run들을 병합하여 전체 배열을 정렬한다.

자연 병합 정렬은 최선의 경우 시간 복잡도가 O(n)이다.

## Heap Sort(힙 정렬)

힙 정렬(Heap Sort)은 힙(Heap) 자료구조를 이용하여 데이터를 정렬하는 알고리즘이다.\
힙 정렬은 제자리 정렬이며 불안정 정렬이다.\
힙 정렬은 Trees 문서에서 이미 다루었으므로 생략하겠다.

## 정렬은 얼마나 빨라질 수 있는가?

일반적인 비교 기반 정렬은 최악의 경우에도 O(nlogn)보다 빠른 시간 복잡도를 달성할 수 없다.\
즉 모든 입력에 대해서 비교 기반 정렬은 시간 복잡도를 O(n)으로 만드는 것은 불가능하다.

시간 복잡도가 O(n)인 정렬은 비교만으로 정렬하는 대신 데이터의 값 범위나 자릿수 같은 추가 정보를 활용해야한다.\
예를 들어, Counting Sort, Radix Sort, Bucket Sort 등이 있다.
