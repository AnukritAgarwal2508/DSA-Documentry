## Logic Building

### Search for insert Position

Same as solving the lower bound question 

T.C : O(logn)

S.C : O(1)

### Floor and ceil in a sorted array

Floor is the largest “ smallest “ value for a number while ceil is smallest “ largest” value for the given number . both the values can be finded in a single binary search 

Conditions:

if num[mid] == given number → return [nums[mid],nums[mid]]

if num[mid] < given number → floor_value = nums[mid] and low = mid + 1

if num[mid] > given number → ceil_value = nums[mid] and high = mid - 1

Edge Case

Floor → if all elements in  array are smaller than given element then floor can be assumed as  :

$$
floor = nums[len(nums) - 1]
$$

Ceil → if all elements in array are larger than given element then ceil can be assumed as  :

$$
ceil = nums[0]
$$

T.C : O(logn)

S.C : O(1)

### First and Last Occurence

To find the first occurence if the element is found we must travel to the left half in order to find the least possible index value for the given number and for last occurence travel to the right half

T.C : O(logn)

S.C : O(1)

### Search in Rotated Sorted Array - I

B.S Can be used even when the array is rotated . this problem can be solved by checking if the element lies in the sorted or unsorted part of the array . 

the sortability of the array can be checked by nature of the pointers for ex:

$$
nums[mid] <= nums[high]
$$

than that means the right part of the array is sorted and the presence of the element can be verified as :

$$
x >= nums[mid]
$$

and 

$$
x <= nums[high]
$$

that means the element lies there 

T.C : O(logn)

S.C : O(1)

### Search in Rotated Sorted Array - II

The slight modification is that now even duplicates are allowed in the array and the criterial to check if the other half is sorted or not might fail in this condition so we have to add one more condition 

$$
nums[low] == nums[mid] == nums[high]
$$

if the above condition arises that means we have to shorter the interval. because if not included equal intervals might confuse the algo to decide which part is sorted or unsorted

T.C : O(logn)

S.C : O(1)

### Find minimum in rotated sorted array

The main issue in this problem here the small element can lie both in the unsorted and sorted part of the array so it is essential to keep track of the min element

in a sorted array the min element can be the first element in that range so we can ignore the whole range because we are dealing with the min element only 

T.C : O(logn)

S.C : O(1)

### How many times the array is rotated

Same problem as above but we have to return the minimum value index **WHY ?**

Because the rotation point ie pivot lies before the min element in the array and (before and after) of the rotation point lies the sorted part of the array 

T.C : O(logn)

S.C : O(1)

### Single element in duplicates array

The solution of this problem lies in the nature of the index of the element ie wether they are even or odd .

if not considering the extreme cases the similar element lies in the order of 

(even , odd) ie nums[0] == 1 and nums[1] == 1 but when single element is hit it is reversed ie (odd , even)

now when getting the mid if its odd or even decides the further course of our answer

if : mid % 2 == 0

then if : mid + 1 is same as the mid then the element lies in the left half 

if : mid % 2 ≠ 0

then if mid + 1 is same as the mid then the element lies in right half

if mid ≠ mid - 1 ≠ mid + 1

then thats the element we are looking for 

!image.png

T.C : O(log n)

S.C : O(1)

### Bitonic Point

Given an array of integers **arr[]** that is first **strictly increasing** and then maybe **strictly decreasing**, find the **bitonic point**, that is the maximum element in the array. Bitonic Point is a point before which elements are strictly increasing and after which elements are strictly decreasing.

**Note:** It is guaranteed that the array contains **exactly one** bitonic point.

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

```python
class Solution:
    def getFloorAndCeil(self, nums, x):
        low = 0
        high = len(nums) - 1
        floor = -1
        ceil = -1

        while low <= high:
            mid = (low + high) // 2

            if nums[mid] == x:
                return [nums[mid],nums[mid]]
            
            if nums[mid] < x:
                floor = nums[mid]
                low = mid + 1
            
            else:
                ceil = nums[mid]
                high = mid - 1
        
        return [floor,ceil]

```

```python
class Solution:
    def searchRange(self, nums, target):
        low = 0
        high = len(nums) - 1
        first_occrence = -1
        last_occrence = -1

        #first_occrence
        while low <= high:
            mid = (low + high) // 2

            if nums[mid] == target:
                first_occrence = mid
                high = mid - 1
            
            elif nums[mid] > target:
                high = mid - 1
            
            else:
                low = mid + 1
                
        low = 0
        high = len(nums) - 1
        #last_occrence
        while low <= high:
            mid = (low + high) // 2

            if nums[mid] == target:
                last_occrence = mid
                low = mid + 1
            
            elif nums[mid] > target:
                high = mid - 1
            
            else:
                low = mid + 1
        
        return [first_occrence,last_occrence]
        
            
```

```python
class Solution:
    def search(self, nums, x):
        low = 0
        high = len(nums) - 1

        while low <= high:
            mid = (low + high) // 2

            #if element is found at once
            if nums[mid] == x:
                return mid
            #right part is sorted
            elif nums[mid] <= nums[high]:
                if (x >= nums[mid] and x <= nums[high]):
                    low = mid + 1
                
                else:
                    high = mid - 1
            #left part is sorted
            else:
                if (x >= nums[low] and x <= nums[mid]):
                    high = mid - 1
                
                else:
                    low = mid + 1
        
        return -1
 
```

```python
**class Solution:
    def searchInARotatedSortedArrayII(self, nums, target):
        low = 0 
        high = len(nums) - 1

        while low <= high:
            mid = (low + high) // 2

            #if element is found at once
            if nums[mid] == target:
                return True
            
            #edge case
            if nums[low] == nums[mid] == nums[high]:
                low += 1
                high -= 1
            
            #right part is sorted
            elif nums[mid] <= nums[high]:
                if (target >= nums[mid] and target <= nums[high]):
                    low = mid + 1
                
                else:
                    high = mid - 1
            #left part is sorted
            else:
                if (target >= nums[low] and target <= nums[mid]):
                    high = mid - 1
                
                else:
                    low = mid + 1
        
        return False**
```

```python
class Solution:
    def findMin(self, nums):
        low = 0
        high = len(nums) - 1
        min_element = float('+inf')

        while low <= high:
            mid = (low + high) // 2

            if nums[mid] <= nums[high]:
                min_element = min(min_element,nums[mid])
                high = mid - 1
            
            else:
                min_element = min(min_element,nums[low])
                low = mid + 1
        
        return min_element
```

```python
class Solution:
    def findKRotation(self, nums):
        low = 0 
        high = len(nums) - 1
        min_index = -1
        min_element = float('+inf')

        while low <= high:
            mid = (low + high) // 2

            if nums[mid] <= nums[high]:
                if min_element >= nums[mid]:
                    min_element = nums[mid]
                    min_index = mid
                high = mid - 1
            
            else:
                if min_element >= nums[low]:
                    min_element = nums[low]
                    min_index = low
                low = mid + 1
        
        return min_index
```

```python
class Solution:
    def singleNonDuplicate(self, nums):
        if len(nums) == 1:
            return nums[0]
        
        if nums[0] != nums[1]:
            return nums[0]
        
        n = len(nums)
        if nums[n - 1] != nums[n - 2]:
            return nums[n - 1]
        
        low = 1 
        high = n - 2

        while low <= high:
            mid = (low + high) // 2
            if nums[mid] != nums[mid - 1] and nums[mid] != nums[mid + 1]:
                return nums[mid]
            
            elif mid%2 == 0:
                if nums[mid] == nums[mid - 1]:
                    high = mid - 1
                else:
                    low = mid + 1
            
            else:
                if nums[mid] == nums[mid + 1]:
                    high = mid - 1
                else:
                    low = mid + 1
        return -1
```