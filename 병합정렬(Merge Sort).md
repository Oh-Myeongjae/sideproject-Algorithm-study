# 병합정렬

- 분할 정복 기법과 재귀 알고리즘을 이용해서 정렬하는 알고리즘

**분할 정복 기법** → 쪼개어 작은 문제들을 해결하는 기법

**재귀** → 자기 자신 다시 호출

주어진 배열을 원소가 하나 밖에 남지 않을 때까지 계속 둘로 쪼갠 후 다시 크기순으로 재배열하면서 원래 크기의 배열로 합친 것

**매커니즘**

- [6,5,3,1,8,7,2,4]
- [6,5,3,1] [8,7,2,4]
- [6,5] [3,1] [8,7] [2,4]
- [6] [5] [3] [1] [8] [7] [2] [4] (더 이상 쪼갤 수 없는 상태 → **분할 정복 기법**)

---

- [5,6] [1,3] [7,8] [2,4] (작은 수 앞에 / 큰 수 뒤에 **재귀**)
- [1,3,5,6] [2,4,7,8] (다시 한 배열에 4개가 들어가게 끔 **재귀**)
- [1,2,3,4,5,6,7,8] (다시 한 배열에 8개가 들어가게 끔 **재귀**)

**특징**

- 쪼개는 시간이 점점 줄어 O(logN) 시간이 필요하며, 병합하는데 모든 값 비교해야하므로 O(N)시간이 소모되어 총 시간 복잡도는 O(NlogN)입니다.(병합 비용 > 분할 비용)
- 다른 알고리즘과 달리 인접값들을 비교하여 자리 교대(swap)이 일어나지 않습니다.

**장점**

- 기준값이 없기에 기준값에 따라 성능이 달리지는 경우는 없음

**단점**

- 두 배열을 병합할 때 병합 결과를 담을 배열이 추가로 필요 → 공간 복잡도 O(N)

```
	public static void main(String[] args) {
		int[] arr = {50,62,51,32,80,90,100,41,30 };
		System.out.println("Before sorting: " + Arrays.toString(arr));
		mergeSort(arr,0,arr.length-1);
		System.out.println("After sorting: " + Arrays.toString(arr));	
	}

	private static void mergeSort(int[] arr, int left, int right) {
		if(left<right) {
			int mid = (left+right)/2;
			
			mergeSort(arr, left, mid);
			mergeSort(arr, mid+1, right);
			
			merge(arr,left,mid,right);
		}
		
	}
											
	private static void merge(int[] arr, int left, int mid, int right) {
		int[] L = Arrays.copyOfRange(arr, left, mid+1);
		int[] R = Arrays.copyOfRange(arr, mid+1, right+1);
		
		int idx = left;
		int l = 0;
		int r = 0;
		
		while(l<L.length && r<R.length) {
			if(L[l]<=R[r]) {
				arr[idx] = L[l];
				l++;
			}else {
				arr[idx] = R[r];
				r++;
			}
			idx++;
		}
		
		while(l<L.length) {
			arr[idx] = L[l];
			l++;
			idx++;
		}
		
		while(r<R.length) {
			arr[idx] = R[r];
			r++;
			idx++;
		}
	}
```
