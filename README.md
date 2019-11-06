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
