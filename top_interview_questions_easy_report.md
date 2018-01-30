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


### 344. Reverse String
Write a function that takes a string as input and returns the string reversed.

**Example:**
Given s = "hello", return "olleh".
** Answer:**

	static int x = [](){
		std::ios::sync_with_stdio(false);
		cin.tie(NULL);
		return 0;
	}();
	class Solution {
	public:
		string reverseString(string s) {
			for(int i=0,j=s.size()-1;i<j;++i,--j){
				swap(s[i],s[j]);
			}
			return s;
		}
	};

### 617. Merge Two Binary Trees
Given two binary trees and imagine that when you put one of them to cover the other, some nodes of the two trees are overlapped while the others are not.

You need to merge them into a new binary tree. The merge rule is that if two nodes overlap, then sum node values up as the new value of the merged node. Otherwise, the NOT null node will be used as the node of new tree.

**Example 1:**

	Input:
		Tree 1                     Tree 2
			  1                         2
			 / \                       / \
			3   2                     1   3
		   /                           \   \
		  5                             4   7
	Output:
	Merged tree:
			 3
			/ \
		   4   5
		  / \   \
		 5   4   7

** Answer:**

	/**
	 * Definition for a binary tree node.
	 * struct TreeNode {
	 *     int val;
	 *     TreeNode *left;
	 *     TreeNode *right;
	 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
	 * };
	 */
	static int x = [](){
		std::ios::sync_with_stdio(false);
		cin.tie(NULL);
		return 0;
	}();
	class Solution {
	public:
		TreeNode* mergeTrees(TreeNode* t1, TreeNode* t2) {
			if(t1==NULL)
				return t2;
			if(t2==NULL)
				return t1;
			TreeNode* merged=new TreeNode(t1->val+t2->val);
			merged->left=mergeTrees(t1->left,t2->left);
			merged->right=mergeTrees(t1->right,t2->right);
			return merged;
		}
	};

### 104. Maximum Depth of Binary Tree
Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

** Answer:**

	/**
	 * Definition for a binary tree node.
	 * struct TreeNode {
	 *     int val;
	 *     TreeNode *left;
	 *     TreeNode *right;
	 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
	 * };
	 */
	static int x = [](){
		std::ios::sync_with_stdio(false);
		cin.tie(NULL);
		return 0;
	}();
	class Solution {
	public:
		int maxDepth(TreeNode* root) {
			if(root==NULL)
				return 0;
			return max(maxDepth(root->left),maxDepth(root->right))+1;
		}
	};

### 448. Find All Numbers Disappeared in an Array

Given an array of integers where 1 ≤ a[i] ≤ n (n = size of array), some elements appear twice and others appear once.

Find all the elements of [1, n] inclusive that do not appear in this array.

Could you do it without extra space and in O(n) runtime? You may assume the returned list does not count as extra space.

**Example:**

	Input:
	[4,3,2,7,8,2,3,1]

	Output:
	[5,6]

** Answer:**

	static int x = [](){
		std::ios::sync_with_stdio(false);
		cin.tie(NULL);
		return 0;
	}();
	class Solution {
	public:
		vector<int> findDisappearedNumbers(vector<int>& nums) {
			vector<bool> exist(nums.size()+1,false);
			for(int i=0;i<nums.size();++i){
				exist[nums[i]]=true;
			}
			vector<int> ret;
			for(int i=1;i<exist.size();++i){
				if(!exist[i]){
					ret.push_back(i);
				}
			}
			return ret;
		}
	};

### 461. Hamming Distance
The Hamming distance between two integers is the number of positions at which the corresponding bits are different.

Given two integers x and y, calculate the Hamming distance.

**Note:**

0 ≤ x, y < 231.

**Example:**

	Input: x = 1, y = 4

	Output: 2

	Explanation:
	1   (0 0 0 1)
	4   (0 1 0 0)
		   ↑   ↑

The above arrows point to positions where the corresponding bits are different.

**Answer:**

	static int x = [](){
		std::ios::sync_with_stdio(false);
		cin.tie(NULL);
		return 0;
	}();
	class Solution {
	public:
		int hammingDistance(int x, int y) {
			int diff=x^y;
			int dist=0;
			while(diff){
				++dist;
				diff^=diff&(-diff);
			}
			return dist;
		}
	};

### 100. Same Tree
Given two binary trees, write a function to check if they are the same or not.

Two binary trees are considered the same if they are structurally identical and the nodes have the same value.

**Example 1:**

	Input:     1         1
			  / \       / \
			 2   3     2   3

			[1,2,3],   [1,2,3]

	Output: true

**Example 2:**

	Input:     1         1
			  /           \
			 2             2

			[1,2],     [1,null,2]

	Output: false

**Example 3:**

	Input:     1         1
			  / \       / \
			 2   1     1   2

			[1,2,1],   [1,1,2]

	Output: false


**Answer:**

	/**
	 * Definition for a binary tree node.
	 * struct TreeNode {
	 *     int val;
	 *     TreeNode *left;
	 *     TreeNode *right;
	 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
	 * };
	 */
	static int x = [](){
		std::ios::sync_with_stdio(false);
		cin.tie(NULL);
		return 0;
	}();
	class Solution {
	public:
		bool isSameTree(TreeNode* p, TreeNode* q) {
			if(!p&&!q){
				return true;
			}
			if(!p||!q||q->val!=p->val){
				return false;
			}
			return isSameTree(p->left,q->left)&&isSameTree(p->right,q->right);
		}
	};

### 226. Invert Binary Tree
Invert a binary tree.

		 4
	   /   \
	  2     7
	 / \   / \
	1   3 6   9
to

		 4
	   /   \
	  7     2
	 / \   / \
	9   6 3   1
Trivia:
This problem was inspired by this original tweet by Max Howell:
Google: 90% of our engineers use the software you wrote (Homebrew), but you can’t invert a binary tree on a whiteboard so fuck off.
**Answer:**
	/**
	 * Definition for a binary tree node.
	 * struct TreeNode {
	 *     int val;
	 *     TreeNode *left;
	 *     TreeNode *right;
	 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
	 * };
	 */
	static int x = [](){
		std::ios::sync_with_stdio(false);
		cin.tie(NULL);
		return 0;
	}();
	class Solution {
	public:
		TreeNode* invertTree(TreeNode* root) {
			if(!root){
				return root;
			}
			TreeNode* t=root->left;
			root->left=root->right;
			root->right=t;
			if(root->left)
				invertTree(root->left);
			if(root->right)
				invertTree(root->right);
			return root;
		}
	};

### 204. Count Primes
**Description:**

Count the number of prime numbers less than a non-negative number, n.

**Credits:**
Special thanks to @mithmatt for adding this problem and creating all test cases.
**Answer:**

	static int x = [](){
		std::ios::sync_with_stdio(false);
		cin.tie(NULL);
		return 0;
	}();
	class Solution {
	public:
		int countPrimes(int n) {
			if(n<3) return 0;
			bool is_prime[n];
			memset(is_prime, true, sizeof(is_prime));
			int prime_sum=1;
			for(int i=3;i<n;i+=2){
				if(is_prime[i]){
					++prime_sum;
					for(long long j=(long long)i*i;j<n;j+=2*i)
						is_prime[j]=false;
				}
			}
			return prime_sum;
		}
	};

### 387. First Unique Character in a String
Given a string, find the first non-repeating character in it and return it's index. If it doesn't exist, return -1.

**Examples:**

	s = "leetcode"
	return 0.

	s = "loveleetcode",
	return 2.
**Note:** You may assume the string contain only lowercase letters.

**Answer:**

	static int x = [](){
		std::ios::sync_with_stdio(false);
		cin.tie(NULL);
		return 0;
	}();
	class Solution {
	public:
		int firstUniqChar(string s) {
			if(s.size()==0) return -1;
			int exist[26]={0};
			for(auto ch:s){
				exist[ch-'a']++;
			}
			for(int i=0;i<s.size();++i){
				if(exist[s[i]-'a']==1){
					return i;
				}
			}
			return -1;
		}
	};
### 189. Rotate Array

Rotate an array of n elements to the right by k steps.

For example, with n = 7 and k = 3, the array [1,2,3,4,5,6,7] is rotated to [5,6,7,1,2,3,4].

**Note:**
Try to come up as many solutions as you can, there are at least 3 different ways to solve this problem.



**Answer:**

	static int x = [](){
		std::ios::sync_with_stdio(false);
		cin.tie(NULL);
		return 0;
	}();
	class Solution {
	public:
		void rotate(vector<int>& nums, int k) {
			int n=nums.size();
			if(k>n)k%=n;
			if(k==n||k==0)
				return;
			int axis=n-k;
			reverse(nums.begin(),nums.begin()+axis);
			reverse(nums.begin()+axis,nums.end());
			reverse(nums.begin(),nums.end());

		}
	};

### 206. Reverse Linked List
Reverse a singly linked list.
**Answer:**

	/**
	 * Definition for singly-linked list.
	 * struct ListNode {
	 *     int val;
	 *     ListNode *next;
	 *     ListNode(int x) : val(x), next(NULL) {}
	 * };
	 */
	static int x = [](){
		std::ios::sync_with_stdio(false);
		cin.tie(0);
		return 0;
	}();
	class Solution {
	public:
		ListNode* reverseList(ListNode* head) {
			if(!head||!head->next) return head;
			ListNode* p=head;
			ListNode* q;
			while(p->next){
				q=p->next;
				p->next=q->next;
				q->next=head;
				head=q;
			}
			return head;
		}
	};