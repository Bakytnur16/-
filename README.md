# Basic algorithm

## Search

### binary search algorithm
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
    print('The index of the element in the array is %d' % result)
else:
    print('The element is not in the array')
```
### linear search algorithm

## Sort
### Insertion Sort
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
print('Sorted array：')
for i in range(len(arr)):
    print('%d' %arr[i])
```
## Quicksort 
Divide and conquer divides a sequence (list) into 2 smaller and larger sub-sequences, and then recursively sorts the two sub-sequences. 
 Select the benchmark value pivot
 split
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

#arr[] --> Sort array
# low  --> Starting index
# high  --> End index

def quickSort(arr, low, high):
    if low < high:
        pi = partition(arr, low, high)

        quickSort(arr, low, pi - 1)
        quickSort(arr, pi + 1, high)


arr = [10, 7, 8, 9, 1, 5]
n = len(arr)
quickSort(arr, 0, n - 1)
print("Sorted array:")
for i in range(n):
    print("%d" % arr[i])
```
### Selection sort
First find the smallest (large) element in the unsorted sequence, store it at the beginning of the sorted sequence, and then continue to find the smallest (large) element from the remaining unsorted elements, and then put it at the end of the sorted sequence.
```
import sys

A = [64, 25, 12, 22, 11]

for i in range(len(A)):

    min_idx = i
    for j in range(i + 1, len(A)):
        if A[min_idx] > A[j]:
            min_idx = j

    A[i], A[min_idx] = A[min_idx], A[i]

print("Sorted array：")
for i in range(len(A)):
    print("%d" % A[i])
```
### Bubble Sort
It repeatedly visits the sequence to be sorted, compares two elements at a time, and swaps them if their order is wrong.
```
def bubbleSort(arr):
    n = len(arr)

    # Traverse all array elements
    for i in range(n):

        # Last i elements are already in place
        for j in range(0, n - i - 1):

            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]


arr = [64, 34, 25, 12, 22, 11, 90]

bubbleSort(arr)

print("Sorted array:")
for i in range(len(arr)):
    print("%d" % arr[i])
```
### Merge sort
```
def merge(arr, l, m, r): 
    n1 = m - l + 1
    n2 = r- m 
  
    # Create a temporary array
    L = [0] * (n1)
    R = [0] * (n2)
  
    # Copy data to temporary array L[] 和 R[] 
    for i in range(0 , n1): 
        L[i] = arr[l + i] 
  
    for j in range(0 , n2): 
        R[j] = arr[m + 1 + j] 
  
# Merge temporary arrays into arr[l. . r] 
     i= 0# Initialize the index of the first subarray
     j= 0# Initialize the index of the second subarray
     k = l# Index of the initial merged subarray
  
    while i < n1 and j < n2 : 
        if L[i] <= R[j]: 
            arr[k] = L[i] 
            i += 1
        else: 
            arr[k] = R[j] 
            j += 1
        k += 1
  
# Copy the reserved element of L[]
    while i < n1: 
        arr[k] = L[i] 
        i += 1
        k += 1
  
# Copy the reserved element of R[]
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
print ("Given array") 
for i in range(n): 
    print ("%d" %arr[i]), 
  
mergeSort(arr,0,n-1) 
print ("\n\nSorted array") 
for i in range(n): 
    print ("%d" %arr[i])
```

### Heapsort
Stacking is a structure that approximates a complete binary tree, and at the same time satisfies the nature of stacking: that is, the key value or index of a child node is always less than (or greater than) its parent node. Heap sorting can be said to be a kind of selection sorting that uses the concept of heap to sort.
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
        arr[i],arr[largest] = arr[largest],arr[i]  # exchange
  
        heapify(arr, n, largest) 
  
def heapSort(arr): 
    n = len(arr) 
  
    # Build a maxheap. 
    for i in range(n, -1, -1): 
        heapify(arr, n, i) 
  
    # Exchange elements one by one
    for i in range(n-1, 0, -1): 
        arr[i], arr[0] = arr[0], arr[i]   # exchange
        heapify(arr, i, 0) 
  
arr = [ 12, 11, 13, 5, 6, 7] 
heapSort(arr) 
n = len(arr) 
print ("After sort") 
for i in range(n): 
    print ("%d" %arr[i])
```
### Counting sort
The core of counting sorting is to convert the input data values into keys and store them in the extra array space opened up. As a kind of linear time complexity sorting, counting sorting requires that the input data must be an integer with a certain range.
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
print ( "Character array sorting %s"  %("".join(ans)) )
```
### Shellsort
Hill sorting, also known as decreasing and incremental sorting algorithm, is a more efficient and improved version of insertion sorting. However, Hill sorting is an unstable sorting algorithm. 
 The basic idea of Hill sorting is: first divide the entire sequence of records to be sorted into several sub-sequences for direct insertion sorting, and when the records in the entire sequence are "basically ordered", all records will be directly inserted and sorted in turn.
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
print ("Before sorting:") 
for i in range(n): 
    print(arr[i]), 
  
shellSort(arr) 
  
print ("\nAfter sorting:") 
for i in range(n): 
    print(arr[i])
```

### Topological sorting
