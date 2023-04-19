Insertion Sort는 2번째 원소부터 시작하여 그 앞(왼쪽)의 원소들과 비교하여 삽입할 위치를 지정한 후, 원소를 뒤로 옮기고 지정된 자리에 자료를 삽입 하여 정렬하는 알고리즘이다.

 #### 장점
- 알고리즘이 단순하다.
 - 대부분의 원소가 이미 정렬되어 있는 경우, 매우 효율적일 수 있다.
 - 정렬하고자 하는 배열 안에서 교환하는 방식이므로, 다른 메모리 공간을 필요로 하지 않는다. => 제자리 정렬(in-place sorting)

 #### 단점
 - 평균과 최악의 시간복잡도가 O(n^2)으로 비효율적이다.
 - Bubble Sort와 Selection Sort와 마찬가지로, 배열의 길이가 길어질수록 비효율적이다.

````
public static void main(String[] args) {
		int[] arr = {50,62,51,32,80,90,100,41,30 };
        System.out.println("Before sorting: " + Arrays.toString(arr));
        InsertionSort(arr);
        System.out.println("After sorting: " + Arrays.toString(arr));	
	}

	private static void InsertionSort(int[] arr) {
		for (int i = 1; i < arr.length; i++) {
			int score = arr[i];
			int findIdx = i-1;
			while(findIdx >= 0 && arr[findIdx]>score) {
				arr[findIdx+1] = arr[findIdx];
				findIdx--;
			}
			arr[findIdx+1] = score;
		}
	}
````
