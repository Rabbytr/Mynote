## OJ框架：
```c++
#include <bits/stdc++.h>

#pragma GCC optimize("O3")
#pragma GCC diagnostic error "-std=c++11"
//#pragma comment(linker, "/STACK:102400000,102400000")
#define REP(i, a, b) for(int i = a; i < b; ++i)
#define debug(x) { cerr << #x << '=' << x << "\n"; }
#define Arr(a, l, r) { cerr << #a << " = {"; REP(_, l, r) cerr << ' ' << a[_]; cerr << " }\n"; }
#define mset(a,b) memset(a,b,sizeof(a))
#define mkpr make_pair
#define ll long long
#define print(x) cout<<x<<"\n"

using namespace std;

int main(){
  ios::sync_with_stdio(false);cin.tie(NULL);cout.tie(NULL);

  ...your code

  return 0;
}
```

#### cout保留小数点后两位

```c++
cout<<setiosflags(ios::fixed)<<setprecision(2);
```

###### 保留有效数字去掉setiosflags(ios::fixed)即可

