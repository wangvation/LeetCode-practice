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