宏定義
```c++
#define ll long long
#define D long double
#define dui pair<ll,ll>
#define INT signed
#define IOS() {std::ios::sync_with_stdio(false); std::cin.tie(nullptr);}
#define VECTOR(n, x)  int n;cin>>n; vector<int> x(n); for (int i = 0; i < n; ++i) { cin>>x[i]; }
#define Vector(m, x)  int zzz=m; vector<int> x(zzz); for (int i = 0; i < zzz; ++i) { cin>>x[i]; }
#define Range(i, n) for (int i = 0; i < (n); ++i)
#define Repeat(n)  int n;cin>>n;while((n)-->0)
int qqqqqqqq;
#define Judge(n) cout<<((n)?"YES":"NO");
#define For(num)  qqqqqqqq=num;while((qqqqqqqq)-->0)
#define PR(n, re) {cout<<(n);return re;}
#define PC(n) {cout<<(n);continue;}
```


# 1983號 956期

##


# 2071

構造一個全排列，使得前綴和沒有任何平方數

> ### 思路
> 如果求和就是的話，無法
> 否則，不行就換一個就好了
> 可以證明，雖然理論複雜度高，但是因為平方數的密度不高，不需要大量避開
```c++
set<int> ji;

if (ji.empty()) for (int i = 1; i < 500010; ++i) ji.insert(i * i);

int n,sum=0;
cin >> n;

if (ji.count(((1 + n) * n) / 2) == 1) PR("-1",)

vector<int> res,ans;
for (int i = n; i > 0 ; --i) res.push_back(i);
while (!res.empty())
{
    vector<int> nw;
    for(int i:res)
        if(ji.count(sum+i)==1) nw.push_back(i);
        else {ans.push_back(i);sum+=i;}
    res=nw;
}
for(int i:ans) cout<<i<<" ";
```

上面代碼為簡化顯示，實際上第一遍篩選直接存不用放數組里會更節約內存
```c++
vector<int> res,ans;
int sum=0;
for (int i = n; i > 0 ; --i)
{
    if(ji.count(sum+i)==1)
        res.push_back(i);
    else
    {ans.push_back(i);sum+=i;}
}
while (!res.empty())
{
    vector<int> nw;
    for(int i:res)
    {
        if(ji.count(sum+i)==1) nw.push_back(i);
        else  {ans.push_back(i);sum+=i;}
    }
    res=nw;
}
for(int i:ans) cout<<i<<" ";
```


# 2022號 978期 二級


# 2075

## A 


給出n和k，構造多次減法使得在最少次數裡面使得n為零
- 被減數範圍為`[1,k]`奇偶性必須和減數相同

思路
1. `n<k`的時候一次
2. `n>=k`的時候減掉一次就為偶數，要麼是k，要麼是k-1
3. 之後就是除法的向上取整

```c++
int n, k, sum = 1;
cin >> n >> k;
if (n >= k)
{
    n -= ((n - k) % 2 == 0) ? k : (k - 1);
    sum += ceil(n * 1.0 / (k / 2 * 2));
}
cout << sum;
```

-----------------------------------------------


# 2094號 1017期 四級


## A

### 題目
每次輸入三個字符串，輸出他們的首字母
```c++
string a, b, c;
cin >> a >> b >> c;
cout << a[0] << b[0] << c[0] << endl;
```

注意不要這麼寫：
```c++
cout << a[0] + b[0] + c[0] << endl;
cout << " " + a[0] + b[0] + c[0] << endl;
```
前者會讓編譯器強轉為數字后相加，後者觸發未定義錯誤

## B

### 題目
每一次給出`n m [l r]`，滿足`l-r=n l<=0 r>=0`，求區間`[a,b]`滿足
1. 新的區間在原其間範圍內`a>l b<r`
2. 新的區間包含`0`
```c++
int n, m, l, r;
cin >> n >> m >> l >> r;
if (l == 0) cout << "0" << " " << m;
else if (r == 0) cout << -m << " " << "0";

else 
{
    double bili=1.0*m/n;
    int newl=bili*l;
    int newr=newl+m;
    cout<<newl<<" "<<newr;
}
cout<<endl;
```

## C


## D


# 2098號 1092期 二級

## A

```c++
int hash[10]={0};
for (int i = 0; i < 10; ++i)
{
    char a;
    cin >> a;
    hash[a - '0']++;
}

string ans;
for (int i = 0; i < 10; ++i)
{
    for (int j = 0; j < 10; ++j)
    {
        if (j >= 9 - i && hash[j] > 0)
        {
            hash[j]--;
            ans += to_string(j);
            break;
        }
    }
}
cout<<ans<<endl;
```



# 2103號 1019期 二級 (4/6)

## A

### 題目
每一次輸入一個數組，現在構造一個數組，要求每一個數字不一樣，並且和原數組對應位置乘積相等
如果做不到，那就和原數組的子數組對應，求子數組的最大長度

### 數據
- `1 2 3`->3
- `3 1 4 1 5`->4
- `1`->1
1. 因為多個數必定有最小公倍數，所以必定能保證有這樣的子數組
2. 但是如第二組一樣，原數組可能重複，這時候我們要把他篩選掉

```c++
set<int> a;
Repeat(n)
{
    int b;
    cin>>b;
    a.insert(b);
}
cout<<a.size()<<endl;
```


## B

### 題目
二進制串表示要輸入的內容，現在按按鈕
1. 按一下按鈕，花費1時間
2. 切換0<->1，花費1時間
- 允許將二進制串某一段翻轉，那麼最小的時間為多少？

```c++
int n;
string s;
cin >> n >> s;
int sum = 0;
s = "0" + s;
int idx = -1, idx0 = -1, idx00;

for (int i = 0; i < s.size(); ++i)
{
    if (s[i] == '1')
    { idx = i; break; }
}
if (idx == -1)//00000
{
    cout << n << endl;
    continue;
}
for (int i = idx; i < s.size(); ++i)
{
    if (s[i] == '0')
    { idx0 = i; break; }
}
if (idx0 != -1)// else -> 000011
{
    for (int i = idx0; i < s.size(); ++i)
    {
        if (s[i] != '1') idx00 = i;
        else break;
    }
    reverse(s.begin() + idx, s.begin() + idx00 + 1);
}
for (int i = 1; i < s.size(); ++i)
    if (s[i - 1] != s[i]) sum++;
cout << sum + n << endl;
```

## C

http://chatgpt.com/c/6816f379-653c-8005-b5c3-3e0f68b48538


## D

https://chatgpt.com/c/68169e5c-80a4-8005-ab5f-dcd9a4186e25

```c++
int n;
cin >> n;
vector<int> a(n),p(n, 0);
int mx = 1, id = -1;

for (int i = 0; i < n; i++)
{
    cin >> a[i];
    if (a[i] == -1) id = i;
    mx = max(a[i], mx);
}

int l = 1, r = n;

for (int i = 1; i <= mx; i++)
{
    for (int j = 0; j < id; j++)
    {
        if (a[j] == i)
        {
            if (i % 2 == 1) p[j] = r--;
            else p[j] = l++;
        }
    }
    for (int j = n - 1; j > id; j--)
    {
        if (a[j] == i)
        {
            if (i % 2 == 1) p[j] = r--;
            else p[j] = l++;
        }
    }
}

for (int i = 0; i < n; i++)
{
    if (a[i] == -1) cout << r << " ";
    else cout << p[i] << " ";
}
cout << "\n";
```

# 2104 期 二级

## A
A<B<C  在C中取出`[1,C.size()]`张牌分到A B堆，使得三堆牌相等

關鍵點：
- `[1 1 1]` 所有數量相等，但是至少取出1个
- `[3 30 30]` B的數量遠超平均值，不能被C分配
```c++
int a, b, c; cin >> a >> b >> c;

if ((a + b + c) % 3 != 0) cout<<"NO";
else
{
    int pjs=(a+b+c)/3;
    if(c<pjs+1||b>pjs) cout<<"NO";
    else cout<<"YES";
}
```

## B

一串數組，長度為n，對於第`i range [1,n]`循環，每一次臨時將任意一個數字（可以就是最後一個元素）放在數組末尾，求末尾i个元素的求和

關鍵點：
- 末尾的`i-1`个必定被選中，當選中其他的第`i`个可能沒被選中
- 所以第`i`个要和賸餘絕對不會選中的相比，取最大的（使用稀疏表max版）
- 因為是`i-1`个元素求和，所以`sum`加總放在輸出後面
```c++
VECTOR(n,x);//大小為n的向量x
ST st(x);//稀疏表模板，索引从1開始
int sum=0;
for (int i = n-1; i >=0 ; --i)
{
    cout<<st.query(1,i+1)+sum<<" ";
    sum+=x[i];
}
```


## C

題目：`[1-n]`的牌，大的可以吃小的，1可以吃n，現在輸入字串為每一張牌歸誰

如果兩張牌：更小的會贏，因為1->n

對於多張牌，因為贏者通吃，所以優勢可以持續，被拿掉優勢牌==輸掉

對於後手而言：
- 尾可以幹掉前面所有的，除了第一章
- 如果第一張是自己的，那不用擔心被回手掏
- 如果前面有任意一張，可以把對方的回手掏壓下，必定贏
- 也就是説，衹要擁有最大一張，就必贏
- 但是如果前面都沒有牌，那麼單獨一張必輸，這是容易驗證的

對於先手而言：
- 因為後手可以看到先手的牌，如果不防禦，最大的會被小的吃，其他的會被最大的吃，一定被別人拿走，有兩種方式
1. 有最大的兩張牌，每一次出第二大的牌，因為對方沒有更大的牌了，因為不出最大的，也沒有辦法用循環攻擊
2. 有最大最小兩張牌，每一次出最大的，最小的牌保證了無法循環攻擊，因為不出最小的，所以無法攻擊

```c++
int n;
string s;
cin >> n >> s;
if (n == 2)
{
    if (s[0] == 'A') cout << "Alice";
    if (s[0] == 'B') cout << "Bob";
}
else
{
    if (s[n - 1] == 'B')
    {
        if (count(s.begin(), s.end(), 'B') >= 2) cout << "Bob";
        else cout << "Alice";
    }
    if (s[n - 1] == 'A')
    {
        if(s[n-2]=='A'||s[0]=='A') cout<<"Alice";
        else cout<<"Bob";
    }
}
```

# 2107 期 二级

## A

每一次輸入一個數組，把他分為兩個數組，要求
1. 數組至少要有一個元素
2. 兩個數組里所有元素的最大公因數（gcd）不能一樣


關鍵點，我們衹要找到一個不是一的數字，剩下的數字gcd后得到1，就可以分開

但是數據`[5, 5, 5, 5]`顯然不滿足，所以嘗試對數組約分（除以公共的gcd）
```c++
VECTOR(n, x);
int gcd = __gcd(x[0], x[1]);
for (int i = 2; i < x.size(); i++) gcd = __gcd(gcd, x[i]);
for (int &i: x) i /= gcd;
for (int i = 0; i < x.size(); ++i)
{
    if (x[i] != 1)
    {
        puts("YES");
        for (int j = 0; j < x.size(); ++j)
        {
            if (j == i) cout << 2 << " ";
            else cout << 1 << " ";
        }
        puts("");
        return;
    }
}
puts("NO");
```


## B

## C


# 2108 期 二级

## A



## B

## C

# 2113 期 二级

## A


两种烧烤，一种要A度以上，消耗X度烤一个，一种要B度以上，消耗Y度烤个，现在T度，烤几个


## B


```c++
int a,b,c,d,x1,y1,x2,y2;
cin>>a>>b>>c>>d>>x1>>y1>>x2>>y2;
if(x1!=x2&&y1!=y2) Judge(abs(x1-x2)%c==0||abs(y1-y2)%d==0)
else Judge(abs(x1-x2)%c==0&&abs(y1-y2)%d==0);
```


## C

我的世界挖礦，空氣，金礦，石頭
一個三硝基甲苯會炸掉以自己為中心的2k+1的正方形的區域，石頭和金礦都會消失
但是衹要在爆炸範圍外一圈，可以收集到

給出地圖，求可以收集多少金礦

> ### 解析
> 
> 因為後續空間越來越充裕可以通過微操來控制，所以考慮第一次損失的數量，使用前綴和維護

```c++
int n, m, k, ex = 0x3f3f3f3f3f3fll, sum = 0;
cin >> n >> m >> k;
k = k - 1;
vector a(n + 1, vector<char>(m + 1));
vector qzh(n + 1, vector<int>(m + 1, 0));
for (int i = 1; i <= n; ++i)
    for (int j = 1; j <= m; ++j)
    {
        cin >> a[i][j];
        sum += (a[i][j] == 'g');
        qzh[i][j] = qzh[i - 1][j] + qzh[i][j - 1] - qzh[i - 1][j - 1] + (a[i][j] == 'g');
    }
for (int i = 1; i <= n; ++i)
    for (int j = 1; j <= m; ++j)
        if (a[i][j] == '.')
        {
            int x1 = max(i - k, 1ll), y1 = max(j - k, 1ll), x2 = min(i + k, n), y2 = min(j + k, m);
            ex = min(ex, qzh[x2][y2] - qzh[x2][y1 - 1] - qzh[x1 - 1][y2] + qzh[x1 - 1][y1 - 1]);
        }
cout << sum - ex;
```


# 2119 二級

## A

让a变成b有两种方式
1. 用x代价加一
2. 用y代价和一异或

### 分析
通過嘗試得知：`x奇數^1=x-1  x偶數^1=x+1`

1. 減的方法最困難，當且僅當**奇數**的時候才能做**一次**
2. 加的方法如果異或更划算，也衹能在偶數的時候使用


```c++
int a, b, x, y;
cin >> a >> b >> x >> y;
if (a > b) cout<<((a % 2 == 1 && a - 1 == b)?y:-1);
else if (a == b) cout << 0;
else
{
    if (y < x)
    {
        int sum = 0;
        for (int i = a; i < b; ++i)
            if (i % 2 == 0) sum += y;
            else sum += x;
        cout << sum;
    }
    else cout << (b - a) * x;
}
```


## B


兩個點的座標和一批長度，按照順序的依次走這一批長度从起點到終點

因為不是限定的特殊經過點，所以只需要直線距離到就可以了

## C




2025/7/7

### 題目
> 構造長度為n的數組，滿足全部按位與等於全部按位異或，每一個的範圍`[l,r]`，字典序最小

### 分析
> 1. 當長度為`1`的時候，必定成立
> 2. 全部与是數組的每一位疊加，有就有
> 3. 全部異或就是數組每一位出現奇數次
> 4. 所以如果有奇數个相同的數字，可以滿足每一位出現的時候必定奇數次，這時候選擇`l`

```c++
int n, l, r, k;
cin >> n >> l >> r >> k;
if (n % 2 == 1) cout << l;
else if (n == 2) cout << -1;
else
{
    // TODO :處理偶數的
}
```

## 偶數

```c++
if (f(l) <= r)
{
    if (k > n - 2)cout << f(l);
    else cout << l;
}
else cout<<-1;
```

我就說為什麼1的時候不能直接輸出，要輸入2
原來如此
```c++
ll f(ll n) {
    if (n <= 0) return 1; // 处理非正数
    
    ull t = static_cast<unsigned long long>(n);
    t |= t >> 1;
    t |= t >> 2;
    t |= t >> 4;
    t |= t >> 8;
    t |= t >> 16;
    t |= t >> 32;
    t++;
    int result = static_cast<long long>(t);
    if (result <= 0) return 0;
    return result;
}
```

### 經驗

> 1. 對於數字本身的操作循環是O(1)不要不敢做！！！
> 2. `10^18`不用擔心`long long`溢出！`2^60≈10^18`  `2^63≈8*10^18`
------------

# 題目


说文正在做一个简繁体对照的校订系统，他需要快速找到一段字符串里修改了的部分：

对于字符串`s1`，每一轮会输入一个新的`str`，长度和`s1`：
- 如果`str`长度比`s1`长，说明加上了某一部分，满足效果等效于在`s1[p]`之后插入一个字符串`s2`
- 如果`str`长度比`s1`长，说明减掉了某一部分，满足效果等效于从`s1[p]`位置开始（包括该字符）删除了长度为`l`的片段
- 等效的效果只有上面两种，不会出现删除一部分又加入一部分的情况

每一轮输出算出的`pos`  `s2`/`l`的值
之后更新`s1`为`str`，重复处理，本题为多组输入，输入到`-`为止。

案例：
```
abcde
abghcde
abghe
-
```
输出；
```
1 gh
4 2
```

案例说明：
1. 首先输入`s1`为`abcde`
2. 输入`str`，算出是在`s1[1]` `gh`
3. 输入`abghe`，算出是在`s1[4]` 后面删除了两个字符

保证，在一个字符串的字串sub1的前后，（缺少精准描述）
你可以得出唯一的结果，
不会出现`ab -> abab`、`abab -> ab`、`aba -> ababa`或者`ababa -> aba`的情况出现，







