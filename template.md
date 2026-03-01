# Template for Competitive Programming

## C++ - Basic
```cpp
#include <bits/stdc++.h>
using namespace std;

void solve();

int main(){
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    cout.tie(nullptr);
    int t;
    cin >> t;
    while(t--){
        solve();
    }
    return 0;
}

void solve(){
    // solve here
}
```

## C++ - Advanced 
```cpp
#include <bits/stdc++.h>
// include <ext/pb_ds/assoc_container.hpp>
// #include <ext/pb_ds/tree_policy.hpp>

using namespace std;
// using namespace __gnu_pbds;

using ll = long long;
using ld = long double;
using ull = unsigned long long;
using vi = vector<int>;
using vll = vector<ll>;
using pii = pair<int, int>;
using pll = pair<ll, ll>;

// template <class T> using ordered_set = tree<T, null_type, less<T>, rb_tree_tag, tree_order_statistics_node_update>;

const int MOD = 1e9 + 7;
const ll INF = 1e18;
const ld EPS = 1e-9;
const ld PI = acos(-1);

const int dx[] = {0, 1, 0, -1};
const int dy[] = {1, 0, -1, 0};
const int dx8[] = {0, 1, 1, 1, 0, -1, -1, -1};
const int dy8[] = {1, 1, 0, -1, -1, -1, 0, 1};

#define all(x) (x).begin(), (x).end()
#define rall(x) (x).rbegin(), (x).rend()
#define sz(x) ((int)(x).size())
#define pb push_back
#define eb emplace_back
#define mp make_pair
#define fi first
#define se second
#define lb lower_bound
#define ub upper_bound
#define uniq(v) (v).erase(unique(all(v)), (v).end())

#define forn(i, n) for (int i = 0; i < (int)(n); ++i)
#define for1(i, n) for (int i = 1; i <= (int)(n); ++i)
#define fore(i, l, r) for (int i = (int)(l); i <= (int)(r); ++i)
#define forr(i, n) for (int i = (int)(n) - 1; i >= 0; --i)

template <typename T>
istream &operator>>(istream &is, vector<T> &v)
{
    for (auto &i : v)
        is >> i;
    return is;
}
template <typename T>
ostream &operator<<(ostream &os, const vector<T> &v)
{
    for (int i = 0; i < sz(v); ++i)
        os << (i ? " " : "") << v[i];
    return os;
}
template <typename T, typename U>
istream &operator>>(istream &is, pair<T, U> &p)
{
    is >> p.fi >> p.se;
    return is;
}
template <typename T, typename U>
ostream &operator<<(ostream &os, const pair<T, U> &p)
{
    os << p.fi << " " << p.se;
    return os;
}

mt19937_64 rng(chrono::steady_clock::now().time_since_epoch().count());
ll random(ll l, ll r) { return uniform_int_distribution<ll>(l, r)(rng); }

ll gcd(ll a, ll b) { return b ? gcd(b, a % b) : a; }
ll lcm(ll a, ll b) { return a / gcd(a, b) * b; }
ll binpow(ll a, ll b, ll m = MOD)
{
    ll res = 1;
    a %= m;
    while (b > 0)
    {
        if (b & 1)
            res = (res * a) % m;
        a = (a * a) % m;
        b >>= 1;
    }
    return res;
}

void solve()
{
    
}

int main()
{
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    cout << fixed << setprecision(10);

    int t = 1;
    cin >> t;
    while (t--)
    {
        solve();
    }
    return 0;
}
```