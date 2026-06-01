# DSA Major tips

🧠 1. “Understand → Then Solve → Then Struggle”

⏱️ 2. Minimum Daily Output Rule

🔁 3. Revision is Mandatory (not optional)

🧩 4. Pattern Recognition > Number of Problems

✍️ 5. Maintain a DSA Notebook (very important)

⚔️ 6. One Topic at a Time (No Chaos)

🧱 7. Build Strong Basics (don’t rush ahead)

🔥 8. Re-solve Problems (this is where growth happens)

🚫 9. Limit Solution Watching

📈 10. Track Your Progress Weekly

**⚖️ 11. Balance ML Smartly (important for you)**

🧠 12. Learn to Sit With Discomfort

# Sorting

| Algorithm | Key Idea | Important Code Section 🔑 | Best Case TC | Average TC | Worst Case TC | Stable? | Swaps |
| --- | --- | --- | --- | --- | --- | --- | --- |
| **Selection Sort** | Pick minimum and place at correct position | Finding `min_index` in inner loop | O(n²) | O(n²) | O(n²) | ❌ No | Minimum (n-1) |
| **Bubble Sort** | Repeatedly swap adjacent elements | Adjacent comparison  | O(n) *(optimized)* | O(n²) | O(n²) | ✅ Yes | Many |
| **Insertion Sort** | Insert element in sorted left part | Shifting elements  | O(n) | O(n²) | O(n²) | ✅ Yes | Few (shifts instead) |

```python
#pick one min element place it at the right postion
def selection_sort(arr,n):
    for i in range(0 , n - 1):
        min = i
        for j in range(i + 1, n):
            if(arr[j] < arr[min]):
                min = j
        arr[i],arr[min] = arr[min],arr[i]
    return arr

#pick max element place it at the last
#sort in asceding order
def bubble_sort(arr,n):
    for i in range(0 , n - 1):
        for j in range(0 , n - i - 1):
            if(arr[j] > arr[j+1]):
                arr[j],arr[j+1] = arr[j+1],arr[j]
    return arr
    
#sort in desecnding order
def bubble_sort(nums: list[int]) -> list[int]:
    for i in range(0 , len(nums)):
        for j in range(0 , len(nums) - i - 1):
            if nums[j + 1] > nums[j]:
                nums[j + 1],nums[j] = nums[j],nums[j + 1]
    
    return nums

#pick one element at a time and place it at the right position 
def insertion_sort(arr, n):
    for i in range(0 ,n):
        j = i
        while(j > 0 and arr[j-1] > arr[j]):
            arr[j],arr[j-1] = arr[j-1],arr[j]
            j-=1
    return arr
```

## Merge Sort ( Divide and Conquer )

Takes an array divide into two parts until its has became as one single element array and then when it backtracks it uses merge function to merge the sorted part of the array and when the process of backtracking completes the array is completely sorted 

S.C : O(N)

T.C : O(NlogN)

!image.png

!image.png

```python
def merge(arr,low,mid,high):
    temp = []
    left = low 
    right = mid + 1

    while(left <= mid and right <= high):
        if(arr[left] <= arr[right]):
            temp.append(arr[left])
            left += 1
        else:
            temp.append(arr[right])
            right += 1
    #write back the original left subarray    
    while(left <= mid):
        temp.append(arr[left])
        left += 1
    
    #write back the original right subarray    
    while(right <= high):
        temp.append(arr[right])
        right += 1
    
    #this is done because temp will always starts from 0 however 
    #the orignal array indices might be different
    for i in range(low , high + 1):
        arr[i] = temp[i - low]
    
    return arr

def merge_sort(arr,low,high):
    if(low >= high):
        return
    mid = (low + high) // 2
    merge_sort(arr,low,mid)
    merge_sort(arr,mid+1,high)
    merge(arr,low,mid,high)
```

!image.png

## Quick Sort ( Divide and Conquer )

Pick a pivot element and place it on the correct side . in ascending order the smaller elements than pivot will be on left while the larger ones will be on right

S.C : O(1)

T.C : O(NlogN) ( Best / Average Case )

T.C : O(N^2)

```python
class Solution:

    # -------------------- PARTITION FUNCTION --------------------
    def partition(self, nums, low, high):
        # Choose the first element as pivot
        pivot = nums[low]

        # i starts from left, j starts from right
        i = low
        j = high

        # Traverse until both pointers cross
        while i < j:

            # Move i to the right:
            # - skip elements already <= pivot (correct side)
            # - stop before going out of bounds
            while nums[i] <= pivot and i <= high - 1:
                i += 1

            # Move j to the left:
            # - skip elements already > pivot (correct side)
            # - stop before going out of bounds
            while nums[j] > pivot and j >= low + 1:
                j -= 1

            # If i and j have not crossed, we found misplaced elements:
            # nums[i] is > pivot (wrong side)
            # nums[j] is <= pivot (wrong side)
            # → swap them
            if i < j:
                nums[i], nums[j] = nums[j], nums[i]

        # Now j is the correct position for pivot:
        # place pivot there by swapping with nums[low]
        nums[low], nums[j] = nums[j], nums[low]

        # return pivot index
        return j

    # -------------------- RECURSIVE QUICK SORT --------------------
    def quickSortHelper(self, nums, low, high):

        # Base case: if the subarray has 0 or 1 element → already sorted
        if low < high:

            # Partition the array and get pivot index
            p_index = self.partition(nums, low, high)

            # Recursively sort left part (elements <= pivot)
            self.quickSortHelper(nums, low, p_index - 1)

            # Recursively sort right part (elements > pivot)
            self.quickSortHelper(nums, p_index + 1, high)

    # -------------------- MAIN FUNCTION --------------------
    def quickSort(self, nums):

        # Start quicksort on full array
        self.quickSortHelper(nums, 0, len(nums) - 1)

        return nums
```

## Fundamental Problems

### Linear Search

Traverse the whole array until finding the index else - 1

T.C : O(N)

S.C : O(1)

### largest element

Traverse the whole array until the largest element is found. 

T.C : O(N)

S.C : O(1)

### Second Largest Element

The idea is to assign negative float values to the both the variables and iterate through the whole array . if any element found greater than the current largest element than assign it . Additionally if the largest element is getting a larger value that means the prior larger values might be second largest value .

Similarly if the value is less than current larger element and it is higher than second largest element but its not the same value as the largest than the second largest element can be assigned to that value

T.C : O(N)

S.C : O(1)

### Left rotate array by d places

when the value of d is equal than the size of the array then we will be getting the same array , in addition to value of d the no of change that will be required for changing the array will be Total_Rotation = d % len(nums) 

Use a for loop , and call the function which will be responsible for rotating the array by 1 element at a time 

T.C : O(N)

SC : O(N*K)

Based on observation

T.C : O(2N)

SC : O(1)

!image.png

## Logic Building problem

### Move zeroes to end

The idea of mine was simple if a  zero element is found traverse the whole array after it and then replace with the current 0th position 

T.C : O(N^2)

SC : O(N)

Append all the non zero elements in a new array and fill the remaining ones with zeroes

T.C : O(N)

S.C : O(N)

Find a zeroth element and then run an another loop and find another non zero element and swap the zeroth element with it and move j ahead`

T.C : O(N)

S.C : O(1)

### **Remove duplicates from sorted array**

Create a new array and append all the distinct element in it . in the end copy all the elements back to main array and the length of the new array will be our no of unique element 

T.C : O(n)

S.C : O(n)

If the adjacent element is equal, move ahead. If it is greater, swap it, or assign the current arr[i] value to the j + 1 position. Why j + 1? Because j + 1 ensures the element is updated starting from the second repeated appearance of the previous element.

T.C : O(N)

S.C : O(1)

Same ideas as mine but more clear code 

T.C : O(N)

S.C : O(1)

### **Find union of two sorted Arrays**

Compare two elements by picking one from each array. Three cases can arise:

1. if arr1[i] < arr2[j] → append arr1[i] (the smaller element). Since the union should not contain duplicates, use the “Appending_element” variable to avoid adding the same value twice.
2. if arr1[i] == arr2[j] → append either element, update the variable, and increment both ‘i’ and ‘j’.
3. if arr1[i] > arr2[j] → append arr2[j] and increment j.

Lastly, if one array is exhausted early, append the remaining elements from the other array to the final array.

T.C : O(min(n,m)) + O(N) + O(M)

S.C : O(n)

In order to avoid the use “Appending_element” union_array[-1] can be used as well 

### **Find Intersection of two sorted Arrays**

Intersecting array should only contain those elements which are common to either of the arrays and the remaining conditions will be same as the union array solution

T.C : O(N)

SC : O(N)

## FAQ’s (Medium)

### Majority Element

Use a dictionary to store the count of each element and then iterate over the dictionary and check the if the occurence > len(arr) // 2 and if all the elements are having single occurence return -1 

T.C : O(N)

S.C : O(N)

#### Booye Moore’s Voting Algorithm

The algorithm states that if the element in an array is in majority then it’s occurrence wont be cancelled out by every other elements then itself . 

How it works?

we take a initial element and then count its occurrence by traversing the array . if an element comes which is not our initial element then we decrease the count .

if count == 0 it means in a given sub array there was no majority element **why ?** because if count is getting 0 , then the element that we chose has been cancelled out by other elements that means that our initial element wasn’t our majority element .

Then we take another element and take count as 1 again **why ?** because initial count of every element is 1 .

However the algorithm might give use a potential element but we need to verify on our own with another array traversal 

T.C : O(N)

S.C : O(N)

### Leaders in an Array

Start iterating the array from right to left and find the greatest element , as soon as the value of Greatest_element will change append it in the new array 

Final result will be reverse of temp array 

T.C : O(n)

S.C : O(n)

### Rearrange array elements sign by sign

Create two arrays one to store +ve numbers and one for -ve numbers . change the final array by adding +ve and -ve numbers alternatively 

T.C : O(n) + O(n)

S.C : O(n/2) + O(n/2)

Use a auxiliary list and since as per the question positive will come first then negative so we have to make sure that in a new array even indices will be occupied by positive while odd indices be occupied by negative indices

T.C :  O(n)

S.C. : O(n)

### Pascal Triangle

#### Pascal Triangle - 1

(Find the element at Rth row and Cth column )

using **combinations (nCr)** to directly compute a value in Pascal’s Triangle instead of building the whole triangle.
****

T.C : O(r)

S.C : O(1)

#### Pascal Triangle - 2

(Find all the pascal element by the given row )

The idea is to calculate the ncr helper function for each of the element of the row 

T.C : O(r^2)

S.C : O(r)

it can be seen that any element in the rth row is of the form:

curr = (prev * (r-i))/(i) where prev is the previous element in the row and i is the index of the element in the row. Using this formula, we can generate the rth row of Pascal's triangle in O(n) time complexity.

T.C : O(r)

S.C : O(r)

#### Pascal Triangle - 3

( Print the whole pascal triangle till the given row )

use the pascal row generator to generate the triangle row by row instead of using NCR to calculate each element

T.C : O(n^2)

S.C : O(N^2)

### Rotate matrix by 90 degrees ( Square Matrix )

Transpose the whole matrix and reverse each row of the matrix 

T.C : O(N^2)

S.C : O(1)

### Two Sum

Look for all possible pairs and return the indices of the both the elements that sum up to target 

T.C : O(n^2)

S.C : O(1)

Use a hashmap and look for the element that makes the target by summing up to the current element , if found then return to the indices if not store the current element along with indices

We are using the same approach as brute however since element can be found in O(1) time in hashmap , so its a better approach then the previous one 

T.C : O(n)

S.C : O(n)

Sort the array and then move the pointer as per the nature of the sum and then look for the indices in the original array 

T.C : O(nlogn)

S.C : O(nlogn)

### Three Sum

Checks all possible triplets and return the whole array comprising of all the triplets

T.C : O(n^3)

S.C : O(n^2)

Use the two sum approach here fix one element in the array and for the remaining part of the array use the 2 sum approach 

T.C : O(n^2)

S.C : O(n^2)

### Four Sum

In brute force check all the possible quadruplets and store them in a set in order to avoid any duplicates 

T.C : O(n^4)

S.C : O(Q) where Q is the number of unique quadruplets

In better approach fix ‘i’ and ‘j’ and and make the k moving and in between j and k add all the elements in a set so as to avoid any duplicate element . in short to find quadruplets for each (i,j) pair , k will be moving and for the fourth element we will be using hashing to avoid the use of another loop 

T.C : O(n^3)

S.C : O(n) + O(q)

In efficient approach we will be using the idea of 2 sum , we will be fixing i and j and then k and l will be used to find a new target which will be

$$
newtarget = target - nums[i] - nums[j]
$$

in order to avoid any duplicates the following if conditions are used for i and j 

T.C : O(n^3)

S.C : O(Q)

### Sort an array with 0’s , 1’s and 2’s

The brute force solution is to just sort the array

T.C : O(nlogn)

S.C : O(1)

Run 3 loops for storing 0 , 1 and 2 in the new_array and since the question ask in-place changes so copy the whole temp array into new array 

T.C : O(4N)

S.C : O(N)

#### Dutch National Flag Algorithm

The idea behind this algo is that we will be using three pointers in order to solve the problem 

[ 0 → low - 1 ] will contain the sorted 0’s

[ low → mid - 1 ] will contain the sorted 1’s

[ mid → high ] will contain unsorted 0’s,1’s,2’s

[ high + 1 → n - 1 ] will contain the sorted 2’s

Approach 

Initialize low = 0 , mid = 0 and high = n - 1 why ? because might be the whole array is unsorted , now mid can have 3 elements 

Case 1 : arr[mid] == 0

if we have 0 then we must swap it with low because the elements left to the low are 0’s and then we will increment the low and mid 

Case 2 : arr[mid] == 1

if we have 1 we dont have to do anything why ? because 1 lies on the middle part of the array , just increment the mid 

Case 3 : arr[mid] == 2

if we have 2 swap it with high and then decrement the high why ? because the element at high still lies in the unknown zone so we are not sure if mid can be incremented or not

### Maximum Subarray Sum

The idea is to find the sum of every sub array and then see if its greater than the max sum or not

T.C : O(n^3)

S.C : O(1)

The idea is instead of calculating sum of a subarray seprately causing another loop we can add one element one by one and check if we are getting max sum or not 

T.C : O(n^2)

S.C : O(1)

#### Kadane Algorithm

The idea is to iterate the array only once and keep track of the nature of the sum . The sum can either be +ve or -ve so the algorithm helps in both the cases as 

1. Case - 1 :
if sum < 0  → then make the whole sum value as 0 this is because if sum will be -ve it can be lethal to check the overall maximum sum so make it as 0
2. Case - 2 :                                                                                                                  If sum > 0 keep adding the elements because even +1 can help us in finding the maximum sum

T.C : O(n)

S.C : O(1)

#### Follow Up Question

It can be asked to return that subarray as well 

The idea is when we analyzed kadane algo and if the sum was getting -ve we were converting it to 0 and starting it from ahead now we can do the same thing here also 

however just in case we should also check if the current -ve sum is larger in the whole subarray 

T.C : O(n)

S.C : O(1)

## Hard problems

### Majority Element - 2

for better solution keep track of each element and then check if the occurence of that element is greater than floor[n  / 3] and simpy return the array consisting of it 

T.C : O(N)

S.C : O(N)

Use the same booye more algorithm but refined in a certain way in order to calculate the remaining majority elements 

T.C : O(N)

S.C : O(1)

Note : The order of the conditional statement is neccessary for the algorithm to run properly 

### Repeating and Missing Number

Ill be using hash map to store the frequency of a number and since as per the question it is specified that all element appear once so the repeating element will be having more than occurence and that we can detect using hash map 

Similarly we can use the same hash map to find the missing element as well

T.C : O(N)

S.C : O(N)

in this we are using two pointer approach in order to look for the same element however the missing element can be calculated from the formula

$$
 missing_element = total sum - (sum_of_array - repeating_element) 
$$

T.C : O(Nlogn)

S.C : O(1)

### Count Inversions

# Binary Search

## Fundamentals

### Binary Search

This algorithm find the element in O(logn) complexity as compared to linear Search having O(n) . The low time complexity arises due safe elimination of the search space . However binary search is only applicable when the array is sorted

The algorithm use three pointers - low ,mid and high . where mid is responsible for checking the elements. 

$$
mid = (low + high)//2
$$

if arr[mid] == target we simply return the index however if > target that means the element lies in the left side of the array . Additionally if < target that means the element lies in the right side of the array 

T.C : O(logn)

S.C : O(1)

### Lower Bound

Lower bound means an element which is minimal greater or equal to the given element 

Same code as binary search but with slight change in the element finding condition 

T.C : O(logn)

S.C : O(1)

### Upper Bound

Lower bound means an element which is minimal greater than the given element 

Same code as binary search but with slight change in the element finding condition 

T.C : O(logn)

S.C : O(1)

## Logic Building

### Search for insert Position

Same as solving the lower bound question 

T.C : O(logn)

S.C : O(1)

```python
class Solution:
    def linearSearch(self, nums, target):
        for i in range(0,len(nums)):
            if(nums[i] == target):
                return i
            
        return -1
        
        
        
        
        
        
```

```python
class Solution:
    def largestElement(self, nums):
        largestElement = float('-inf')
        for num in nums:
            if num > largestElement:
                largestElement = num
        return largestElement
        
```

```python
class Solution:
    def secondLargestElement(self, nums):
        if len(nums) < 2:
            return -1

        largest_ele = float("-inf")
        second_largest_ele = float("-inf")

        for i in nums:
            if i > largest_ele:
                second_largest_ele = largest_ele
                largest_ele = i
            else:
                if i > second_largest_ele and i != largest_ele:
                    second_largest_ele = i

        if second_largest_ele == float('-inf'):
            return -1
        
        return second_largest_ele
```

```python
class Solution:
    def rotate(self,nums):
        first_ele = nums[0]
        for i in range(1,len(nums)):
            nums[i - 1] = nums[i]
        nums[len(nums) - 1] = first_ele

    def rotateArray(self, nums, k: int) -> None:
        total_rotations = k % len(nums)

        for i in range(total_rotations):
            self.rotate(nums)
    
        return nums
```

```python
def rotate_array(arr,low,high):
    while low <= high:
        arr[low],arr[high] = arr[high],arr[low]
        low += 1
        high -= 1
    

def rotate_array_efficient_solution(arr,k,n):
    total_rotations = k % n
    rotate_array(arr,0,total_rotations - 1)
    rotate_array(arr,total_rotations , n - 1)
    rotate_array(arr,0,n - 1)
    
    return arr
```

```python
def move_zeroes_to_end_my_brute_force(arr,n):
    for i in range(1,n - 1):
        if(arr[i] != 0):
            continue
        else:
            for j in range(i + 1 , n):
                if arr[j] == 0:
                    continue
                else:
                    arr[i],arr[j] = arr[j],arr[i]
```

```python
def move_zeroes_to_end_sir_brute_force(arr,n):
    temp =[]
    for i in range(0 , n):
        if(arr[i] != 0):
            temp.append(arr[i])
    
    for i in range(0,len(temp)):
        arr[i] = temp[i]
    
    for i in range(len(temp),len(arr)):
        arr[i] = 0
```

```python
def move_zeroes_to_end_efficient(arr,n):
    for j in range(0,n):
        if(arr[j] == 0):
            break
    
    for i in range(j + 1 , n):
        if arr[i] != 0:
            arr[j],arr[i] = arr[i],arr[j]
            j += 1
```

```python
def remove_duplicates_my_brute_force(arr,n):
    temp = [arr[0]]
    temp_count = 0
    for i in range(1,n):
        if arr[i] == temp[temp_count]:
            continue
        else:
            temp.append(arr[i])
            temp_count += 1
    
    for i in range(0,len(temp)):
        arr[i] = temp[i]
    
    return len(temp)

```

```python
def remove_duplicates_my_efficient(arr,n):
    if(n == 1):
        return 1
    
    j = 0
    #since array is sorted either adjacent elements can be equal or greater
    for i in range(1,n):
        #if equal skip
        if(arr[j] == arr[i]):
            continue
        else:
           
                #if an increasing element found then swap
                arr[j+1] = arr[i]
                #move ahead
                j += 1
    
    return j+1
```

```python
def remove_duplicates_sir_efficient(arr,n):
    i = 0
    for j in range(1,n):
        if(arr[j] != arr[i]):
            arr[i + 1] = arr[j]
            i += 1
    return i + 1
```

```python
def union_array_my_approach(arr1, arr2, n, m):
    i = 0
    j = 0
    appending_element = float('-inf')
    union_array = []

    while i < n and j < m:
        if arr1[i] < arr2[j]:
            if arr1[i] != appending_element:
                appending_element = arr1[i]
                union_array.append(arr1[i])
            i += 1

        elif arr1[i] == arr2[j]:
            if arr1[i] != appending_element:
                appending_element = arr1[i]
                union_array.append(arr1[i])
            i += 1
            j += 1

        else:
            if arr2[j] != appending_element:
                appending_element = arr2[j]
                union_array.append(arr2[j])
            j += 1

    while i < n:
        if arr1[i] != appending_element:
            appending_element = arr1[i]
            union_array.append(arr1[i])
        i += 1   

    while j < m:
        if arr2[j] != appending_element:
            appending_element = arr2[j]   
            union_array.append(arr2[j])
        j += 1  

    return union_array

```

```python
class Solution:
def intersectionArray(self, nums1, nums2):
i,j = 0,0
n = len(nums1)
m = len(nums2)
append_element = float('-inf')
intersect_array = []
while i < n and j < m:
if nums1[i] < nums2[j]:
i += 1
elif nums1[i] > nums2[j]:
j += 1
else:
if nums1[i] != append_element:
intersect_array.append(nums1[i])
i += 1
j += 1
return intersect_array
```

```python
def majority_element_my_better_approach(arr,n):
    count_occurence = {}
    for num in arr:
        if num in count_occurence:
            count_occurence[num] += 1
        else:
            count_occurence[num] = 1

    for key in count_occurence:

        if count_occurence[key] > n//2:
            return int(key)
    
    return -1
```

```python
def majority_element_sir_efficient_solution(arr,n):
    count = 0
    el = 0

    # finding the potential element
    for i in range(0,n):
        if count == 0:
            count = 1
            el = arr[i]
        elif arr[i] == el:
            count += 1
        else:
            count -= 1

    # verifying it 
    count1 = 0
    for i in range(0,n):
        if arr[i] == el:
            count1 += 1
    if(count1 > n // 2):
        return el
    
    return -1
```

```python
def leaders_in_an_array_my_approach(arr,n):
    Greatest_elemet = arr[-1]
    lead = [arr[-1]]

    for i in range(n - 2 , -1 , -1):
        if arr[i] > Greatest_elemet:
            Greatest_elemet = arr[i]
            lead.append(Greatest_elemet)
    
    return lead

```

```python
def rearrange_by_opposite_signs_my_brute_approach(arr,n):
    temp_positive = []
    temp_negative = []

    for i in range(0 , n):
        if arr[i] > 0 :
            temp_positive.append(arr[i])
        else:
            temp_negative.append(arr[i])
    
    for i in range(0,n):
        if i % 2 == 0:
            arr[i] = temp_positive[i//2]
        else:
            arr[i] = temp_negative[i//2]
```

```python
def rearrange_by_opposite_signs_sir_efficient_approach(arr,n):
    final_ans = []
    positive_index = 0
    negative_index = 1

    for i in range(0 , n):
        if arr[i] > 0:
            final_ans.append(arr[i])
            positive_index += 2
        else:
            final_ans.append(arr[i])
            negative_index += 2
    
    return final_ans
```

```python
def ncr_helper(n , r):

    if n == r or r == 0:
         return 1
         
    res = 1
    for i in range(0 , r):
         res *= n - i
         res //= i + 1

    return res

def pascal_trianle_problem1(r,c):

     return ncr_helper(r - 1 , c - 1)
     
```

```python
def pascal_trianle_problem2_my_approach(r):
     
     pascal_row = []
     for i in range(1 , r + 1):
          pascal_row.append(ncr_helper(r - 1 , i - 1))

     return pascal_row
```

```python
def pascal_trianle_problem2_sir_efficient_approach(r):
    pascal_row = [1]
    prev = 1
    for i in range(1 , r):
         prev = prev * ( r - i )
         prev //= i
         pascal_row.append(prev)
    
    return pascal_row
```

```python
class Solution:
    def pascal_helper(self , row):
        pascal_row = [1]
        prev = 1
        for i in range(1 , row):
            prev = prev * (row - i)
            prev = prev // i
            pascal_row.append(prev)
        
        return pascal_row

    def pascalTriangleIII(self, n):
        pascal_triangle = []
        
        for i in range(1 , n + 1):
            pascal_triangle.append(self.pascal_helper(i))

        
        return pascal_triangle
         
```

```python
def rotate_matrix_by_90_degrees_my_approach(matrix , n):
     
     #  Step - 1 for i != j swap it with its diaognally adjacent element 
     for i in range(n): # 0 , 1 , 2 , 3
          # i + 1 in order to avoid the already swapped element
          for j in range(i + 1 , n):
               if i != j:
                    matrix[i][j] , matrix[j][i] = matrix[j][i], matrix[i][j]

     # Step - 2 reverse each row of the matrix
     for i in range(n):
          matrix[i].reverse()
    
```

```python
def two_sum_better_approach(arr,target,n):
    dict_sum = {}
    for i in range(0,n):
        diff = target - arr[i]
        if diff in dict:
            return [i,dict_sum[diff]]
        
        else:
            dict_sum[diff] = i
    
    return -1
```

```python
def two_sum_better_approach(arr,target,n):
    dict_sum = {}
    for i in range(0,n):
        diff = target - arr[i]
        if diff in dict_sum:
            return [i,dict_sum[diff]]
        
        else:
            dict_sum[arr[i]] = i
    
    return -1
```

```python
def two_sum_optimal_approach(arr, target, n):
    sorted_array = sorted(arr)
    left = 0 
    right = n - 1
    first_number = float('-inf')
    second_number = float('-inf')
    two_sum_indices = []

    # sort the array and then use two pointer approach 
    while left < right:
        if sorted_array[left] + sorted_array[right] == target:
            first_number = sorted_array[left]     
            second_number = sorted_array[right]   
            break                                 
        
        elif sorted_array[left] + sorted_array[right] < target:
            left += 1
        else:
            right -= 1
    
    # if no pair found
    if first_number == second_number == float('-inf'):
        return [-1]
    
    # find indices in original array
    for i in range(n):
        if arr[i] == first_number and first_number is not None:
            two_sum_indices.append(i)
            first_number = None   
        
        elif arr[i] == second_number and second_number is not None:
            two_sum_indices.append(i)
            second_number = None  
    
    return two_sum_indices

```

```python
def three_sum_brute_force(arr,n):
    triplet_set = set()

    for i in range(n):
        for j in range(i+1,n):
            for k in range(j+1,n):
                if arr[i] + arr[j] + arr[k] == 0:
                    triplet_set.add(tuple(sorted([arr[i],arr[j],arr[k]])))
    
    return list(triplet_set)
```

```python
class Solution:
    def threeSum(self, nums):
        nums.sort()
        triplets_set = set()

        n = len(nums)

        for i in range(n - 2):

            left = i + 1
            right = n - 1

            while left < right:

                total = nums[i] + nums[left] + nums[right]

                if total == 0:
                    triplets_set.add((nums[i], nums[left], nums[right]))

                    left += 1
                    right -= 1

                elif total < 0:
                    left += 1

                else:
                    right -= 1

        return [list(t) for t in triplets_set]
```

```python
def four_sum_brute_approach(arr , target , n):
    quadruplets = set()
    
    for i in range(0 , n - 3):

        for j in range(i + 1, n - 2):
            for k in range(j + 1, n - 1):
                for l in range(k + 1 , n):
                    if arr[i] + arr[j] + arr[k] + arr[l] == target:
                        temp = [arr[i],arr[j],arr[k],arr[l]]
                        temp.sort()
                        quadruplets.add(tuple(temp))
        
    return [list(t) for t in quadruplets]
```

```python
def four_sum_better_approach(arr,target,n):

    quadruplets = set()
    arr.sort()

    for i in range(0 , len(arr) - 3):
        for j in range(i + 1 , len(arr) - 2):
            hash_set = set()
            for k in range(j + 1 , len(arr) - 1):
                fourth_element = target - (arr[i] + arr[j] + arr[k])
                if fourth_element in hash_set:
                    temp = [arr[i],arr[j],arr[k],fourth_element]
                    temp.sort()
                    quadruplets.add(tuple(temp))

                else:
                    hash_set.add(arr[k])
    

    return [list(t) for t in quadruplets]
```

```python
def four_sum_efficient_approach(arr,target,n):

    quadruplets = set()
    arr.sort()

    for i in range(0 , len(arr) - 3):
        if (i != 0 and arr[i] == arr[i- 1]):
            continue
        else:
            for j in range(i + 1 , len(arr) - 2):
                if j != i + 1 and arr[j] == arr[j - 1]:
                    continue
                else:
                    k = j + 1
                    l = len(arr) - 1

                    while k < l:
                        new_target = target - (arr[i] + arr[j])
                        
                        if arr[k] + arr[l] == new_target:
                            temp = [arr[i],arr[j],arr[k],arr[l]]
                            temp.sort()
                            quadruplets.add(tuple(temp))

                            k += 1
                            l -= 1
                        
                        elif arr[k] + arr[l] < new_target:
                            k += 1
                        
          
                        else:
                            l -= 1
    return [list(t) for t in quadruplets]
```

```python
def sort_an_array_with_0_1_2_brute_approach(arr,n):
    arr.sort()
```

```python
def sort_an_array_with_0_1_2_my_approach(arr,n):
    temp = []
    for i in arr:
        if i == 0:
            temp.append(i)
    
    for i in arr:
        if i == 1:
            temp.append(i)
    
    for i in arr:
        if i == 2:
            temp.append(i)
    

    for i in range(n):
        arr[i] = temp[i]

    return arr
```

```python
def sort_an_array_with_0_1_2_efficient_approach(arr,n):
    low = 0
    mid = 0
    high = n - 1

    while (mid <= high):
        if arr[mid] == 0:
            arr[low],arr[mid] = arr[mid],arr[low]
            low += 1
            mid += 1
        
        elif arr[mid] == 1:
            mid += 1

        else:
            arr[mid],arr[high] = arr[high],arr[mid]
            high -= 1
    
    return arr
```

T.C : O(N)

S.C : O(1)

```python
def subarray_maximum_sum_my_brute_force(arr,n):
    max_sum = float('-inf')
    
    for i in range(n - 1, -1 , -1):
        
        low = 0
        high = i 
        while high < n:
            sum = 0
            if low == high:
                sum = arr[low]
            
            else:
                for j in range(low , high + 1):
                    sum += arr[j]
            
            if sum > max_sum:
                max_sum = sum
            
            low += 1
            high += 1
            
    return max_sum
```

```python
def subarray_maximum_sum_better_approach(arr,n):
    max_sum = float('-inf')
    for i in range(n):
        sum = 0
        for j in range(i,n):
            sum += arr[j]
            max_sum = max(max_sum,sum)
    return max_sum
```

```python
def subarray_maximum_sum_efficient_approach(arr,n):
    max_sum = float('-inf')
    sum = 0
    for i in range(n):
        sum += arr[i]
        if sum > max_sum:
           max_sum = sum

        if sum < 0:
            sum = 0
    
    return max_sum

```

```python
def subarray_maximum_sum_efficient_approach_followup(arr,n):
    max_sum = float('-inf')
    ans_start = -1 
    ans_end = -1
    sum = 0
    start = 0

    for i in range(n):
        if sum == 0:
            start = i

        sum += arr[i]

        if sum > max_sum:
            max_sum = sum
            ans_start = start 
            ans_end = i
        
        if sum < 0:
            sum = 0

    return [arr[i] for i in range(ans_start,ans_end+1)]
```

```python
def majority_element_2(self,arr,n):
            element_count = defaultdict(int)
            majority_element = []
            for i in arr:
                element_count[i] += 1
            
            for key,values in element_count.items():
                if values > math.floor(n / 3):
                    majority_element.append(values)
            
            return majority_element
```

```python
import math
class Solution:
    def majorityElementTwo(self, nums):
        cd1 = None
        cd2 = None 
        count1 = 0 
        count2 = 0
        n = len(nums)
        ele = []
        
        for i in nums:

            if i == cd1:
                count1 += 1

            elif i == cd2:
                count2 += 1

            elif count1 == 0:
                cd1 = i
                count1 = 1

            elif count2 == 0:
                cd2 = i
                count2 = 1

            else:
                count1 -= 1
                count2 -= 1
        
        count1 = 0
        count2 = 0

        for i in nums:
            if i == cd1:
                count1 += 1
            if i == cd2:
                count2 += 1
        
        if count1 > math.floor(n/3):
            ele.append(cd1)
        if count2 > math.floor(n/3):
            ele.append(cd2)
        
        if cd1 == cd2:
            return cd1
        
        return ele
            
```

```python

def missing_and_repeating_number(nums: list[int] , n: int) -> list[int]:
    two_elements = []
    #to find the repeating number we can use a hashmap
    count_freq = defaultdict(int)
    for i in nums:
        count_freq[i] += 1
    
    #we have a repeating element
    for key , value in count_freq.items():
        if value > 1:
            two_elements.append(key)
    
    #to find the missing number we will use the concept of Arithmetic series
    for i in range(1, n + 1):
        if i in count_freq:
            continue

        else:
            two_elements.append(i)
    
    return two_elements
```

```python
def missing_and_repeating_number_optimal_approach(nums: list[int], n: int) -> list[int]:
    nums.sort()
    two_elements = []
    
    sum_of_array = 0
    repeating_element = -1

    # Find repeating element and array sum
    for i in range(n):
        sum_of_array += nums[i]

        if i < n - 1 and nums[i] == nums[i + 1]:
            repeating_element = nums[i]
            two_elements.append(repeating_element)

    total_sum = (n * (n + 1)) // 2

    # Missing number formula
    missing_element = total_sum - (sum_of_array - repeating_element)

    two_elements.append(missing_element)

    return two_elements
```

```python
class Solution:
    def search(self, nums, target):
        low = 0
        high = len(nums) - 1
        while low <= high:
            mid = (low + high) // 2
            if nums[mid] == target:
                return mid
            
            elif nums[mid] > target:
                high = mid - 1
            
            else:
                low = mid + 1
                
        return -1
        
```

```python
class Solution:
    def lowerBound(self, nums, target):
        low = 0
        high = len(nums) - 1
        #if all elements are less than the given target
        idx = len(nums)
        while low <= high:
            mid = (low + high) // 2
            if nums[mid] >= target:
                idx = mid
                high = mid - 1
            else:
                low = mid + 1
        
        return idx 
        
```

```python
class Solution:
    def upperBound(self, nums, x):
        low = 0
        high = len(nums) - 1
        idx = len(nums)
        while low <= high:
            mid = (low + high) // 2
            if nums[mid] <= x:
                low = mid + 1
            
            else:
                idx = mid
                high = mid - 1
        
        return idx
```

```python
class Solution:
    def searchInsert(self, nums, target):
        low = 0
        high = len(nums) - 1
        ins_index = len(nums)
        while low <= high:
            mid = (low + high) // 2
            if nums[mid] >= target:
                ins_index = mid
                high = mid - 1
            else:
                low = mid + 1
        
        return ins_index
```