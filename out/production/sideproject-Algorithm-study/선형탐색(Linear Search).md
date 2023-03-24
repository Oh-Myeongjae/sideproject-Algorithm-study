**선형탐색이란?(Linear Search)**

- 자료가 일렬로 나열되었을 때, 한쪽방향으로 차례대로 탐색하는 것을 말합니다.

**선형탐색의 특징**

- **장점**
    - 알고리즘의 가장 기초 중 하나이기 때문에 굉장히 쉬움.
- **단점**
    - 배열 크기와 시간이 비례하기 때문에 배열이 클 수 록 탐색 시간이 길어짐.

```java
public static int LinearSearch(int[] arr, int find) {
	for (int i = 0; i < arr.length; i++) {
	// 찾는 값이 배열에 있으다면 그것의 위치를 반환함.
		if (find == arr[i]) {
			return i;
		}
	}
	// 찾는 값이 없는 경우
	return -1;
}
```
