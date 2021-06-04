AVL树，即平衡二叉搜索树，当一棵二叉搜索树的左右子树高度相差(平衡因子)小于等于1时，我们称其为平衡二叉搜索树。  
当一棵二叉搜索树在插入数据时平衡被打破，我们需要手动调整树的节点使其重新满足平衡二叉搜索树的性质。  
# 平衡二叉树的基本操作
平衡二叉搜索树的操作有两种：左旋和右旋
![QQ截图20201120193947.png](https://i.loli.net/2020/11/20/RheqYg9k6S3tKEj.png)
## 右旋
- 具体步骤
    1. 使用临时变量保存根节点(旋转节点)的左子树
    2. 将根节点的左子树设置为左子树的右子树
    3. 将之前保存下来的左子树的右子树设置为根节点。
    4. 更新根节点以及该节点左子树的高度(顺序不能错，因为此时根节点已经成为了原先左子树的右子树)。
    5. 将根节点设置为临时保存下来的左子树
- 代码
```cpp
void R(int &u)
{
    int p=l[u];
    l[u]=r[p],r[p]=u;
    update(u),update(p);//更新高度。
    u=p;
}
```
## 左旋
步骤与右旋相反
- 代码
```cpp
void R(int &u)
{
    int p=r[u];
    r[u]=l[p],l[p]=u;
    update(u),update(p);//更新高度。
    u=p;
}
```

# 平衡二叉树的失衡情形以及对应解决方法
使平衡二叉树失去平衡主要有四种情形:  
1. 左子树比右子树高2
    1. 左子树的左子树比左子树的右子树高1
    2. 左子树的右子树比左子树的左子树高1
2. 右子树比左子树高2
    1. 右子树的右子树比右子树的左子树高1
    2. 右子树的左子树比右子树的右子树高1
![QQ截图20201120200144.png](https://i.loli.net/2020/11/20/kCGn3Fec2E4aAMb.png)  
  
上面四种情况从上往下分别对应图中的1、3、2、4。  
解决方法为:  
1. 
    1. R(root)
    2. L(l[root]), R(root)
2.
    1. L(root)
    2. R(r[root]), L(root)
> 这里的root指的是左右不平衡的节点(平衡因子大于2或小于-2)

# 实战
## AVL树的根
AVL树是一种自平衡二叉搜索树。  
在AVL树中，任何节点的两个子树的高度最多相差 1 个。  
如果某个时间，某节点的两个子树之间的高度差超过 1，则将通过树旋转进行重新平衡以恢复此属性。  
现在，给定插入序列，请你求出 AVL 树的根是多少。  

### 输入格式
第一行包含整数 N，表示总插入值数量。

第二行包含 N 个不同的整数，表示每个插入值。

### 输出格式
输出得到的 AVL 树的根是多少。

### 数据范围
1≤N≤20
### 输入样例1：
5  
88 70 61 96 120
### 输出样例1：
70
### 输入样例2：
7  
88 70 61 96 120 90 65
### 输出样例2：
88

## AC代码
```
#include<iostream>
#include<cstring>
using namespace std;
const int N = 30;
int l[N], r[N], e[N], idx;//记录二叉树信息
int h[N];//记录节点高度
int n;
void update(int u)
{
	h[u] = max(h[l[u]], h[r[u]]) + 1;
}

int get_balance(int u)
{
	return h[l[u]] - h[r[u]];
}

void R(int& u)
{
	int p = l[u];
	l[u] = r[p];
	r[p] = u;
	update(u), update(p);
	u = p;
}

void L(int& u)
{
	int p = r[u];
	r[u] = l[p];
	l[p] = u;
	update(u), update(p);
	u = p;
}

void insert(int& u,int val)
{
	if (u == -1)e[idx] = val, u = idx++;
	else if (val < e[u])
	{
		insert(l[u], val);
		if (get_balance(u) == 2)
		{
			if (get_balance(l[u]) == 1)R(u);
			else L(l[u]),R(u);
		}
	}
	else
	{
		insert(r[u], val);
		if (get_balance(u) == -2)
		{
			if (get_balance(r[u]) == -1)L(u);
			else R(r[u]),L(u);
		}
	}
	update(u);
}

int main()
{
	memset(l, -1, sizeof(l));
	memset(r, -1, sizeof(r));
	int root = -1;
	cin >> n;
	int a;
	while (n--)
	{
		cin >> a;
		insert(root, a);
	}
	cout << e[root];
}
```