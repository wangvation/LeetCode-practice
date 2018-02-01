### 146. LRU Cache

Design and implement a data structure for Least Recently Used (LRU) cache. It should support the following operations: get and put.

get(key) - Get the value (will always be positive) of the key if the key exists in the cache, otherwise return -1.
put(key, value) - Set or insert the value if the key is not already present. When the cache reached its capacity, it should invalidate the least recently used item before inserting a new item.

**Follow up:**

Could you do both operations in O(1) time complexity?

**Example:** **

	LRUCache cache = new LRUCache( 2 /* capacity */ );

	cache.put(1, 1);
	cache.put(2, 2);
	cache.get(1);       // returns 1
	cache.put(3, 3);    // evicts key 2
	cache.get(2);       // returns -1 (not found)
	cache.put(4, 4);    // evicts key 1
	cache.get(1);       // returns -1 (not found)
	cache.get(3);       // returns 3
	cache.get(4);       // returns 4

** Answer:**

	static auto x = [](){
		std::ios::sync_with_stdio(false);
		cin.tie(NULL);
		return 0;
	}();
	class LRUCache {
	public:
		LRUCache(int capacity) {
			this->size=0;
			this->capacity=capacity;
			this->cache_map=new map<int,CacheEntry*>();
			this->tail=NULL;
			this->head=NULL;
		}

		int get(int key) {
			if(this->cache_map->count(key)>0){
				CacheEntry* entry=(*(this->cache_map))[key];
				bringToHead(entry->keyIdx);
				return entry->value;
			}
			return -1;
		}

		void put(int key, int value) {
			if(this->cache_map->count(key)>0){
				CacheEntry* entry=(*(this->cache_map))[key];
				entry->value=value;
				bringToHead(entry->keyIdx);
				return ;
			}
			KeyList* keyIdx=new KeyList(key,NULL,head);
			CacheEntry* entry=new CacheEntry(value,keyIdx);
			if(this->head==NULL){
				this->head=keyIdx;
				this->tail=this->head;
			}else{
				 this->head->previous=keyIdx;
				 this->head=keyIdx;
			}
			(*(this->cache_map))[key]=entry;
			if(this->size<this->capacity){
				this->size++;
			}else{
				CacheEntry* tail_entry=(*(this->cache_map))[this->tail->key];
				this->cache_map->erase(this->tail->key);
				delete tail_entry;
				this->tail=this->tail->previous;
				delete this->tail->next;
				this->tail->next=NULL;
			}

		}
		~LRUCache(){
			map<int,CacheEntry*>::iterator iter;
			for(iter = this->cache_map->begin(); iter != this->cache_map->end(); iter++) {
				CacheEntry* entry=iter->second;
				delete entry;
				(*(this->cache_map))[iter->first]=NULL;
			}
			this->cache_map->clear();
			delete this->cache_map;
			KeyList* p=this->head;
			KeyList* q=p;
			while(p){
				q=p->next;
				delete p;
				p=q;
			}
			this->head=NULL;
			this->tail=NULL;
		}
	private:

		struct KeyList{
			int key;
			KeyList* previous;
			KeyList* next;
			KeyList(int pKey, KeyList* pPrevious,KeyList* pNext){
				key=pKey;
				previous=pPrevious;
				next=pNext;
			}
		};
		struct CacheEntry{
			int value;
			KeyList* keyIdx;
			CacheEntry(int pValue, KeyList* pKeyIdx){
				value=pValue;
				keyIdx=pKeyIdx;
			}
		};
		map<int,CacheEntry*> *cache_map;
		int size;
		int capacity;
		KeyList* head;
		KeyList* tail;
		void bringToHead(KeyList* keyIdx){
			if(keyIdx==this->head)
				return ;
			if(keyIdx==this->tail){
				this->tail=keyIdx->previous;
				this->tail->next=NULL;
			}else{
				KeyList* preEntry=keyIdx->previous;
				preEntry->next=keyIdx->next;
				keyIdx->next->previous=preEntry;
			}
			keyIdx->previous=NULL;
			keyIdx->next=this->head;
			this->head->previous=keyIdx;
			this->head=keyIdx;
		}
	};

	/**
	 * Your LRUCache object will be instantiated and called as such:
	 * LRUCache obj = new LRUCache(capacity);
	 * int param_1 = obj.get(key);
	 * obj.put(key,value);
	 */

### 23. Merge k Sorted Lists
Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.

**Answer:**

	//Answer#1
	/**
	 * Definition for singly-linked list.
	 * struct ListNode {
	 *     int val;
	 *     ListNode *next;
	 *     ListNode(int x) : val(x), next(NULL) {}
	 * };
	 */
	class Solution {
	public:
		ListNode* mergeKLists(vector<ListNode*>& lists) {
			int k=lists.size();
			if(k==0){
				return NULL;
			}
			ListNode* head=NULL;
			ListNode* p=NULL;
			while(true){
				ListNode* minnode=NULL;
				int minIdx=-1;
				for(int i=0;i<k;++i){
					ListNode* node=lists[i];
					if(node==NULL){
						continue;
					}
					if(minIdx==-1||node->val<minnode->val){
						minnode=node;
						minIdx=i;
					}
				}
				if(minIdx==-1){
					break;
				}
				if(head==NULL){
					head=lists[minIdx];
					p=head;
				}else{
					p->next=lists[minIdx];
					p=p->next;
				}
				lists[minIdx]=lists[minIdx]->next;
				p->next=NULL;
			}
			return head;
		}
	};
	//Answer#2
	/**
	 * Definition for singly-linked list.
	 * struct ListNode {
	 *     int val;
	 *     ListNode *next;
	 *     ListNode(int x) : val(x), next(NULL) {}
	 * };
	 */
	static auto x = [](){
		std::ios::sync_with_stdio(false);
		cin.tie(NULL);
		return 0;
	}();
	class Solution {
	public:
		struct cmp {
			bool operator()(ListNode *a, ListNode *b) {
				return a->val > b->val;
			}
		};
		ListNode* mergeKLists(vector<ListNode*>& lists) {
			int k=lists.size();
			ListNode* head=nullptr;
			ListNode **p=&head;
			priority_queue<ListNode*,vector<ListNode*>,cmp> que;
			for(int i=0;i<k;++i){
				if(lists[i]){
					que.emplace(lists[i]);
				}
			}
			while(!que.empty()){
				ListNode* cur=que.top();
				que.pop();
				if(cur->next){
					que.emplace(cur->next);
				}
				*p=cur;
				p=&(cur->next);
			}
			return head;
		}
	};
	