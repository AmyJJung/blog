---
layout: post
title: (알고리즘) Quick Sort와 Merge Sort의 시간복잡도  
tags:
  - 알고리즘
---

<br>

### Quick Sort의 시간복잡도

---

- 시간복잡도 : O(nlogn) / 최악의 시간복잡도 : O(n^2)

- QuickSort의 구현 코드 

- ```java
    public static void quickSort(int[] arr, int left, int right) {
        int part2 = partition(arr,left,right);
        if(left+1<part2) {
          quickSort(arr,left,part2-1);
        }
        if(part2<right) {
          quickSort(arr,part2,right);
        }
  
    }
  
    public static int partition(int[] arr, int left, int right) {
        int pivot = arr[(left+right)/2]; 
        while(left<=right) {
          while(arr[left]<pivot) left++;
          while(arr[right]>pivot) right--;
          if(left<=right) {
            swap(arr,left,right);
            left++; right--;
          }
        }
        return left;
    }
  
    public static void swap(int[] arr, int a, int b) {
      int temp = arr[a];
      arr[a] = arr[b];
      arr[b] = temp;
    }
  ```

- partitioning 에 걸리는 시간 => Θ(n) 

- - n길이의 배열이 들어왔을때 pivot을 기준으로 나머지 n-1개의 숫자를 비교
  
  - 즉, 파티셔닝을 한번 수행할 때 마다 최대 n번 숫자비교 

- partitioning이 수행되는 횟수  => lonN / N
  
  - 경우에 따라 횟수가 달라진다 (**Balanced Partitioning** vs **unbalanced Partitioning**)
  
  - **Balanced Partitioning**
    
    - 각 하위 문제가 기존 문제의 절반 크기로 나누어지는 경우  => logN
  
  - **Unbalanced Partitioning**
    
    - 매번 pivot 기준으로 정렬할 때 마다 1과 n-1개로 나누어지는 경우 => N
  
  ![](https://raw.githubusercontent.com/dadaJJung/blog/0ef5dafb8f4c8bdea4504bbdb734e16b12603435/images/DataStructure/SortTimeComplexity.png)

<br>

<br>

### Merge Sort의 시간복잡도

---

- Merge Sort는 물리적으로 배열의 반을 나누기 때문에 O(nlogn)의 시간복잡도를 가진다

- 하지만 QuickSort와는 달리 추가적인 배열공간이 필요하다. 

- Merge Sort의 구현코드

- ```java
  //arr 배열 => 정렬될 숫자가 담긴 배결
  //temp 배열 => 정렬하면서 임시로 데이터를 담기 위해 필요한 배열, arr.length 길이와 같다
  
  public static void mergeSort(int[] arr, int left, int right, int[] temp) {
    if(left<right){
      int mid = (left+right)/2;
      mergeSort(arr,left,mid,temp);   
      mergeSort(arr,mid+1,right,temp);
      merge(arr,left,mid,right,temp);
    }
  }
  
  public static void merge(int[] arr, int left, int mid, int right, int[] temp){
  
    int index = left;
    int s1 = left;
    int s2 = mid+1;
  
    while(s1<=mid && s2<=right){
      if(arr[s1]<=arr[s2]){
        temp[index++] = arr[s1++];
      }else{
        temp[index++] = arr[s2++];
      }
    }
  
    while(s1<=mid){
      temp[index++] = arr[s1++];
    }
  
    while(s2<=right){
      temp[index++] = arr[s2++];
    }
  
    for(int i=left; i<=right; i++){
      arr[i] = temp[i];
    }
  }
  ```
