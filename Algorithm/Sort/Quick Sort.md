# Quick Sort Algorithm

- 찰스 앤터니 리처드 호어가 개발한 정렬 알고리즘. 
- 불완전 정렬로, 다른 원소와의 비교만으로 정렬을 수행하는 비교 정렬에 속한다. 
- 분할 정복 알고리즘의 하나로, 평균적으로 매우 빠른 수행 속도를 가진다. 
  - 분할 정복 방법
    - 문제를 작은 문제로 분리하고 각각을 해결한 다음, 결과를 모아서 원래의 문제를 해결하는 방법.
    - 대개 순환 호출을 이용하여 구현
- 퀵 정렬 알고리즘의 개념
  - 하나의 리스트를 피벗을 기준으로 두 개의 비균등한 크기로 분할하고 분할된 리스트를 정렬한 다음, 두 개의 정렬된 부분 리스트를 합하여 전체가 정렬된 리스트가 되게 하는 방법이다.
  - 퀵 정렬의 단계
    - 분할(divide) : 입력 배열을 피벗을 기준으로 비균등하게 2개의 부분 배열로 분할
    - 정복(conquer) : 부분 배열을 정렬. 부분 배열의 크기가 충분히 작지 않으면 순환 호출을 이용하여 다시 분할 정복 방법을 적용
    - 결합(combine) : 정렬된 부분 배열들을 하나의 배열에 합병
    - 순환 호출이 한번 진행될 때마다 최소한 하나의 원소(피벗)는 위치가 확정 되므로, 이 알고리즘은 반드시 끝난다는 것이 보장 가능
- 알고리즘 구현(java, 내림차순)
  - 리스트 안에 있는 한 요소를 선택->피벗(pivot)
  - 피벗을 기준으로 작은 요소들은 피벗의 왼쪽으로, 큰 요소들은 오른쪽으로 모두 옯겨진다.
  - 피벗을 제외한 왼쪽 리스트와 오른쪽 리스트를 다시 정렬
    - 분할된 부분 리스트에 대하여 순환 호출을 이용해 정렬을 반복
    - 부분 리스트에서도 다시 피벗을 정하고 피벗을 기준으로 2개의 부분 리스트로 나누는 과정을 반복
  - 부분 리스트들이 더 이상 분할이 불가능할 때까지 반복. 리스트의 크기가 0이나 1이 될 때까지 반복

```java
public static void quickSort(String[] arr, int left, int right) {
		int pivot = left;
		int idxL = pivot;
		int idxR = left+1;
		
		if(left<right) {
			for(;idxR<=right;idxR++)
				if(arr[pivot]>arr[idxR]) {
					idxL++;
					swap(arr, idxL, idxR);
				}
			swap(arr, left, idxL);
			pivot = idxL;
			
			quickSort(arr, left, pivot-1);
			quickSort(arr, pivot+1, right);
		}
	}
	public static void swap(String[] arr, int idxL, int idxR) {
		String temp = arr[idxL];
		arr[idxL] = arr[idxR];
		arr[idxR] = temp;
	}
```

- 퀵 정렬의 특징

  - 정렬된 리스트에 대해서는 불균형 분할에 의해 오히려 수행시간이 더 걸린다.

  - 퀵정렬의 불균형 분할을 방지하기 위하여 피벗을 선택할 때 더욱 리스트를 균등하게 분할 가능한 데이터를 선택 ex) 데이터 몇개를 선택해 중간값을 피벗으로 선택

- 퀵 정렬의 시간 복잡도

  - 최선의 경우 : O(nlog2n)
  - 최악의 경우 : O(n^2)
  - 평균 : O(nlog2n), 시간 복잡도가 같은 정렬 알고리즘과 비교했을 때도 가장 빠르다.
    - b/c 불필요한 데이터의 이동 감고, 먼거리의 데이터를 교환, 한번 결정된 피벗들이 추후 연산에서 제외