# problem solving report

## Array

### Two Sum

Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

Example:
    Given nums = [2, 7, 11, 15], target = 9,
    Because nums[0] + nums[1] = 2 + 7 = 9,
    return [0, 1].

Answer:

    '''cpp
    //输入输出流加速
    static int x = [](){
		std::ios::sync_with_stdio(false);
		cin.tie(NULL);
		return 0;
    }();

    class Solution {
    public:
        vector<int> twoSum(vector<int>& nums, int target) {
            map<int,int> sum_map;
            for(int i=0;i<nums.size();i++)
            {
                auto search = sum_map.find(nums[i]);
                if(search != sum_map.end()) {
                    return vector<int>{search->second,i};
                }
                sum_map[target-nums[i]]=i;
            }
        }
    };
    '''



### Remove Duplicates from Sorted Array

Given a sorted array, remove the duplicates in-place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

**Example:**

    Given nums = [1,1,2],
    Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.
    It doesn't matter what you leave beyond the new length.

**Answer:**

	'''C++
	//输入输出流加速
    static int x = [](){
		std::ios::sync_with_stdio(false);
		cin.tie(NULL);
		return 0;
    }();
    class Solution {
    public:
        int removeDuplicates(vector<int>& nums) {
            int length=nums.size();
            if(length==0)return 0;
            int index=0;
            int j=1;
            while(j<length)
            {
                if(nums[index]!=nums[j]){
                    nums[++index]=nums[j];
                }
                ++j;
            }
            return index+1;
        }
    };
    '''
### 326. Power of Three
Given an integer, write a function to determine if it is a power of three.

** Follow up: **
Could you do it without using any loop / recursion?

** Credits:**
Special thanks to @dietpepsi for adding this problem and creating all test cases.

**Answer:**

	'''C++
	//Answer 1
	//输入输出流加速
    static int x = [](){
		std::ios::sync_with_stdio(false);
		cin.tie(NULL);
		return 0;
    }();
	class Solution {
	public:
		bool isPowerOfThree(int n) {
			if(n==1)
				return true;
			long long i;
			for(i=1;i*3<=n;i*=3);
			return i==n;
		}
	};

	//Answer 2
	//输入输出流加速
    static int x = [](){
    std::ios::sync_with_stdio(false);
    cin.tie(NULL);
    return 0;
    }();
	class Solution {
	public:
		bool isPowerOfThree(int n) {
			if(n<=0)
				return false;
			while(n%3==0)
			{
				n/=3;
			}
			return 1==n;
		}
	};

	//Answer 3
	//without using any loop / recursion
	static int x = [](){
		std::ios::sync_with_stdio(false);
		cin.tie(NULL);
		return 0;
    }();
	class Solution {
	public:
		bool isPowerOfThree(int n) {
			if(n==1) return true;
			double epsilon=1e-15;
			double i=log10(n) / log10(3);
			return abs(round(i) - i) < 2*epsilon;
		}
	};

	//Answer 4
	//without using any loop / recursion
	static int x = [](){
    std::ios::sync_with_stdio(false);
    cin.tie(NULL);
    return 0;
    }();
	class Solution {
	public:
		const double epsilon=1e-15;
		bool isPowerOfThree(int n) {
			double i=log10(n) / log10(3);
			return abs(round(i) - i) < 2*epsilon;
		}
	};
	'''
### 371. Sum of Two Integers
Calculate the sum of two integers a and b, but you are not allowed to use the operator + and -.

**Example:**
Given a = 1 and b = 2, return 3.

**Credits:* ***
Special thanks to @fujiaozhu for adding this problem and creating all test cases.
**Answer:**

	'''
	static int x = [](){
		std::ios::sync_with_stdio(false);
		cin.tie(NULL);
		return 0;
	}();
	class Solution {
	public:
		int getSum(int a, int b) {
			int sum;
			int carry;
			do{
				sum=a^b;
				carry=(a&b)<<1;
				a=sum;
				b=carry;
			} while(carry!=0);
			return sum;
		}
	};

### 7. Reverse Integer
Given a 32-bit signed integer, reverse digits of an integer.

**Example 1:**

Input: 123
Output:  321

**Example 2:**

Input: -123
Output: -321

**Example 3:**

Input: 120
Output: 21

**Note:**
Assume we are dealing with an environment which could only hold integers within the 32-bit signed integer range. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

**Answer:**

	static int x = [](){
		std::ios::sync_with_stdio(false);
		cin.tie(NULL);
		return 0;
	}();

	class Solution {
	public:
		int reverse(int x) {
			long long ret=0;
			while(x!=0){
				ret=ret*10+x%10;
				if(ret>INT_MAX||ret<INT_MIN)
					return 0;
				x/=10;
			}
			return ret;
		}
	};


### 283. Move Zeroes
Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

For example, given nums = [0, 1, 0, 3, 12], after calling your function, nums should be [1, 3, 12, 0, 0].

**Note:**
You must do this in-place without making a copy of the array.
Minimize the total number of operations.
** Answer:**

	static int x = [](){
		std::ios::sync_with_stdio(false);
		cin.tie(NULL);
		return 0;
	}();
	class Solution {
	public:
		void moveZeroes(vector<int>& nums) {
			for(int i=0,j=0;i<nums.size();++i){
				if(nums[i]){
					if(i!=j)
						swap(nums[j++],nums[i]);
					else
						++j;
				}
			}
		}
	};

### 268. Missing Number
Given an array containing n distinct numbers taken from 0, 1, 2, ..., n, find the one that is missing from the array.

** Example 1**

	Input: [3,0,1]
	Output: 2
** Example 2**

	Input: [9,6,4,2,3,5,7,0,1]
	Output: 8

** Note:**
Your algorithm should run in linear runtime complexity. Could you implement it using only constant extra space complexity?
** Answer:**

	//Answer1
	class Solution {
	public:
		int missingNumber(vector<int>& nums) {
			vector<bool> is_exist(nums.size()+1,false);
			for(int i=0;i<nums.size();++i){
				is_exist[nums[i]]=true;
			}
			for(int i=0;i<is_exist.size();++i){
				if(!is_exist[i]) return i;
			}
		}
	};

	//Answer2
	static int x = [](){
		std::ios::sync_with_stdio(false);
		cin.tie(NULL);
		return 0;
	}();
	class Solution {
	public:
		int missingNumber(vector<int>& nums) {
			int miss=0;
			int n=nums.size();
			for(int i=0;i<n;++i){
				miss^=i^nums[i];
			}
			miss^=n;
			return miss;
		}
	};

### 136. Single Number

Given an array of integers, every element appears twice except for one. Find that single one.

**Note:**
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?
** Answer:**

	static int x = [](){
		std::ios::sync_with_stdio(false);
		cin.tie(NULL);
		return 0;
	}();
	class Solution {
	public:
		int singleNumber(vector<int>& nums) {
			for(int i=1,len=nums.size();i<len;++i){
				nums[0]^=nums[i];
			}
			return nums[0];
		}
	};

### 69. Sqrt(x)
Implement int sqrt(int x).

Compute and return the square root of x.

x is guaranteed to be a non-negative integer.


**Example 1:**

	Input: 4
	Output: 2
**Example 2:**

	Input: 8
	Output: 2
	Explanation: The square root of 8 is 2.82842..., and since we want to return an integer, the decimal part will be 	truncated.
**Answer:**

	static int x = [](){
		std::ios::sync_with_stdio(false);
		cin.tie(NULL);
		return 0;
	}();
	class Solution {
	public:
		int mySqrt(int x) {
			if(x<=1) return x;
			int low=0;
			int high=x;
			long long mid;
			long long prod; 
			while(high>=low){
				mid=(high+low)>>1;
				prod=mid*mid;
				if(prod==x) return mid;
				if(prod>x)
					high=mid-1;
				else
					low=mid+1;
			}
			return high;
		}
	};