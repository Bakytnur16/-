# 基础算法

## 查找

### 二分查找
```
def search(arr,l,r,x):
    if r >= 1:
        mid = int(l + (r - l)/2)
        if arr[mid] == x:
            return mid
        elif arr[mid] > x:
            return search(arr, l, mid-1, x)
        else:
            return search(arr,mid+1, r, x)
    else:
        return -1

arr = [2, 3, 4, 10, 40]
x = 10

result = search(arr, 0, len(arr) - 1,x)

if result != -1:
    print('元素在数组中的索引为 %d' % result)
else:
    print('元素不在数组中')
```
### 线性查分

## 排列
### 插入排序 Insertion Sort
```
arr = [23, 13, 224, 10, 40,3]
def insertionSort(arr):
    for i in range(1, len(arr)):
        key = arr[i]
        j = i -1
        while j >= 0 and key < arr[j]:
            arr[j+1] = arr[j]
            j -= 1
        arr[j + 1] = key
insertionSort(arr)
print('排序后的数组：')
for i in range(len(arr)):
    print('%d' %arr[i])
```
## 快速排序 
Divide and conquer 把一个序列（list）分为较小和较大的2个子序列，然后递归地排序两个子序列。
挑选基准值 pivot
分割
```
def partition(arr,low,high):
    i = (low -1)
    pivot = arr[high]

    for j in range(low, high):
        if arr[j] <= pivot:
            i = i+1
            arr[i], arr[j] = arr[j],arr[i]
    arr[i+1],arr[high] = arr[high],arr[i + 1]
    return (i+1)

#arr[] --> 排序数组
# low  --> 起始索引
# high  --> 结束索引

def quickSort(arr, low, high):
    if low < high:
        pi = partition(arr, low, high)

        quickSort(arr, low, pi - 1)
        quickSort(arr, pi + 1, high)


arr = [10, 7, 8, 9, 1, 5]
n = len(arr)
quickSort(arr, 0, n - 1)
print("排序后的数组:")
for i in range(n):
    print("%d" % arr[i])
```
### 选择排序 Selection sort
首先在未排序序列中找到最小（大）元素，存放到排序序列的起始位置，然后，再从剩余未排序元素中继续寻找最小（大）元素，然后放到已排序序列的末尾。
```
import sys

A = [64, 25, 12, 22, 11]

for i in range(len(A)):

    min_idx = i
    for j in range(i + 1, len(A)):
        if A[min_idx] > A[j]:
            min_idx = j

    A[i], A[min_idx] = A[min_idx], A[i]

print("排序后的数组：")
for i in range(len(A)):
    print("%d" % A[i])
```
### 冒泡排序
它重复地走访过要排序的数列，一次比较两个元素，如果他们的顺序错误就把他们交换过来
```
def bubbleSort(arr):
    n = len(arr)

    # 遍历所有数组元素
    for i in range(n):

        # Last i elements are already in place
        for j in range(0, n - i - 1):

            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]


arr = [64, 34, 25, 12, 22, 11, 90]

bubbleSort(arr)

print("排序后的数组:")
for i in range(len(arr)):
    print("%d" % arr[i])
```
### 归并排序
```
def merge(arr, l, m, r): 
    n1 = m - l + 1
    n2 = r- m 
  
    # 创建临时数组
    L = [0] * (n1)
    R = [0] * (n2)
  
    # 拷贝数据到临时数组 arrays L[] 和 R[] 
    for i in range(0 , n1): 
        L[i] = arr[l + i] 
  
    for j in range(0 , n2): 
        R[j] = arr[m + 1 + j] 
  
    # 归并临时数组到 arr[l..r] 
    i = 0     # 初始化第一个子数组的索引
    j = 0     # 初始化第二个子数组的索引
    k = l     # 初始归并子数组的索引
  
    while i < n1 and j < n2 : 
        if L[i] <= R[j]: 
            arr[k] = L[i] 
            i += 1
        else: 
            arr[k] = R[j] 
            j += 1
        k += 1
  
    # 拷贝 L[] 的保留元素
    while i < n1: 
        arr[k] = L[i] 
        i += 1
        k += 1
  
    # 拷贝 R[] 的保留元素
    while j < n2: 
        arr[k] = R[j] 
        j += 1
        k += 1
  
def mergeSort(arr,l,r): 
    if l < r: 
  
        
        m = int((l+(r-1))/2)
  
       
        mergeSort(arr, l, m) 
        mergeSort(arr, m+1, r) 
        merge(arr, l, m, r) 
  
  
arr = [12, 11, 13, 5, 6, 7] 
n = len(arr) 
print ("给定的数组") 
for i in range(n): 
    print ("%d" %arr[i]), 
  
mergeSort(arr,0,n-1) 
print ("\n\n排序后的数组") 
for i in range(n): 
    print ("%d" %arr[i])
```

### 堆排序
堆积是一个近似完全二叉树的结构，并同时满足堆积的性质：即子结点的键值或索引总是小于（或者大于）它的父节点。堆排序可以说是一种利用堆的概念来排序的选择排序。
```
def heapify(arr, n, i): 
    largest = i  
    l = 2 * i + 1     # left = 2*i + 1 
    r = 2 * i + 2     # right = 2*i + 2 
  
    if l < n and arr[i] < arr[l]: 
        largest = l 
  
    if r < n and arr[largest] < arr[r]: 
        largest = r 
  
    if largest != i: 
        arr[i],arr[largest] = arr[largest],arr[i]  # 交换
  
        heapify(arr, n, largest) 
  
def heapSort(arr): 
    n = len(arr) 
  
    # Build a maxheap. 
    for i in range(n, -1, -1): 
        heapify(arr, n, i) 
  
    # 一个个交换元素
    for i in range(n-1, 0, -1): 
        arr[i], arr[0] = arr[0], arr[i]   # 交换
        heapify(arr, i, 0) 
  
arr = [ 12, 11, 13, 5, 6, 7] 
heapSort(arr) 
n = len(arr) 
print ("排序后") 
for i in range(n): 
    print ("%d" %arr[i])
```
### 计数排列
计数排序的核心在于将输入的数据值转化为键存储在额外开辟的数组空间中。作为一种线性时间复杂度的排序，计数排序要求输入的数据必须是有确定范围的整数。
```
def countSort(arr):
   count = [ 0 for i in range(256)]
   output = ["" for _ in arr]
   mx, mn = 0, 255
   for i in arr:
      idx = ord(i)
      if idx > mx: mx = idx
      if idx < mn: mn = idx
      count[idx] += 1
   idx = 0
   for i in range(mn, mx + 1):
      if count[i] == 0: continue
      for _ in range(count[i]):
         output[idx] = chr(i)
         idx += 1
   return output
arr = "wwwrunoobcom"
ans = countSort(arr) 
print ( "字符数组排序 %s"  %("".join(ans)) )
```
### 希尔排序
希尔排序，也称递减增量排序算法，是插入排序的一种更高效的改进版本。但希尔排序是非稳定排序算法。
希尔排序的基本思想是：先将整个待排序的记录序列分割成为若干子序列分别进行直接插入排序，待整个序列中的记录"基本有序"时，再对全体记录进行依次直接插入排序。
```
def shellSort(arr): 
  
    n = len(arr)
    gap = int(n/2)
  
    while gap > 0: 
  
        for i in range(gap,n): 
  
            temp = arr[i] 
            j = i 
            while  j >= gap and arr[j-gap] >temp: 
                arr[j] = arr[j-gap] 
                j -= gap 
            arr[j] = temp 
        gap = int(gap/2)
  
arr = [ 12, 34, 54, 2, 3] 
  
n = len(arr) 
print ("排序前:") 
for i in range(n): 
    print(arr[i]), 
  
shellSort(arr) 
  
print ("\n排序后:") 
for i in range(n): 
    print(arr[i])
```

### 拓扑排序
