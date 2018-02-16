# 8.2.3 bsearch
1. BinarySearch

    只适用于有序数列，时间复杂度O(logn)，一般不使用递归。

    ~~~c++
    int bsearch(int* A, int x, int y, int target){
        int m;
        while(x < y){
            m = x + (y-x)/2;
            if(A[m] == target)
                return m;
            else{
                if(A[m] < target){
                    x = m+1;
                }
                else{
                    y = m;
                }
            }
        }
        return -1;
    }

    ~~~

2. 二分求上下界

    问题：数组内有多个v，如何求出值等于v的完整区间

    以下程序返回一个位置i,v值存在时i代表v第一次出现时的位置,v值不存在时i代表v应该插入的位置,插入后数组仍有序.

    * A[m] == v 此时已找到一个,左边可能还有 区间变为[x,m]

    * A[m] <  v i不可能等于m,一定在右边 区间变为[m+1,y]

    * A[m] >  v 一定在左边 区间变为[x,m]

  输入为左闭右开区间[x,y),但输出可能为闭区间[x,y],因为如果v值大于A[x-1],输出为y.

  ~~~c++
    int my_lower_bound(int* A,int x,int y,int v){
        int m;
        while(x < y){
            m = x + (y-x)/2;
            if(A[m]>=v){
                y = m;
            }else{
                x = m + 1;
            }
        }
        return x;
    }

    ~~~

    ---

    以下程序返回一个位置i,v值存在时代表v最后一次出现的位置,v值不存在时i代表v应该插入的位置,插入后数组仍有序.

    * A[m] == v 此时已经找到一个v值,还有更多可能存在于右半边 区间变为[m+1,y]

    * A[m] < v m不可能!! 一定在右边 区间变更为[m+1,y]

    * A[m] > v m有可能!! 可能在左边 区间变更为[x,m]

  ~~~c++
  int my_upper_bound(int* A,int x,int y,int v){
      int m;
      while(x < y){
          m = x + (y-x)/2;
          if(A[m] <= v){
              x = m + 1;
          }else{
              y = m;
          }
      }
      return x;
  }

  ~~~
