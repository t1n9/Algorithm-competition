# PAT

## STL(standard template library)标准库

### vector

可以**存放任意类型的动态数组**，能够增加和压缩数据

可以使用[]**下标**的方式访问其中数据

```c++
assign新内容覆盖就内容并调整size
size()返回大小
push_back(i)尾插
pop_back()尾删
insert(it,x)任意位置插入，it为迭代器位置
erase(it)任意位置删除
erase(first,last)删除区间元素，一样都是迭代器
swap和另一个vector交换数据
clear()清空数据
```

### set

通过红黑树自动递增，不含重复元素的**集合**

```c++
set<int>S;
S.insert();插入，且自动排序去重
S.find(value);返回值为value迭代器
S.erase(value);删除值为value的元素
S.erase(firse,last);删除first到last迭代器之间的内容
S.size();返回大小
S.clear();清空
//遍历元素可以通过迭代器，也可以通过:
for(set<int>iterator it=S.begin();it!=S.end();it++){
    cout<<*it;
}
for(int i:S){
    cout<<i;
}
```

### unordered_set

通过哈希表实现，不排序

```c++
unordered_set<int> S;
S.insert(i);//插入元素
S.count(i);//查找元素是否存在，不存在则返回0
S.find(i);//查找元素下标，不存在则返回末位元素
S.erase(i);//删除i元素
```



### map

映射，通过红黑树，按照键key的大小进行排序

```c++
map<char,int>M;
M['a']=1;
M.find('a');返回的是迭代器
//迭代器可通过->first,->second来访问key和value
M.erase(it);删除迭代器//可先find找到，然后放到括号里面
M.erase(key);删除映射的键值
M.erase(first,last);删除first到last之间的迭代器
M.size();返回大小
M.clear();清空
```

①字符串与整数之间映射<string,int>

②字符串与可变数组之间的映射<string,set<int>>

③建立映射，可用来统计数量，

```c++
map<type,int>M;
M[name]++;
遍历：
    for(map<type,int>::iterator it=M.begin();it!=M.end();it++)
        //通过访问first和second来操作
```

### unordered_map

哈希实现，只处理映射，不处理排序，比map快。

```c++
unordered_map<int,string>M;
//插入元素：
M.insert({1,"one"});//使用键值对插入
M.emplace(2,"two");//原地构造键值对后插入
//访问元素：
M[3];//返回空字符串
M.at(3);//抛出异常
//元素存在情况下，两种操作都能正常返回value
//删除元素
M.erase(2)//删除键为2的元素
//查找、查询
M.find(2);//返回键为2的迭代器
M.count(2);//若元素存在返回1，否则返回0
```

### queue

**队列**先进先出

```c++
queue<int>Q;
//访问
Q.front();Q.back();
//入队出队
Q.push();Q.pop();
//检测
Q.empty();//为空则返回true
Q.size();//返回大小
```

使用front()和pop()之前，先用empty()检查是否为空

### priority_queue

**优先队列**：头文件与queue一致，插入、删除、查看都会依照优先级进行排序

```c++
priority_queue<int>Q;
//访问只能通过top
Q.top();//队首是优先级最高的元素
//其他操作与普通queue一致
//注意每次插入都会进行排序，复杂度log(n)
//排序
默认按照各种类型的数据进行排序
如：int类型按照数字大小排序，char按照字典排序；
自定义结构体，需要重载'<'小于运算符
```

### stack

**栈**：后进先出；常用在递归

```c++
push()/pop()/top()/empty()/size()
```

### pair

需要头文件<utility>，<map>有包含。

相当于有两个元素的结构体。

```c++
pair<int,char>P;
p.first=1;p.second='c';
//两个pair比较大小
//先比较first，若first比较不出来，再比较second
//常用：
map<string,int>M;
M.insert(mak_pair("aaa",111));//插入键值对
M.insert(pair<string,int>("bbb",222));//也可以
```

### algorithm头文件下的操作

```c++
max(a,b)、min(a,b);//返回最大最小值，三个数可以max(a,max(b,c))
abs((int)a)、fabs((flaot)a);//绝对值，整形用前者，浮点型添加头文件math用后者
swap(a,b);//交换
fill(it1,it2,value);//对数组或容器的某一区间赋相同值
sort();//排序

```

```c++
reverse(it1,it2);//将it1和it2之间的元素或迭代器反转
eg:reverse(s.begin()+2,s.begin()+6);
```

```c++
next_permutation();//给出一个序列在全排列中的下一个序列
eg:int a[6]={1,2,3,4,5,6};
do{
    cout<<a[0]<<a[1]<<a[2]<<' ';
}while(next_permutation(a,a+3));
//输出：123 132 213 231 312 321
```

```c++
lower_bound(it1,it2,value);
upper_bound(it1,it2,value);
//查找it1到it2之间value存在的话所处的位置
//数组返回指针，容器返回迭代器
int a[10]={1,2,2,3,3,3,5,5,6,7};
int *lowerPos=lower_bound(3);//返回a+3
int *upperPos=upper_bound(3);//返回a+6
int *lowerPos=lower_bound(4);//返回a+6，此时元素不存在，与upper返回地址相同，是其若存在则应该处在的位置
```

## 二叉查找树insert插入

其**插入过程**与此树最终的**先根遍历**是一样的；

此树最终的<u>中序遍历</u>是<u>有序</u>的。

```c++
void insert(Node*&root,int data) {
	if (root == NULL) {//找到插入的位置
		root = new Node;
		root->val = data;
		root->left = root->right = NULL;//未知风险，最好写上
		return;
	}
	if (root->val > data)insert(root->left, data);
	else insert(root->right, data);
}
```



## 最短路径DFS求法

通常要求距离最短，加上某个变量的多少来确定唯一路径。

下面要求s城市到d城市距离最短，cost消耗最少的路径。

通常用vector来记录全部邻接信息，若需要记录走过的路，可用path记录，当条件符合更新路径时，将final_path更新为当前path。

过程中涉及到的各种判断，根据题目来判断。

若需要统计路径最短的相同路径数，则需要在到达目的城市后，判断距离是否相同，同则路径数加一，否则路径数归一。

用min_dis来记录到达此城市的最短距离，不需要写visited，注意前期赋高值，中期更新，最后判断即可。

```c++
#include<iostream>
#include<vector>
using namespace std;
int n, m, s, d;
vector<int>v[501], path, final_path;
int min_dis[501], min_cost = 1000000;
int cost[501][501], dis[501][501];

void dfs(int cur_city, int cur_dis, int cur_cost) {
    if (min_dis[cur_city] < cur_dis)return;
    path.push_back(cur_city);
    if (cur_city == d) {
        if (cur_dis < min_dis[d] || (cur_dis == min_dis[d] && min_cost > cur_cost)) {
            final_path = path;
            min_cost = cur_cost;
            min_dis[d] = cur_dis;
        }//refresh
    }
    else {
        if (min_dis[cur_city] > cur_dis)min_dis[cur_city] = cur_dis;
        for (int i : v[cur_city]) {
            dfs(i, cur_dis + dis[cur_city][i], cur_cost + cost[cur_city][i]);
        }
    }
    path.pop_back();
}

int main() {
    cin >> n >> m >> s >> d;
    while (m--) {
        int a, b, c, cc;
        cin >> a >> b >> c >> cc;
        v[a].push_back(b);
        v[b].push_back(a);
        dis[a][b] = dis[b][a] = c;
        cost[a][b] = cost[b][a] = cc;
    }//
    for (int i = 0; i < n; i++)min_dis[i] = 1000000;
    dfs(s, 0, 0);
    for (int i = 0; i < final_path.size(); i++) {
        cout << final_path[i] << ' ';
    }
    cout << min_dis[d] << ' ' << min_cost << endl;
}
```

