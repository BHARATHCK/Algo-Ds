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
