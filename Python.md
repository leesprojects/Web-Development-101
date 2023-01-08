import sys

import time Used for runtime calculations

from numpy import random

import numpy as np

Visualise these https://visualgo.net/en

Documentation for each language https://www.geeksforgeeks.org/binary-search/?ref=lbp

  

### SORTING ALGORITHMS

  
```python
class StackArray:

        def createStack():

            stack = []

            return stack

  

        def isEmpty(stack):

            return len(stack) == 0

  

        def push(stack, item): #Constant time

            stack.append(item)

            print(item + " pushed to stack")

  

        def pop(stack):

            if(StackArray.isEmpty(stack)):

                return str("Null")

            return stack.pop()

  

class Queue: #Using circular array

    def __init__(self, capacity):

        self.front = self.size = 0

        self.rear = capacity - 1

        self.Q = [None]*capacity

        self.capacity = capacity

  

    def isFull(self):

        return self.size == self.capacity

  

    def EnQueue(self, item):

        if self.isFull():

            print("Full")

            return

        self.rear = (self.rear + 1) % (self.capacity)

        self.Q[self.rear] = item

        self.size = self.size + 1

        print ("% s enqueued to queue" % str(item))

  

class BubbleSort: #Runtime is O(N^2), θ(N^2)

    def bubbleSort(arr):

        n = len(arr)

        for i in range(0, n-1): #Go through all array elements

            for j in range(0, n-i-1): #Go through all array elements without already sorted

                if arr[j] > arr[j+1]:   #If J is greater than the next, then swap

                    arr[j], arr[j+1] = arr[j+1], arr[j]

        return arr

  

class SelectionSort: #Runtime is O(N^2), θ(N^2)

    def selectionSort(arr):

        n = len(arr)

  

        for i in range(0, n-1): #Go through all array elements || O(N^2)

            min_index = i

            for j in range(i+1, n-1): #Find min element in sorted array || O(N^2)

                if arr[min_index] > arr[j]:

                    min_index = j

  

        arr[i], arr[min_index] = arr[min_index], arr[i] #Swap min element found with current sorted index

        return arr

class InsertionSort:

    def insertionSort(arr):

        n = len(arr)

        for i in range(1, n):

            key = arr[i]

            j = i - 1

            while j >= 0 and key < arr[j]:

                arr[j + 1] = arr[j]

                j -= 1

            arr[j + 1] = key

        return arr

  

class QuickSort: #Python recursion limit is 1000 so it sucks

    def quickSort(arr, low, high): #Uses recursion since it calls itself using a previous value

        if low < high:             #Prevents an infinite loops

            partitionIndex = QuickSort.partition(arr, low, high)

            QuickSort.quickSort(arr, low, partitionIndex - 1)

            QuickSort.quickSort(arr, partitionIndex + 1, high)

  

        return arr

  

    def partition(arr, low, high):

        i = (low - 1)

        pivot = arr[high]

  

        for j in range(low, high):

            if arr[j] < pivot:

                i = i + 1

                arr[i], arr[j] = arr[j], arr[i]

        arr[i + 1], arr[high] = arr[high], arr[i + 1]

        return(i + 1)

  
  

class MergeSort:

    def mergeSort(arr):

        if len(arr) > 1:

            mid = len(arr) // 2 #Floor divide, remove any decimals

            L = arr[:mid] #all before mid point

            R = arr[mid:] #all after mid point

  

            # Recursive call on each half

            MergeSort.mergeSort(L)

            MergeSort.mergeSort(R)

  

            # Two iterators for traversing the two halves

            i = 0 #Left iterator

            j = 0 #Right iterator

            # Iterator for the main list

            k = 0

            while i < len(L) and j < len(R):

                if L[i] <= R[j]:

                # The value from the left half has been used

                    arr[k] = L[i]

                # Move the iterator forward

                    i += 1

                else:

                    arr[k] = L[j]

                    j += 1

                # Move to the next slot

                k += 1

  

            # For all the remaining values

            while i < len(L):

                arr[k] = L[i]

                i += 1

                k += 1

  

            while j < len(R):

                arr[k]=R[j]

                j += 1

                k += 1

  

            return arr

  

class CheckArrays:

    def checkArray(arr1, arr2, arr3, arr4, arr5):

        if (np.array_equal(arr1, arr2)) and (np.array_equal(arr3, arr4)) and (np.array_equal(arr5, arr1)) :

            print("True")

class bstNode: #Create the first node and the tree root

    def __init__(self, key):

        self.left = None

        self.right = None

        self.val = key

  

class BinarySortTree: #Given a tree, insert a node, Key is the new value

    def bstInsert(root, key):

        if root is None: #Recursion ender

            return bstNode(key)

        else: #Tree Traversal

            if root.val == key:

                return root

            elif root.val < key:

                root.right = BinarySortTree.bstInsert(root.right, key)

            else:

                root.left = BinarySortTree.bstInsert(root.left, key)

        return root

  

    def bstSearch(root, key):

        if root is None or root.val == key:

            return root

  

        if root.val < key:

            return BinarySortTree.bstSearch(root.right, key)

  

        return BinarySortTree.bstSearch(root.left, key)

  
  
  

if __name__ == "__main__":

    print("Start Program")

    start_time = time.time()

  

    #STACK CODE

    #stack = StackArray.createStack()

    #StackArray.push(stack, str("Dog"))

    #StackArray.push(stack, str("Cat"))

    #print(StackArray.pop(stack) + " from stack")

  

    #Initalise Array

    arr = [1, 5, 2, 6, 7, 2, 5, 3, 4321, 235, 2314, 135, 1523, 61, 23165, 3, 4, 234, 2362, 324, 42365, 23423, 523]

    arr_Rand = random.randint(10000, size=(1000))

    arr_Bubble = arr_Rand

    arr_Selection = arr_Rand

    arr_Insertion = arr_Rand

    arr_Quick = arr_Rand

    arr_Merge = arr_Rand

    #print(arr, "\n", arr_Bubble, "\n", arr_Selection, "\n", arr_Insertion, "\n", arr_Quick)

  

    #BUBBLESORT CODE

    startTime_Bubble = time.time()

    arr_BubbleSorted = BubbleSort.bubbleSort(arr_Bubble)

    runTime_Bubble = time.time() - startTime_Bubble

    print("\nBubble Sorted Results\n", arr_BubbleSorted, "\nRuntime: ", runTime_Bubble)

  

    #SELECTION SORT

    startTime_Selection = time.time()

    arr_SelectionSorted = SelectionSort.selectionSort(arr_Selection)

    runTime_Selection = time.time() - startTime_Selection

    print("\nSelection Sorted Results\n", arr_SelectionSorted, "\nRuntime: ", runTime_Selection)

  

    #INSERTION SORT

    startTime_Insertion = time.time()

    arr_InsertionSorted = InsertionSort.insertionSort(arr_Insertion)

    runTime_Insertion = time.time() - startTime_Insertion

    print("\nInsertion Sorted Results\n", arr_InsertionSorted, "\nRuntime: ", runTime_Insertion)

  

    #QUICK SORT

    startTime_QuickSort = time.time()

    arr_QuickSorted = QuickSort.quickSort(arr_Quick, 0, len(arr_Quick) - 1)

    runTime_Quick = time.time() - startTime_QuickSort

    print("\nQuick Sorted Results\n", arr_QuickSorted, "\nRuntime: ", runTime_Quick)

  

    #MERGE SORT

    startTime_MergeSort = time.time()

    arr_MergeSorted = MergeSort.mergeSort(arr_Merge)

    runTime_Merge = time.time() - startTime_MergeSort

    print("\Merge Sorted Results\n", arr_MergeSorted, "\nRuntime: ", runTime_Merge)

    print("\nBubbleSorted Runtime: ", runTime_Bubble, "\nSelectionSorted Runtime: ", runTime_Selection, "\nInsertionSorted Runtime: ", runTime_Insertion)

    print("QuickSorted Runtime: ", runTime_Quick, "\nMergeSorted Runtime: ", runTime_Merge)

    CheckArrays.checkArray(arr_BubbleSorted, arr_SelectionSorted, arr_InsertionSorted, arr_QuickSorted, arr_MergeSorted)

  

    print("\nBinary Sort Tree")

    r = bstNode(45) #Create tree with node

    r = BinarySortTree.bstInsert(r, 35) #Create new node in existing tree r

    r = BinarySortTree.bstInsert(r, 18)

    r = BinarySortTree.bstInsert(r, 402)

    r = BinarySortTree.bstInsert(r, 3)

  

    r = BinarySortTree.bstSearch(r, 18)

    print(r)
```

