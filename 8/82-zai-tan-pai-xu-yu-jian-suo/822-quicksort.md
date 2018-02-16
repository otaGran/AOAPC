# QuickSort
---
## 1. QuickSort


Divide and Conquer.

1.划分问题

    把数组的各个元素重排后分成左右两部分，使得左边的任意元素都小于或等于右边的任意元素。

2.递归求解

    对左右两部分分别做排序

3.合并问题

    无需合并。此时数组已排序

  ```c++

  int parition(int* A, int lo,int hi){
      int pivot = A[hi];
      int i = lo - 1;
      for(int j = lo;j<hi;j++){
          if(A[j] < pivot){
              i += 1;
              swap(A[i],A[j]);
          }
      }
      swap(A[i+1],A[hi]);
      return i+1;
  }
  void quickSort(int* A, int lo, int hi){
      if(lo < hi){
          int p = parition(A, lo, hi);
          quickSort(A, lo, p-1);
          quickSort(A, p, hi);
      }
  }


    ```
---

## 2. Top-K

  沿用quick-sort基本代码，并进一步优化为O(n)

  在每次parition后判断pivot位置，递归左半或右半


  ```c++
    int parition(int* A,int lo,int hi){
        int pivot = A[hi];//pick an element
        int i = lo - 1;
        for(int j = lo;j < hi;j++){
            if(A[j] < pivot){
                i += 1;
                swap(A[i],A[j]);
            }
        }
        swap(A[hi],A[i+1]);
        return i+1;
    }
    int topK(int* A, int lo, int hi,int k){
        if(lo < hi){
            int p = parition(A,lo,hi);
            int howManyInHi = hi - p + 1;
            printf("lo: %d hi: %d p: %d\n",lo,hi,p);
            if(howManyInHi == k){
                return A[p];
            }
            if(howManyInHi > k) {
                topK(A, p, hi, k);
            }
            else {
                topK(A, lo, p - 1, k-howManyInHi);
            }
        }
    }
    ```
