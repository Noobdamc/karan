#include<bits/stdc++.h>
using namespace std;
typedef long long int ll ;
const int M=1e9+7;


#include <ext/pb_ds/assoc_container.hpp>
#include <ext/pb_ds/tree_policy.hpp>

typedef __gnu_pbds::tree<ll, __gnu_pbds::null_type, less<ll>, __gnu_pbds::rb_tree_tag,
__gnu_pbds::tree_order_statistics_node_update> ordered_set;


typedef __gnu_pbds::tree<
ll,
__gnu_pbds::null_type,
less_equal<ll>,
__gnu_pbds::rb_tree_tag,
__gnu_pbds::tree_order_statistics_node_update> ordered_multiset;


void srt(vector<ll> &v){
sort(v.begin(),v.end());
}


class DisjointSet{
 public:
vector<int> rank,parent,siz;
 DisjointSet (int n){
rank.resize(n+1,0);
parent.resize(n+1);
siz.resize(n+1,1);
for (int i=0;i<=n;i++){ 
parent[i] = i;
} 
 }
int find_par(int nd){
if (nd == parent[nd]) return nd;
return parent[nd] = find_par(parent[nd]);
}
void union_rank(int u,int v){
int ul_u = find_par(u);
int ul_v = find_par(v);
if (ul_u == ul_v) return;
if (rank[ul_u] > rank[ul_v]){
parent[ul_v] = ul_u;
}
else if (rank[ul_u] < rank[ul_v]){
parent[ul_u] = ul_v;
}
else {
parent[ul_v] = ul_u;
rank[ul_u]++;
}
 }
  void union_size(int u,int v){
int ul_u = find_par(u);
int ul_v = find_par(v);
if (ul_u == ul_v) return;
if (siz[ul_u] >= siz[ul_v]){
parent[ul_v] = ul_u;
siz[ul_u]+= siz[ul_v];
}
 else {
parent[ul_u] = ul_v;
siz[ul_v]+= siz[ul_u];
 }
}
 };


class SGT{
public:
vector<int> seg,lazy;
SGT(int n){
seg.resize(4*n);
lazy.resize(4*n);
}
void build(int ind, int low, int high, vector<int> &arr) {
if(low == high) {
seg[ind] = arr[low];
return;
}
int mid = (low + high) >> 1; 
build(2*ind+1, low, mid, arr); 
build(2*ind+2, mid+1, high, arr); 
seg[ind] = seg[2*ind+1] + seg[2*ind+2];
}

void update(int ind, int low, int high, int l, int r, 
int val) {
// update the previous remaining updates 
// and propogate downwards 
if(lazy[ind] != 0) {
seg[ind] += (high - low + 1) * lazy[ind]; 
// propogate the lazy update downwards
// for the remaining nodes to get updated 
if(low != high) {
lazy[2*ind+1] += lazy[ind]; 
lazy[2*ind+2] += lazy[ind]; 
}

lazy[ind] = 0; 
}

// no overlap 
// we don't do anything and return 
// low high l r or l r low high 
if(high < l or r < low) {
return; 
}

// complete overlap 
// l low high r 
if(low>=l && high <= r) {
seg[ind] += (high - low + 1) * val; 
// if a leaf node, it will have childrens
if(low != high) {
lazy[2*ind+1] += val; 
lazy[2*ind+2] += val; 
}
return; 
}
// last case has to be partial overlap case
int mid = (low + high) >> 1; 
update(2*ind+1, low, mid, l, r, val);
update(2*ind+2, mid+1, high, l, r, val); 
seg[ind] = seg[2*ind+1] + seg[2*ind+2];
}

int query(int ind, int low, int high, int l, int r) {

// update if any updates are remaining 
// as the node will stay fresh and updated 
if(lazy[ind] != 0) {
seg[ind] += (high - low + 1) * lazy[ind]; 
// propogate the lazy update downwards
// for the remaining nodes to get updated 
if(low != high) {
lazy[2*ind+1] += lazy[ind]; 
lazy[2*ind+2] += lazy[ind]; 
}

lazy[ind] = 0; 
}

// no overlap return 0; 
if(high < l or r < low) {
return 0; 
}

// complete overlap 
if(low>=l && high <= r) return seg[ind]; 

int mid = (low + high) >> 1; 
int left = query(2*ind+1, low, mid, l, r);
int right = query(2*ind+2, mid+1, high, l, r);
return left + right; 
}
};


class BIT{
public:
vector<int> bit;
BIT(int n) {
bit.resize(n+1,0);
}

void update(int id, int x){
int sz = bit.size();
for(int i= id; i<sz; i += (i &(-i))) {
bit[i] += x;
}
}

ll get_sum (int id) {
ll res=0; int sz = bit.size();
for (int i=id;i>0;i-= (i&(-i))){
res += bit[i];
}
return res;
}
};


ll gcd(ll a, ll b,ll &x,ll &y)
{
if (b == 0)
{
x = 1;
y=0;
return a;
}
ll x1,y1;
ll d = gcd(b,a%b,x1,y1);
x = y1;
y = x1 - y1*(a/b);
return d;
}


ll binexpo(ll a,ll b){
ll ans=1;
while(b>0){
 if (b&1){
ans = (ans*a)%M;
}
a= (a*a)%M;
b>>=1;
}
return ans;
}


const int N = 1e5+1;
ll fact[N];



ll ncr(ll n, ll r) {
ll num = fact[n];
ll den = fact[r]*1LL*fact[n-r];
den%=M;

return (num*1LL*binexpo(den,M-2))%M;
}






    void solve(){
     ll n;
     cin>>n;


     vector<ll> v(n);
     for (int i=0;i<n;i++){ 
         cin>>v[i]; 
     } 


    


    }






 int main(){

ios_base::sync_with_stdio(false);
cin.tie(NULL);
cout.tie(NULL);
     ll t;
     cin>>t;
     while (t--){
solve();
 
     } 

     return 0;
}
