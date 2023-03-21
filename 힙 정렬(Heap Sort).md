# 힙 정렬

- 힙은 완전 이진트리 기반의 트리형 자료구조로써 최댓값이나 최솟값을 찾아내기 위해 사용된다.
- 힙에는 최대 힙과 최소 힙이 존재한다.
- 최대 힙은 부모 노드의 키가 자식 노드의 키보다 같거나 큰 완전 이진 트리이며 최소 힙은 자식 노드의 키가 부모 노드의 키보다 같거나 큰 완전 이진 트리이다.

*완전 이진 트리?

- 삽입할 때 왼쪽부터 차례로 추가하는 이진트리

### 힙 생성(Heapify) 알고리즘

- 어떤 부모 노드의 두 자식 노드 중 크기가 더 큰 자식을 부모와 바꾸는 알고리즘이다.
- 이러한 과정은 자식이 더이상 존재하지 않을 때까지 반복된다.
- 힙 정렬은 이러한 힙 생성 알고리즘을 사용하고 있다.


```
import java.util.*;

public class Main {
	static void SWAP(int[] arr,int i,int j) {
		int temp=arr[i];
		arr[i]=arr[j];
		arr[j]=temp;
	}
	static void heapify(int[] arr,int n,int i) {
		//인덱스가 0부터 시작이기에 다음과 같이 설정함
		int p=i; //부모 인덱스
		int l=2*i+1; //왼쪽자식 인덱스
		int r=2*i+2; //오른쪽자식 인덱스
	
		//만약 왼쪽 자식의 값이 더 크다면
		if(l<n && arr[p]<arr[l]) p=l;
	
		//만약 오른쪽 자식의 값이 더 크다면
		if(r<n && arr[p]<arr[r]) p=r;
	
		//여기까지 한 것 : 부모, 왼쪽 자식, 오른쪽 자식 값 비교하여 최대 값이 있는 노드를 찾음
	
		//만약 자식의 값이 부모의 값보다 더 크다면
		if(i!=p) {
			SWAP(arr,p,i); // 부모와 자식의 값을 바꾸고
			heapify(arr, n, p); //부모의 위치에서 자식노드 위치로 내려간 노드를 기준으로 힙을 재구성한다.(DownHeap) 
		}
	}


	static void HeapSort(int[] arr) {
		int n=arr.length;
	
		//init(i가 n/2-1부터 시작하는 이유는 부모노드 인덱스가 관심 영역이기 때문이다.)
		//Max-Heap으로 구성하기
		for(int i=n/2-1;i>=0;i--) {
			heapify(arr,n,i);
		}
	
		//extract
		for(int i=n-1;i>0;i--) {
			SWAP(arr,0,i);//Heap의 root에 위치한 max값을 가장 마지막 리프노드와 교환한다.
			heapify(arr, i, 0); //힙 사이즈를 하나씩 줄여나가면서, 힙을 재구성한다.
		}
		//이 결과로는 오름차순 정렬이 될 것이다.
	
	}
	public static void main(String[] args) {
		int[] arr= {22,16,123,6,1,23,5,4,2,3,13,25,78,97,65,52,45};
		HeapSort(arr);
		System.out.println(Arrays.toString(arr));
	}
}
```
