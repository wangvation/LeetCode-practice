### Top interview questions medium report

#### 743. Network Delay Time

There are N network nodes, labelled 1 to N.

Given times, a list of travel times as directed edges times[i] = (u, v, w), where u is the source node, v is the target node, and w is the time it takes for a signal to travel from source to target.

Now, we send a signal from a certain node K. How long will it take for all nodes to receive the signal? If it is impossible, return -1.

**Note:**
1. N will be in the range [1, 100].
2. K will be in the range [1, N].
3. The length of times will be in the range [1, 6000].
4. All edges times[i] = (u, v, w) will have 1 <= u, v <= N and 1 <= w <= 100.

** Answer:**

	```cpp
	class Solution {
		struct LinkedEdge{
			int next;
			int to;
			int weight;
		};
	public:
		const int INF=600000;
		int networkDelayTime(vector<vector<int>>& times, int N, int K) {
			int head[N+1];
			fill(head,head+N+1,-1);
			vector<LinkedEdge> edges(times.size());
			for(int i=0;i<times.size();++i){
				LinkedEdge edge;
				edge.to=times[i][1];
				edge.weight=times[i][2];
				edge.next=head[times[i][0]];
				head[times[i][0]]=i;
				edges[i]=edge;
			}
			int dist[N+1];
			fill(dist,dist+N+1,INF);
			typedef pair<int,int> dist_pair;
			priority_queue<dist_pair,vector<dist_pair>,greater<dist_pair> > que;
			dist[K]=0;
			que.push(dist_pair(0,K));
			while(!que.empty()){
				dist_pair dp=que.top();
				que.pop();
				int v=dp.second;
				if(dist[v]<dp.first) continue;
				for(int i=head[v];i!=-1;i=edges[i].next){
					if(dist[edges[i].to]>dist[v]+edges[i].weight){
						dist[edges[i].to]=dist[v]+edges[i].weight;
						que.push(dist_pair(dist[edges[i].to],edges[i].to));
					}
				}
			}
			int max_time=0;
			for(int i=1;i<=N;++i){
				if(dist[i]>=INF)
					return -1;
				if(max_time<dist[i]){
					max_time=dist[i];
				}
			}
			return max_time;
		}

	};

### 148. Sort List
Sort a linked list in O(n log n) time using constant space complexity.
**Answer:**

	/**
	 * Definition for singly-linked list.
	 * struct ListNode {
	 *     int val;
	 *     ListNode *next;
	 *     ListNode(int x) : val(x), next(NULL) {}
	 * };
	 */
	static int x=[](){
		std::ios::sync_with_stdio(false);
		cin.tie(NULL);
		return 0;
	}();
	class Solution {
	public:
		ListNode* sortList(ListNode* head) {
			if(!head||!head->next) return head;
			typedef pair<int,ListNode*> nodepair;
			priority_queue<nodepair,vector<nodepair>,greater<nodepair> > que;
			ListNode *p=head;
			while(p){
				que.push(nodepair(p->val,p));
				p=p->next;
			}
			nodepair np=que.top();
			que.pop();
			head=np.second;
			p=head;
			while(!que.empty()){
				np=que.top();
				que.pop();
				p->next=np.second;
				p=p->next;
				p->next=NULL;
			}
			return head;
		}
	};

### 179. Largest Number
Given a list of non negative integers, arrange them such that they form the largest number.

For example, given [3, 30, 34, 5, 9], the largest formed number is 9534330.

Note: The result may be very large, so you need to return a string instead of an integer.

**Credits:**
Special thanks to @ts for adding this problem and creating all test cases.

**Answer:**

	static auto x = [](){
		std::ios::sync_with_stdio(false);
		cin.tie(NULL);
		return 0;
	}();
	class Solution {
	public:
		string largestNumber(vector<int>& nums) {
			if(nums.size()==0)
				return 0;
			sort(nums.begin(),nums.begin()+nums.size(),cmp);
			return vectostr(nums);
		}
		static bool cmp(int a,int b){
			int lga=log(a)/log(10);
			int lgb=log(b)/log(10);
			long long pow10a=pow(10,lga+1);
			long long pow10b=pow(10,lgb+1);
			pow10a=pow10a>=10?pow10a:10;
			pow10b=pow10b>=10?pow10b:10;
			long long ab=a*pow10b+b;
			long long ba=b*pow10a+a;
			return ab>ba;
		}
		string vectostr(vector<int>& nums){
			int start=0;
			int len=nums.size();
			while(start<len&&nums[start]==0)start++;
			if(start>=len){
				return "0";
			}
			stringstream ss;
			for(int i=start;i<len;++i){
				ss<<nums[i];
			}
			return ss.str();
		}
	};

### 8. String to Integer (atoi)

Implement atoi to convert a string to an integer.

**Hint:**
Carefully consider all possible input cases. If you want a challenge, please do not see below and ask yourself what are the possible input cases.

**Notes:**
It is intended for this problem to be specified vaguely (ie, no given input specs). You are responsible to gather all the input requirements up front.
**Answer:**

	static int x=[](){
		std::ios::sync_with_stdio(false);
		cin.tie(NULL);
		return 0;
	}();
	class Solution {
	public:
		const int MAX_INT=2147483647;
		const int MIN_INT=-2147483648;
		int myAtoi(string str) {
			int flag=0;
			int start=0;
			for(;start<str.length()&&str[start]==' ';++start);
			char c=str[start];
			if(c=='+'){
				start++;
			}else if(c=='-') {
				start++;
				flag=1;
			}
			long long ans=0;
			for(int i=start;i<str.length()&&str[i]>='0'&&str[i]<='9';++i){
				if(flag){
					ans=ans*10-(str[i]-'0');
					if(ans<MIN_INT){
						ans=MIN_INT;
						break;
					}
				}else{
					ans=ans*10+(str[i]-'0');
					if(ans>MAX_INT){
						ans=MAX_INT;
						break;
					}
				}
			}
			return ans;
		}
	};

### 29. Divide Two Integers

Divide two integers without using multiplication, division and mod operator.

If it is overflow, return MAX_INT.

**Answer:**

	static int x = [](){
		std::ios::sync_with_stdio(false);
		cin.tie(NULL);
		return 0;
	}();
	class Solution {
	public:
		const int MAX_INT=2147483647;
		const int MIN_INT=-2147483648;
		int divide(int dividend, int divisor) {
			if(dividend==MIN_INT&&divisor==-1)
				return MAX_INT;
			unsigned int udividend=dividend<0?-dividend:dividend;
			unsigned int udivisor=divisor<0?-divisor:divisor;
			if(udividend<udivisor){
				return 0;
			}
			unsigned int ans=0;
			unsigned int scale=1;
			unsigned int scale_div=udivisor;
			while(scale_div<=udividend>>1){
				scale_div<<=1;
				scale<<=1;
			}
			ans+=scale;
			udividend-=scale_div;
			if(udividend>=udivisor)
				ans+=divide(udividend,udivisor);
			if(dividend>>31==divisor>>31){
				return ans;
			}
			return -ans;
		}
	};

### 15. 3Sum

Given an array S of n integers, are there elements a, b, c in S such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.

Note: The solution set must not contain duplicate triplets.

For example, given array S = [-1, 0, 1, 2, -1, -4],

A solution set is:

	[
	  [-1, 0, 1],
	  [-1, -1, 2]
	]

**Answer:**

	static int x = [](){
    std::ios::sync_with_stdio(false);
    cin.tie(NULL);
    return 0;
	}();
	class Solution {
	public:
		vector<vector<int>> threeSum(vector<int>& nums) {
			sort(nums.begin(), nums.end());
			int n=nums.size();
			vector<vector<int>> result;
			for(int i=0;i<n;++i){
				if(nums[i]>0)
					break;
				if(i>0&&nums[i]==nums[i-1]) continue;
				int target =-nums[i];
				int front=i+1;
				int end=n-1;
				while(front<end){
					int sum=nums[front]+nums[end];
					if(sum<target){
						front++;
					}else if(sum>target){
						end--;
					}else{
						result.push_back({nums[i],nums[front++],nums[end--]});
						while(front<end&&nums[front]==nums[front-1])++front;
						while(front<end&&nums[end]==nums[end+1])--end;
					}
				}
			}

			return result;
		}
	};