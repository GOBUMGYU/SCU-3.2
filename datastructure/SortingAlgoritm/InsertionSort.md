# Insertion Sort
삽입 정렬은 현재 비교하고자 하는 target(타겟)과 그 이전의 원소들과 비교하며 자리를 교환(swap)하는 정렬 방법이다.

삽입 정렬은 데이터를 ‘비교’하면서 찾기 때문에 ‘비교 정렬’이며 정렬의 대상이 되는 데이터 외에 추가적인 공간을 필요로 하지 않기 때문에 ‘제자리 정렬(in-place sort)’이기도 하다. 정확히는 데이터를 서로 교환하는 과정(swap)에서 임시 변수를 필요로 하나, 이는 충분히 무시할 만큼 적은 양이기 때문에 제자리 정렬로 보는 것이다. 이는 선택정렬과도 같은 부분이다.

그리고 이전에 다뤘던 선택 정렬과는 달리 삽입 정렬은 ‘안정 정렬’이다.

삽입 정렬의 경우 원리 자체는 간단하다. 앞에서부터 해당 원소가 위치 할 곳을 탐색하고 해당 위치에 삽입하는 것이다.

삽입 정렬의 전체적인 과정은 이렇다. (오름차순을 기준으로 설명)

## Insertion Sort 정렬 방법

1. 현재 타겟이 되는 숫자와 이전 위치에 있는 원소들을 비교한다. (첫 번째 타겟은 두 번째 원소부터 시작한다)
2. 타겟이 되는 숫자가 이전 위치에 있던 원소보다 작다면 위치를 서로 교환한다.
3. 그 다음 타겟을 찾아 위와 같은 방법으로 반복한다.

첫 번째 원소는 타겟이 되어도 비교 할 원소가 없기 때문에 처음 원소부터 타겟이 될 필요가 없고 두 번째 원소부터 타겟이 되면 된다.

결과적으로 타겟 이전 원소가 타겟 숫자보다 크기 직전까지 모든 수를 뒤로 한칸씩 밀어내는 것이다.

## 알고리즘 개요

```java
static void inertionSort(int[] a, int n) {
  //라운드
	for(int i = 1; i < n; i++) {
    int j;
    int target = a[i]; //타겟넘버

//타겟이 이전 원소보다 크기 전 까지 반복
    for(j = i; j > 0 && a[j - 1] > target; j--) {
       a[j] = a[j - 1];//이전 원소를 한 칸씩 뒤로 미룬다.
    }
//위 반복문에서 탈출 하는 경우 앞의 원소가 타겟보다 작다는 의미이므로 j번째 원소 뒤에 와야 한다.
    a[j] = target;
}
```

## 삽입정렬의 장점 및 단점

**[장점]**

1. 추가적인 메모리 소비가 적다.
2. 거의 정렬 된 경우 매우 효율적이다. 즉, 최선의 경우 O(N)의 시간복잡도를 갖는다.
3. 안정정렬이 가능하다.

**[단점]**

1. 역순에 가까울 수록 매우 비효율적이다. 즉, 최악의 경우 O(n²)의 시간 복잡도를 갖는다.
2. 데이터의 상태에 따라서 성능 편차가 매우 크다.

### 시간복잡도

Bubble Sort나 Selection Sort 와 이론상 같은 시간복잡도를 갖음에도 평균 비교 횟수에 대한 기대값이 상대적으로 적기 때문에 **평균 시간복잡도가 O(N2) 인 정렬 알고리즘 중에서는 빠른편에 속하는 알고리즘**이다.