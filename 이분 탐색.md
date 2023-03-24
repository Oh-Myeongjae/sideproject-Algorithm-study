## 이분 탐색/이진 탐색 -- (Binary Search)

- 탐색 범위를 두 부분으로 분할하면서 찾는 방식
- 배열 내부의 데이터가 정렬되어 있어야만 사용할 수 있는 알고리즘

```
public int BinarySearch(int[] arr, int num) {
        int count = 0;
        int start = 0;
        int mid = 0;
        int end = arr.length - 1;

        Arrays.sort(arr);

        while (start <= end) {
            count++;
            mid = (start + end) / 2;

            if (arr[mid] == num) {
                return count;
            } else if (arr[mid] > num) {
                end = mid - 1;
            } else {
                start = mid + 1;
            }
        }
        return -1;
    }
```
