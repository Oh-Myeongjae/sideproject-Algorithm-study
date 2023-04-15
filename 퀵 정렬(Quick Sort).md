# 퀵 정렬(Quick Sort)이란?
- 분할 정복 알고리즘의 하나, 평균적으로 매우 빠른 수행 속도를 자랑하는 정렬 방법
   - 분할 정복(divide and conquer) 방법 : 문제를 작은 2개의 문제로 분리하고 각각을 해결한 다음, 결과를 모아서 원래의 문제를 해결하는 전략
- 불안정 정렬, 다른 원소와의 비교만으로 정렬을 수행하는 비교 정렬에 속한다.

### 과정 설명
1. 리스트 안에 있는 한 요소를 선택한다. 이렇게 고른 원소를 피벗(pivot)이라고 한다.
2. 피벗을 기준으로 피벗보다 작은 요소들은 모두 피벗의 왼쪽으로 옮겨지고 피벗보다 큰 요소들은 모두 피벗의 오른쪽으로 옮겨진다.
   (피벗을 중심으로 왼쪽 : 피벗보다 작은 요소들 / 오른쪽 : 피벗보다 큰 요소들)
3. 피벗을 제외한 왼쪽 리스트와 오른쪽 리스트를 다시 정렬한다.
   (부분 리스트에서도 다시 피벗을 정하고 피벗을 기준으로 2개의 부분 리스트로 나누는 과정을 반복한다.)
4. 부분 리스트들이 더 이상 분할이 불가능할 때까지 반복한다.
   (리스트의 크기가 0이나 1이 될 때까지 반복한다.)

### 요약
- 하나의 리스트를 피벗을 기준으로 두 개의 비균등한 크기로 분할하고 분할된 부분 리스트를 정리한 다음, 두 개의 정렬된 부분 리스트를 합하여 전체가 정렬된 리스트가 되게 하는 방법이다.
  - 분할 : 비균등하게 2개의 부분 배열
  - 정복 : 부분 배열을 정렬
  - 결합 : 정렬된 부분 배열들을 하나의 배열에 합병

### 특징
- 장점
  - 속도가 빠르다.
  - 추가 메모리 공간을 필요로 하지 않는다.
- 단점
  - 정렬된 리스트에 대해서는 퀵 정렬의 불균형 분할에 의해 오히려 수행시간이 더 많이 걸린다.  

## 구현
```
public static void main(String[] args) {
		int[] arr = { 5, 3, 8, 4, 2 };
        int n = arr.length;
        System.out.println("Before sorting: " + Arrays.toString(arr));
        quickSort(arr, 0, n - 1);
        System.out.println("After sorting: " + Arrays.toString(arr));	
	}

	private static void quickSort(int[] arr, int start, int end) {
		if(start<end) {
			
			int pivot = partition(arr,start,end);
			
			quickSort(arr,start,pivot-1);
			quickSort(arr,pivot+1,end);
		}
	}

	private static int partition(int[] arr, int start, int end) {
		
		int pivot = arr[start];
		int l = start;
		int r = end;
		
		while(l<r) {
			while(pivot<arr[r]) {
				r--;
			}
			while(l<r && pivot>=arr[l]) {
				l++;
			}

			int temp = arr[l];
			arr[l] = arr[r];
			arr[r] = temp;

		}
		arr[start] = arr[l];
		arr[l] = pivot;
		return l;
	}
   ```
