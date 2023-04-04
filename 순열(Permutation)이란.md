# 순열(Permutation)이란 

- 서로 다른 n개의 값 중에서 r개의 숫자를 선택 후 나열하는 것
  - [1,2,3,4]인 4개의 원소로 이루어진 배열에서 2개의 숫자를 뽑아 나열하는 경우는
  - (1,2)(1,3)(1,4)(2,1)(2,3)(2,4)(3,1)(3,2)(3,4)(4,1)(4,2)(4,3) 로 12개이다.

### 순열의 알고리즘적 구현 1  - swap을 이용한 구현

- 배열의 첫 값부터 순서대로 하나씩 바꾸어 모든 값을 한번씩 swap한다.
- depth를 기준 인덱스로 하여 depth보다 인덱스가 작은 값들은 그대로 고정하고
- depth보다 인덱스가 큰 값들만 가지고 다시 swap을 진행한다.
- 순열의 경우의 수가 사전적으로 정렬되어 나오지 않는다.

```
public class Main {
  
    public static void main(String[] args) {
        int arr[] = {1,2,3,4}; //뽑을 배열
        per permutation = new per();
        permutation.permutation(arr, 0, 2); //arr에 있는 숫자들중 2개 순열로 뽑기
     
        System.out.print("총 개수: ");
        System.out.println(permutation.count);
    }
}

class per{
    public int count; //순열 경우의 수
      
    public per(){
        this.count = 0;
    }
      
      
    //permutation: arr에 있는 숫자들 중 r개 순열로 뽑기
    public void permutation(int[] arr, int depth, int r){
        if(depth==r){ //depth와 r이 같아지면 출력
            for(int i = 0; i < r; i++){
                System.out.print(arr[i]);
                System.out.print(" ");
            }
            System.out.println();
            count++;
            return;
        }
        for(int i = depth; i<arr.length; i++){
            this.Swap(arr, depth, i);
            this.permutation(arr, depth+1, r); //재귀함수 들어갈때 depth+1
            this.Swap(arr, depth, i); //복구
        }
      
        }
          
    public void Swap(int[] arr, int index1, int index2){
        int tmp = arr[index1];
        arr[index1] = arr[index2];
        arr[index2] = tmp;
    }
}
```


### 순열의 알고리즘적 구현 2  - Visited 배열을 이용해 DFS로 구현
- DFS를 돌면서 모든 인덱스를 방문하여 craft 에 값을 넣고 넣은 값의 visited값을 true로 바꾼다.
- visited값이 false인 값을 넣는다. 
- depth 값은 craft 에 들어간 숫자의 길이이다. 
- depth 의 값이 r 만큼 되면 craft 에 들어있는 값을 출력
```
public class Main {

    public static void main(String[] args) {
        int arr[] = {1,2,3,4};
        int r = 2;
        //4개중 2개 뽑아 나열
        per permutation = new per();
        permutation.permutation(arr, 0 ,r, new boolean[arr.length], new int[r]);
       
        System.out.print("총 개수: ");
        System.out.println(permutation.count);
    }
}

class per{
public int count;

    public per(){
        this.count = 0;
    }
        
        
    //permutation: arr에 있는 숫자들 중 r개 순열로 뽑기, arr.length의 크기를 갖고 visited를 나타내는 boolean 배열, 값을 저장하는 int배열
    public void permutation(int[] arr,int depth, int r, boolean[] visited, int[] craft){
        if(depth==r){ //depth 와 r이 같아지면 출력
            for(int i = 0; i< craft.length; i++){
                System.out.print(craft[i]);
                System.out.print(" ");
            }
            System.out.println("");
            count++;
            return;
        }
        
        for(int i = 0; i<arr.length; i++){
            if(visited[i]==false){//visite가 false이면 아직 안들어간 숫자, true이면 이미 들어간 숫자이다
                visited[i] = true;
                craft[depth] = arr[i];
                this.permutation(arr, depth+1 ,r,visited, craft);//재귀함수 들어갈때 depth+1
                visited[i] = false; //복구
                craft[depth] = 0; //복구
            }
        }
        
        
        }
}
```

### 중복 순열
- n개중에 r개를 선택하는 경우의 수(중복 허용)
- 순서 O
- (1,2)(1,3)(1,4)(2,1)(2,3)(2,4)(3,1)(3,2)(3,4)(4,1)(4,2)(4,3) + (1,1)(2,2)(3,3)(4,4) 16개

### 조합
- 서로 다른 n개중에 r개를 선택하는 경우의 수
- 순서 X
- (1,2)(1,3)(1,4)(2,3)(2,4)(3,4) 6개

### 중복 조합
- n개중에 r개를 선택하는 경우의 수
- 순서 x
- 조합과 동일하지만 중복 허용
- (1,2)(1,3)(1,4)(2,3)(2,4)(3,4) + (1,1)(2,2)(3,3)(4,4) 10개