# Algo-Ds
Understanding algorithms and data structures 

# SEARCHING

## BINARY SEARCH
Searching is one of the humane things we do in our daily life, Fortunately, we are evolved species and we sort of have an idea how to efficiently do things [by things I mean "Searching" for the sake of this topic]. 
For example:
* To look for a word in a dictionary, You don't just start going through each word until you find the word you are looking for.
  In fact, the dictionary is designed in a specific way so that we can find the word we are looking for fast-ly and efficiently.
  * Ya, you guessed it right, the dictionary is sort of a Data Structure [Not just data!, It is Structured in a specific way to help us implement an algorithm to find the word we are looking for].
* So, now you know that the words in the dictionary are *sorted*, so by this, you figure out where the word would be in the dictionary.
* Hopefully, you will approximate the word to be present in any one half of the dictionary ie.. you pull up the dictionary from the middle[approx.] and then decide if you should search in the first half or the second half.
* And you repeat the above process until you find the word.

_Guess what? 
You just did a Binary Search_.

So, now you know what binary search is, All we have to do is just tell it to a computer:smiley:.

#### But How?
Let's understand with a simple example, Given is an array of integers and a target integer. We have to find out if the target integer is present in the array using Binary Search [Cause it's efficient] and return the index if present or else return -1.

Let's lay out the process in simple english to understand:smiley:.
>Let's assume a function which receives an array along with target to be searched for.
>* So, as a normal human would do, we need to find the half of the array
>* Now, after finding the element inside the position we need to compare the value with target.
>   * if the value is less, we eliminate the second half of the array and repeat the process for the first half.
>   * if the value is greater, we eliminate the first half of array and repeat the process for second half of the array.
>   * if the value is equal to the target, We found the required index:smiley:.
>* finally you will reach a position where value matches the target.
>* If you don't and no more values to compare, then that value is not present.

Below is the implementation in Python:

````python
def BinarySearch(array , target):
# we will pass 0 by default to place a pointer at the start of index and call it left
# we will pass the last index of the array and call it right.
 return BinarySearchHelper(array , target , 0 , len(array)-1)
 
def BinarySearchHelper(array , target , left , right):
# use a while loop to know if the value is present or not [if left not greater than right then the value might be present in the array].
  while left <= right:
      # calculate the middle point of the array
    	middlePointer = (left + right)//2
      # get the value in the middlePointer position and store in a variable
    	potentialMatch = array[middlePointer]
      # Compare the value with the target
    	if potentialMatch == target:
      		return middlePointer
      # check if the value is in first half of array or the second half and adjust the left or right pointers accordingly to eliminate the unnecessary half.
    	elif target < potentialMatch:
      		right = middlePointer - 1
    	else:
      		left = middlePointer + 1
  return -1;
````

## SEARCH 3 LARGEST NUMBERS IN AN ARRAY
If you thought you could just sort the array and pick the largest last 3 indexes, you are right. But, we need not sort the entire array just to get 3 elements.

#### Cool, But how to do that?
Simple, just pick each element from given array and put the element in an array of size 3 [let's name this array as threeLargest] while comparing that element with value in 2,1,0 indexes of the threeLargest array.
* if the element is greater replace and shift the other values.
* if not, then we dont care about that value.
Finally, after iterating through all values of array, we will end up with an array of 3 largest numbers:smiley:.

````python
def findThreeLargestNumbers(array):
	threeLargestArray = [None,None,None]
	for num in array:
		updateThreeLargest(threeLargestArray,num)
	return threeLargestArray

def updateThreeLargest(threeLargestArray , num):
	if threeLargestArray[2] is None or num > threeLargestArray[2]:
		shiftAndUpdate(threeLargestArray , num , 2) 
	elif threeLargestArray[1] is None or num > threeLargestArray[1]:
		shiftAndUpdate(threeLargestArray , num , 1) 
	elif threeLargestArray[0] is None or num > threeLargestArray[0]:
		shiftAndUpdate(threeLargestArray , num , 0) 
		
def shiftAndUpdate(array , num , index):
	for i in range (index+1):
		if i == index:
			array[i] = num
		else:
			array[i] = array[i+1]
````


## SEARCH FOR A NUMBER IN A 2D MATRIX
Given a 2d matrix where all the rows and columns are sorted and a target number, we need to find if the target is present in the matrix or not. If the target is present then we need to return the co-ordinates and an array of -1,-1 if not.
Note: the matrix doesn't necessarily have equal rows and columns.

let' take a look at the matrix:
> [1,4,7,12,15,1000]  
> [2,5,19,31,32,1001]  
> [3,8,24,33,35,1002]  
> [40,41,42,43,45,1003]  
> [99,100,103,106,128,1004]   
>  TARGET : 44

So, Obviously iterating through all the elements is not the way to go. What we can do is use the concept of Binary Search [Rows and Columns are sorted, Remember?] and keep eliminating the un-necessary values.

If you think about it what we can do is start at 1000 and compare with 44.
* Since, it's a sorted matrix and 44 is less than 1000, we need not iterate through last column.
* Now, we are at 15. So, since 15 is less than 44, we need not iterate further in that row and move to next row.

Below is the implementation of python:

````python
def searchInSortedMatrix(matrix, target): 
	row = 0
	col = len(matrix[0]) - 1
	
	while row < len(matrix) and col >= 0:
		if matrix[row][col] > target:
			col = col - 1
		elif matrix[row][col] < target:
			row = row + 1
		else:
			return [row,col]
	return [-1,-1]
	

````

## SHIFTED BINARY SEARCH
Similar to binary search, but as the name suggests, it's shifted.
let's assume an array -> [45,61,71,72,73,0,1,21,33,45] and target = 33
* So, first as usual consider the middle pointer.
	* left = 0 , right = len(array) - 1 , middlePointer is 4 in this case.
* now , we need to try eliminating a half of an array.
* compare 73 with 45, since 45 is less than 73, we can assume that the target is in the left part of the array but we also need to 		compare the target with 45 to confirm if the target is in this half of the array.
	* Since, target < 45 it's not in this part of the array.
* then we can go ahead and ignore 1st half of array and binary search on the 2nd half of the array.
* repeat the process until the left pointer is <= right pointer:smiley:.

Implementation in python:

````python
def shiftedBinarySearch(array,target):
	return shiftedbinarysearchhelper(array , target , 0 , len(array) - 1)
	
def shiftedbinarysearchhelper(array , target , left , right):
	while left <= right:
		middle = (left + right) // 2
		potentialMatch = array[middle]
		leftNum = array[left]
		rightNum = array[right]
		
		if potentialMatch == target:
			return middle
		
		if leftNum <= potentialMatch:
			if target < potentialMatch and target >= leftNum:
				right = middle - 1
			else:
				left = middle + 1
		else:
			if target > potentialMatch and target <= rightNum:
				left = middle + 1
			else:
				right = middle -1
	return -1
````


## SEARCH FOR RANGE
Just like searching for a target in a sorted array using binary search, we now need to handle an array which is also sorted but has duplicate target numbers.
Let's assume the below scenario:
> [0,1,22,33,45,45,45,45,45,80,61,54,87,90]    
> Target : 45;

So, how to solve the above?

> * Simple just follow binary search but we need to check if other indexes contain the target element.
> * and also check if the target elements are extreme indices in the array.

Implementation in python:

````python
def searchForRange(array, target):
	finalRange = [-1,-1]
	getTheRange(array , target , 0 , len(array) - 1 , finalRange , True)
	getTheRange(array , target , 0 , len(array) - 1 , finalRange , False)
	return finalRange
	
def getTheRange(array , target , left , right , finalRange , goLeft):
	while left <= right:
		while left <= right:
			middle = (left + right) // 2
		
			if target < array[middle]:
				right = middle - 1
			elif target > array[middle]:
				left = middle + 1
			else:
				if goLeft:
					if middle == 0 or array[middle - 1] != target:
						finalRange[0] = middle
						return 
					else:
						right = middle - 1
				else:
					if middle == len(array) - 1 or array[middle + 1] != target:
						finalRange[1] = middle
						return
					else:
						left = middle + 1	
````



# SORTING
Sorting elements in a datastructure is very important operation which is vital in any software workings.

## BUBBLE SORT
In this sorting algorithm the intention is to finally sort the array by swapping two elements if they are not in ascending order while iterating through the array until the entire array is sorted.

> Let's assume an array:
> [8,5,2,9,5,6,3]
> The output should be a sorted array -> [2,3,5,5,6,8,9]

Steps to be followed:

> * Declare a Boolean value and set it to false.
> * using a for loop, iterate through the array.
> * while 2 elements are not in ascending order , Swap them.
> * and finally we need to check if we have reached a iteration where we haven't swapped any elements which means the array is sorted, for that consider changing the Boolean to false at if.

Implementation in Python:

````python
def BubbleSort(array):
	isSorted = False
	while not isSorted:
		isSorted = True
		for i in range (len(array) - 1):
			if array[i] > array[i+1]:
				array[i],array[i+1] = array[i+1] , array[i]
				isSorted = False
	return array
````

This Tenchnique can be further improved by making changes to the function by which we can stop the iteration of the array until the greatest element of the array.

````python
def BubbleSort(array):
	isSorted = False
	counter = 0;
	while not isSorted:
		isSorted = True
		for i in range ((len(array) - 1) - counter):
			if array[i] > array[i+1]:
				array[i],array[i+1] = array[i+1] , array[i]
				isSorted = False
		counter +=1
	return array
````

## INSERTION SORT
This algorithm is not the best of the lot but is pretty much straightforward.
Let's assume an array [8,5,2,9,5,6,3]
The steps to follow to sort the array using insertion sort:

> * Iterate through the array using a for loop
> * Compare the later element with current element
> 	* If current element is greater than later element, swap them.
	* While the above is true, continue to compare with previous elements until you reach 0.
> * Repeat until you complete 1 iteration.

Implementing with the example:

````
Compare 5 with 8 : Since, 8 > 5 , Swap them
Now the array is as Follows : [5,8,2,9,5,6,3].

Compare 2 with 8 : Since, 8 > 2 , Swap them
Now the array is as Follows : [5,2,8,9,5,6,3].

Remember? Repeat until you reach 0th index.

So, Compare 2 with 5 , Since 5 > 2 , Swap them
Now the array is as Follows : [2,5,8,9,5,6,3].

You get the GIST right!
````

Voila! Now you have a sorted array.

Implementation in python : 

````python
def insertionSort(array):
	for i in range(1 , len(array)):
		j = i
		while j > 0 and array[j] < array[j-1]:
			swap(array , j , j-1)
			j -= 1 # Reducing j by 1 so that the while loop runs until j hits 0 
	return array
	
def swap(array , i , j):
	array[i] , array[j] = array[j] , array[i]
````

## SELECTION SORT
As the name suggests the algorithm is about selecting an element from the array and finding other element which is lesser and swap with the selected element, Eventually, the entire array gets sorted.

Let's assume an array -> [8,5,2,9,5,6,3]

Steps to sort the array using Selection sort:

> * select 8 [use a pointer for it]
> * compare with other elements, since 8 > 5 swap them
> * Resulting array -> [5,8,2,9,5,6,3]
> * compare 5 with 2 -> Swap
> * Resulting array: [2,8,5,9,5,6,3]
> * similarly after 1 iteration increase the pointer and repeat the process.

Finally, the array is sorted after n^2 iteration at the best case.

Implementation in python:

````python
def selectionSort(array):
    currentIndex = 0
	print(len(array))
	while currentIndex <= len(array) - 1:
		smallestIndex = currentIndex
		for i in range (currentIndex + 1 , len(array)):
			if array[smallestIndex] > array[i]:
					smallestIndex = i
		swap(array , smallestIndex , currentIndex)
		currentIndex += 1
	return array

def swap(array , i , j):
	array[i] , array[j] = array[j] , array[i]
````

