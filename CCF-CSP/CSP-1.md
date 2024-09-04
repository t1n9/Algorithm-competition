# CSP-第一题(201812-202312)

这是csp历年来的第一题，不算难，特别是以前的题目，完全送分，但是近几年需要转个弯，如果能掌握一些容器、数学素养好一点可能会做得更快，效率更高。

题目描述这里就不贴出来了，可以前往网站查看，完全免费。[CCF认证考试系统](http://118.190.20.162/home.page)

还有一些更早的题目，当时忘记贴上来了，不过比较简单，这里也就不进行更新了。没有解释的题目一般就是秒解的。

## 201812小明上学

```c++
#include<iostream>
using namespace std;
int main() {
	int r, y, g;
	cin >> r >> y >> g;
	int n;
	cin >> n;
	int ans = 0;
	while (n--) {
		int a, b;
		cin >> a >> b;
		if (a != 3)ans += b;
		if (a == 2) {//黄
			ans += r;
		}
	}
	cout << ans;
}
```

## 201903小中大

```c++
#include<iostream>
#include<algorithm>
using namespace std;
int main() {
	int n;
	cin >> n;
	int arr[100001];
	for (int i = 0; i < n; i++)cin >> arr[i];
	sort(arr, arr + n);
	int min = arr[0], max = arr[n - 1];
	double mid;
	if (n % 2)mid = arr[n / 2];
	else {
		mid = ((double)arr[n / 2] + (double)arr[n / 2 - 1]) / 2;
	}
	if(mid!=floor(mid))
		printf("%d %.1f %d", max, mid, min);
	else printf("%d %d %d", max, int(mid), min);
}
```

## 201909小明种苹果

简单将数据输入，将最大值进行保存，比较更新即可。

```c++
#include<iostream>
using namespace std;
int num[1000000];
int main() {
	int n, m;
	cin >> n >> m;
	int max_num, max_del = 0, sum = 0;
	for (int i = 1; i <= n; i++) {
		cin >> num[i];
		int del = 0;
		for (int j = 0; j < m; j++) {
			int a; cin >> a;
			num[i] += a;
			del -= a;
		}
		sum += num[i];
		if (max_del < del) {
			max_del = del;
			max_num = i;
		}
	}
	cout << sum << ' ' << max_num << ' ' << max_del;
}
```

## 201912报数

```c++
#include<iostream>
using namespace std;
int num[4] = { 0 };
bool pass(int x) {
	if (x % 7 == 0)return true;
	while (x > 0) {
		if (x % 10 == 7)return true;
		x /= 10;
	}
	return false;
}
int main() {
	int n; cin >> n;
	for (int i = 1,j=1; j <= n; i++) {
		if (pass(i))num[(i - 1) % 4]++;
		else j++;
	}
	for (int i = 0; i < 4; i++)
		cout << num[i] << endl;
}
```

## 202006线性分类器

刚开始一直在想是否由点和线的映射关系，但是一直没想出来，网上查了都是用最水的方法，完全模拟出来的，一点没有思考的痕迹。最后我想到可以用比较y轴交点的方法来做，结合set的特性一下就解出来了。

```c++
#include<iostream>
#include<unordered_set>
using namespace std;
struct Dot {
	int x, y;
	int z;
	char type;
}d[1001];
int main() {
	int n, m;
	cin >> n >> m;
	for (int i = 0; i < n; i++) {
		cin >> d[i].x >> d[i].y >> d[i].type;
	}
	while (m--) {
		int a, b, c; cin >> a >> b >> c;
		unordered_set<char>up, down;
		for (int i = 0; i < n; i++) {
			if (b * d[i].x + c * d[i].y > -a)
				up.insert(d[i].type);
			else down.insert(d[i].type);
		}
		if (up.size() > 1 || down.size() > 1)cout << "No\n";
		else cout << "Yes\n";
	}
}
```

## 202009称检测点查询

排序问题

```c++
#include<iostream>
#include<math.h>
#include<algorithm>
using namespace std;
struct Point {
	int no;
	double dis;
}p[201];

bool cmp(Point x, Point y) { 
	if (x.dis != y.dis)return x.dis < y.dis;
	else return x.no < y.no;
}
int main() {
	int n;
	double x, y;
	cin >> n >> x >> y;
	for (int i = 0; i < n; i++) {
		double a, b;
		cin >> a >> b;
		p[i].no = i + 1;
		p[i].dis = sqrt(pow(x - a, 2) + pow(y - b, 2));
	}
	sort(p, p + n, cmp);
	for (int i = 0; i < 3; i++) {
		if (i)cout << endl;
		cout << p[i].no;
	}
}
```

## 202012期末预测之安全指数

简单

```c++
#include<iostream>
#include<math.h>
using namespace std;
int main() {
	int n;
	cin >> n;
	int ans = 0;
	while (n--) {
		int a, b;
		cin >> a >> b;
		ans += a * b;
	}
	cout << max(ans, 0);
}
```

##  202104灰度直方图

简单

```c++
#include<iostream>
using namespace std;
int num[256] = { 0 };
int main() {
	int n, m, k;
	cin >> n >> m >> k;
	for (int i = 0; i < n; i++) {
		for (int j = 0; j < m; j++) {
			int a; cin >> a;
			num[a]++;
		}
	}
	for (int i = 0; i < k; i++) {
		if (i)cout << ' ';
		cout << num[i];
	}
}
```

## 202109数组推导

简单

```c++
#include<iostream>
using namespace std;
int arr[10000];
int main() {
	int n; cin >> n;
	for (int i = 0; i < n; i++)cin >> arr[i];
	int Min, Max, pre;
	Min = Max = arr[0];
	for (int i = 1; i < n; i++) {
		if (arr[i] == arr[i - 1])Max += arr[i];
		else { Min += arr[i]; Max += arr[i]; }
	}
	cout << Max << endl << Min;
}
```

## 202112序列查询

根据样例信息即可。

```c++
#include<iostream>
using namespace std;
int arr[10000001];
int main() {
	int n,m;
	cin >> n >> m;
	for (int i = 0; i < n; i++) {
		int a; cin >> a;
		arr[a] = 1;
	}
	arr[0] = 0;
	int ans = 0;
	for (int i = 1; i < m; i++) {
		if (arr[i] == 1)arr[i] = arr[i - 1] + 1;
		else arr[i] = arr[i - 1];
		ans += arr[i];
	}
	cout << ans;
}
```

## 202203未初始化警告

简单查找

```c++
#include<iostream>
#include<unordered_set>
using namespace std;
int main() {
	unordered_set<int>s;
	int ans = 0;
	int n, k; cin >> n >> k;
	s.insert(0);
	while (k--) {
		int a, b;
		cin >> a >> b;
		if (!s.count(b))ans++;
		s.insert(a);
	}
	cout << ans;
}
```

## 202206归一化处理

数学计算，按照过程进行即可

```c++
#include<iostream>
#include<math.h>
using namespace std;
double arr[1001];
int main() {
	int n; cin >> n;
	double aver = 0, bzdiff = 0;
	for (int i = 0; i < n; i++) {
		cin >> arr[i];
		aver += arr[i];
	}
	aver /= n;
	for (int i = 0; i < n; i++) {
		bzdiff += pow(arr[i] - aver, 2);
	}
	bzdiff /= n;
	bzdiff = sqrt(bzdiff);
	for (int i = 0; i < n; i++) {
		printf("%f\n", (arr[i] - aver) / bzdiff);
	}
}
```

## 202209如此编码

题目看着难，但是跟着解释就可以发现一些思路，不断求商再减去，重复即可从后往前得出答案。

```c++
#include<iostream>
#include<math.h>
using namespace std;
int arr[21], c[21], ans[21];
int main() {
	int n, m;
	cin >> n >> m;
	for (int i = 0; i < n; i++)cin >> arr[i];
	c[0] = 1;
	for (int i = 1; i < n; i++) {
		c[i] = arr[i - 1] * c[i - 1];
	}
	for (int i = n - 1; i >= 0; i--) {
		ans[i] = m / c[i];
		m -= ans[i] * c[i];
	}
	for (int i = 0; i < n; i++) {
		if (i)cout << ' ';
		cout << ans[i];
	}
}
```

## 202212 现值计算

还是数学问题，正着不行，反过来咯，结果下标为0的才是现在的年份。好吧，最后就是普通的计算求和，秒了。

```c++
#include<iostream>
#include<math.h>
using namespace std;
int main() {
	int n; double k;
	cin >> n >> k;
	double ans;
	for (int i = 0; i <= n; i++) {
		double a; cin >> a;
		if (i == 0) { ans = a; continue; }
		ans += a * pow(1 + k, -i);
	}
	cout << ans;
}
```

##  202303田地丈量

若已有田地是落在方格中，那其重叠部分左下角坐标(0<x<x0,0<y<y0)，右上角坐标也一样，以此将重叠部分的左下右上坐标进行更新，最后计算求和即可。刚开始没想出来，用最土的方法结果情况没考虑全，没得分。

```c++
#include<iostream>
#include<math.h>
using namespace std;
int main() {
	int n, x, y;
	cin >> n >> x >> y;
	int ans = 0;
	for (int i = 0; i < n; i++) {
		int a, b, c, d;
		cin >> a >> b >> c >> d;
		a = min(max(0, a), x);
		b = min(max(0, b), y);
		c = min(max(0, c), x);
		d = min(max(0, d), y);
		ans += (c - a) * (d - b);
	}
	cout << ans;
}
```

## 202305重复局面

用map做，检查是否出现过，二值用来存出现的次数，num数组用来当前情况是第几次出现。最后按序输出num即可。

```c++
#include<iostream>
#include<unordered_map>
using namespace std;
unordered_map<string, int>M;
int num[101];
int main() {
	int n; cin >> n;
	for (int i = 0; i < n; i++) {
		string s = "";
		for (int i = 0; i < 8; i++) {
			string s1; cin >> s1;
			s += s1;
		}
		if (M.find(s) == M.end()) {
			M[s] = 1;
			num[i] = 1;
		}
		else {
			M[s]++;
			num[i] = M[s];
		}
	}
	for (int i = 0; i < n; i++) {
		if (i)cout << endl;
		cout << num[i];
	}
}
```

## 202309坐标变换（其一）

将变换的过程整合，最后将输入坐标和变换过程进行相加即可。

```c++
#include<iostream>
using namespace std;
int main() {
	int n, m;
	cin >> n >> m;
	int x = 0, y = 0;
	for (int i = 0; i < n; i++) {
		int a, b;
		cin >> a >> b;
		x += a; y += b;
	}
	while (m--) {
		int a, b;
		cin >> a >> b;
		cout << a + x << ' ' << b + y << endl;
	}
}
```

## 202312仓库规划

废了好大劲，主要还是想要用排序来做，不想暴力从头排到尾，但是这貌似是最好的方法了，有时候不要一直想着如何用招式来解决，朴素地快速地解决也是好的方法。

```c++
#include<iostream>
using namespace std;
int n, m;
struct Store {
	int no;
	int boos;
	int val[10];
}s[1001];
int main() {
	cin >> n >> m;
	for (int i = 1; i <= n; i++) {
		s[i].no = i;
		for (int j = 0; j < m; j++)cin >> s[i].val[j];
	}
	for (int i = 1; i <= n; i++) {
		int flag = 0, j;
		for (j = 1; j <= n; j++) {
			if (i == j)continue;
			flag = 0;
			int k;
			for (k = 0; k < m; k++) {
				if (s[i].val[k] < s[j].val[k]) {
					continue;
				}
				else {
					break;
				}
			}
			if (k == m) {
				flag = 1; break;
			}
		}
		if (flag)s[i].boos = s[j].no;
		else s[i].boos = 0;
	}
	for (int i = 1; i <= n; i++) {
		if (i!=1)cout << endl;
		cout << s[i].boos;
	}
}
```

