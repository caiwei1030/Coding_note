- # 栈、队列、STL学习

### 全排列用法

- 计算序列全排列的函数(头文件`#include<algorithm>`）

`next_permutation（start,end）`和`prev_permutation（start,end）`。

- 两个函数作用是一样，区别就在于前者求的是当前排列的下一个排列，后一个求的是当前排列的上一个排列。

- 当前序列不存在下一个排列时，函数返回false，否则返回true。

- 函数实际会改变迭代器内（如数组）元素的顺序。

- 函数会将 `[first, last)` 范围内的元素重新排列为下一个字典序更大的排列。

  #### **练习题A**

[A-老子的全排列呢_牛客竞赛语法入门班数组栈、队列和stl习题](https://ac.nowcoder.com/acm/contest/19850/A)

```c++
`#include<bits/stdc++.h>`
`using namespace std;`

`int main(){`
    `int num[]={1,2,3,4,5,6,7,8};`
    `do{`
        `for(int i=0;i<8;i++){`
            `cout<<num[i];`
            `if(i!=7){`
                `cout<<" ";`
            `}`
        `}`
        `cout<<endl;`
        
    `}while(next_permutation(num,num+8));`
    `return 0;`
`}`
```

- > [!NOTE]
  >
  > **为什么用 `do-while`？**
  >
  > 因为 `next_permutation` 在调用时会生成下一个排列。如果使用 `while`，初始排列会被跳过。

[wnm的全排列](https://ac.nowcoder.com/acm/problem/24647)

```
#include<bits/stdc++.h>
using namespace std;

int main(){
    int t;
    cin>>t;
    int tmp=t;
    while(t--){
        string str;
        cin>>str;
        int n;
        cin>>n;
        //可排序数的数量是阶乘数
        int fact=1;
        for(int i=1;i<=str.length();i++){
            fact*=i;
        }        
        //要求结果大于可排序数
        if(n>fact){
            cout<<"Case "<<tmp-t<<": no solution"<<endl;
        }else{
            sort(str.begin(),str.end());
            //全排列第n次
            while(--n){
                next_permutation(str.begin(),str.end());
            }
           //如何除去前导0？
            cout<<"Case "<<tmp-t<<": "<<stoi(str);
            cout<<endl;
        }
    }       
    return 0;
}
```

> [!NOTE]
>
> **字符串输出时如何解决前导0问题？**
>
> C++中， stoi() 是一个标准库函数，用于将字符串（ `*std::string*` 或 C 风格字符串）转换为整数（ int）。
>
> 这个函数定义在 <string> 头文件中。是 C++11 引入的一个标准库函数，用于**将字符串转换为整数**。
>
> 与 atoi() 不同，stoi() 提供了更强的功能，包括错误处理、支持指定进制等。
>
> stoi()会自动省略前导0。



### **cin的小技巧**

- `ios::sync_with_stdio(false);`
- `cin.tie(0); cout.tie(0);`
- 可以将cin和scanf的效率相匹敌
- cin，cout之所以效率低，是因为先把要输出的东西存入缓冲区，再输出，导致效率降低，而这段代码可以来打消iostream的输入 输出缓存，可以节省许多时间，使效率与scanf与printf相差无几.
- 相当于把C++的输入输出速度提高到与C相同。

### vector用法

- 序列式容器 : 序列式容器的元素排列的顺序与元素本身无关 , 其先后顺序**由元素添加到容器中的顺序决定** ;

- 常用的序列式容器 : C++ 的 STL ( 标准模板库 ) , 包括 vector ( 向量 ) , list ( 列表 ) , queue ( 队列 ) , dequeue ( 双向队列 ) , stack ( 栈 ) , priority_queue ( 优先队列 ) ;

- **vector , dequeue , list 调用方式基本一致 , 这里只研究 vector 一种 ;**

- 声明 vector ( 基本用法 ) : 格式 " vector <元素类型名称> 容器名称 ; 

  ```
  //声明向量
  vector<int> vector_1;
  ```

- 声明 vector ( 指定容量 ) : 调用构造方法 , 并传入 int 类型参数 , 该参数就是 vector 容器的元素个数 ;

  ```
  //调用向量的构造方法 , 并传入一个 int 类型参数
    //表示创建一个有 8 个 int 类型元素空间的向量
    vector<int> vector_2(8);
  ```

  声明 vector ( ① 指定容量 ② 初始化内容 ) : 调用构造方法 , 传入 2 个参数 ;

① 容量 : 第一个参数是 vector 容量 ;
② 元素 : 第二个参数是 vector 中初始化的元素内容 ;

```
	//表示创建有 8 个元素的向量 , 8 个元素的值都是 2
	vector<int> vector_3(8 , 2);
```

声明 vector ( 使用另外 vector 初始化 ) : 调用构造方法 , 传入vector 对象 ;

```
//初始化向量时 , 传入另一个向量
vector<int> vector_4(vector_3);
```

**vector ( 向量 ) 添加元素**

添加元素 : 调用 **push_back** 方法 , 容器出入策略 , **后进先出** ;

	// ( 1 ) 增加元素 : 调用 push_back 方法 , 容器出入策略, 后进先出
	vector_1.push_back(8);
	vector_1.push_back(88);
**vector ( 向量 ) 查询元素**

1. 通过**下标**获取元素 : 使用格式 " vector 变量名称 [ 下标索引 ] " , 这里的 [] 在 vector 中进行了运算符重载 ;

  ```
  // <1> 通过下标获取元素
  //	这里的 [] 在 vector 中进行了运算符重载
  cout << "通过下标获取 vector_1 第 0 个元素 : vector_1[0] : " << vector_1[0] << endl;
  ```

2. 通过 **at() 方法**获取对应索引的元素 ;

  ```
  // <2> 通过 at() 方法获取对应索引的元素
  cout << "通过 at 方法获取 vector_1 第 0 个元素 : vector_1.at(0) : " << vector_1.at(0) << endl;
  ```

3. 获取**vector.front()**获取向量第一个元素 ;

  ```
  // <3> 获取第一个元素
  cout << "通过 front 方法获取 vector_1 第 1 个元素 : vector_1.front() : " << vector_1.front() << endl;
  ```

4. 获取**vector.back()**最后一个元素 ;

  ```
  // <4> 获取最后一个元素
  cout << "通过 back 方法获取 vector_1 最后 1 个元素 : vector_1.back() : " << vector_1.back() << endl;
  ```

**vector ( 向量 ) 删除元素**

1. 删除最后加入的元素 : 调用 pop_back 方法 , 容器出入策略 , 后进先出 ; 

  注意这里并没有修改 vector 容量大小 , 只是将最后的元素清空了 ;

  ```
  // <1> 调用 pop_back 方法 , 容器出入策略 , 后进先出
  vector_1.pop_back();
  ```

2. 删除所有元素 , 这里只是清空元素内容为 0

  ```
  // <2> 删除所有元素 , 这里只是清空元素内容为 0
  vector_1.clear();
  ```

3. 删除指定位置区间的元素 , 这里只是清空元素内容为 0 , 传入 2 个参数 ;

① 第 1 个是删除的起始位置 ;
② 第 2 个参数是删除的结束位置 ;

```
	// <3> 删除指定位置区间的元素 , 这里只是清空元素内容为 0
	//		第 1 个是删除的起始位置 , 
	//		第 2 个参数是删除的结束位置 ;
	//删除从开始到结束的所有元素
	vector_1.erase(vector_1.begin() , vector_1.end());
```



4. 关于删除元素的内存说明 : 删除若干元素后 , vector 的容量 , 即内存所占的空间是不会减小的 ;

5. 打印删除元素后的 vector 容器大小 : 调用 vector 的 capacity() 方法即可获取其容量大小 ;

① 代码示例 :

```
	//打印 vector 容器容量大小 , 调用 vector 的 capacity() 方法即可获取其容量大小
	//	这个容量大小是元素个数 , 不是内存字节数
	cout << "打印 vector_1 容量大小 : vector_1.capacity() : " << vector_1.capacity() << endl;
```

② 执行结果 :
 vector_1 容量大小 : `vector_1.capacity()` 
这个容量大小是元素个数 , 不是内存字节数 ;vector ( 向量 ) 容量改变

1. 容量修改 : 删除元素 , 并不能修改容器的容量 , 如果要修改容量 , 需要使用其他容器与该容器进行交换 ;

2. 容器交换 : 调用 vector 的 swap() 方法 , 进行容器交换 , 传入 vector 容器对象当做参数 ;

① 代码示例 :

```
	//创建一个新的 vector , 此时其容量为 0
	vector<int> vector_swap;
	//将创建的新的 vector_swap 与 vector_1 容器进行交换
	vector_swap.swap(vector_1);
	cout << "打印 vector_1 交换后的容量大小 : vector_1.capacity() : " << vector_1.capacity() << endl;
```

② 执行结果 :
打印 vector_1 交换后的容量大小 : vector_1.capacity() : 0


vector ( 向量 ) 涉及到的运算符重载

**vector 运算符重载 : 使用 " [] " 可以访问 vector 中指定索引的变量** 

    _NODISCARD _Ty& operator[](const size_type _Pos) {
        auto& _My_data = _Mypair._Myval2;
    #if _CONTAINER_DEBUG_LEVEL > 0
            _STL_VERIFY(
                _Pos < static_cast<size_type>(_My_data._Mylast - _My_data._Myfirst), "vector subscript out of range");
    #endif // _CONTAINER_DEBUG_LEVEL > 0
    
        return _My_data._Myfirst[_Pos];
    }
#### 练习题B

[B-装进肚子_牛客竞赛语法入门班数组栈、队列和stl习题](https://ac.nowcoder.com/acm/contest/19850/B)

```
#include<bits/stdc++.h>

using namespace std;

const int maxn=1e5+1;
int a[maxn],b[maxn];
int diff[maxn];//早晚甜蜜值差值

int main(){
    int n,k;
    long long sum=0;
    cin>>n>>k;
    for(int i=0;i<n;i++)cin>>a[i];
    for(int i=0;i<n;i++){
        cin>>b[i];
        sum+=b[i];
    }
    //计算早晚甜蜜度差值
   for(int i=0;i<n;i++){
       diff[i]=a[i]-b[i];
   }
    sort(diff,diff+n,greater<int>());
    for(int i=0;i<k;i++){
        sum+=diff[i];
    }
    cout<<sum;
    return 0;
}
```

> [!NOTE]
>
> **贪心**
>
> 计算早晚甜蜜度差值，将其按高到低重新排序。以晚上甜蜜度为基准，求和所有晚上甜蜜度，再将差值由高到低相加前k个即可。

### sort函数

- sort()函数可以对给定区间所有元素进行排序。三个参数`sort(begin, end, cmp)`，其中begin为指向待sort()的数组的第一个元素的指针，end为指向待sort()的数组的最后一个元素的下一个位置的指针，cmp参数为排序准则。
- cmp参数默认从小到大进行排序。
- 从大到小排序可以将cmp参数写为`greater<int>()`就是对int数组进行排序，<>中也可以写double、long、float等。
- 如果需要按照其他的排序准则，需要定义一个bool类型的函数来传入。

**按照每个数的个位进行从大到小排序**

```
bool cmp(int x,int y){
	return x % 10 > y % 10;
}
```

**对结构体进行排序**
 **sort()也可以对结构体进行排序。**

定义一个结构体含有学生的姓名和成绩的结构体Student，然后我们按照每个学生的成绩从高到底进行排序。

```
struct Student{
	string name;
	int score;
	Student() {}
	Student(string n,int s):name(n),score(s) {}
};
```

根据排序要求我们可以将排序准则函数写为：

```
bool cmp_score(Student x,Student y){
	return x.score > y.score;
}
```

比如每一个学生有四科成绩，我们需要根据学生的四科成绩的平均分高低进行排名，那么这个cmp函数我们就可以定义为：

```
bool cmp_score(Student x,Student y){
	double average_x,average_y;
	average_x = (x.score[0]+x.score[1]+x.score[2]+x.score[3])/4;
	average_y = (y.score[0]+y.score[1]+y.score[2]+y.score[3])/4;
	return average_x > average_y;
}
```

**关于值传递与引用传递**
 在以上的代码示例中使用了值传递，使用值传递每次调用函数时都会创建Student对象的副本，会增加额外的开销也会降低排序的效率。最好使用引用传递。使用引用传递的好处：

- 避免拷贝开销：值传递会创建参数的副本，对于大型对象或复杂数据结构，这可能涉及大量的内存分配和数据复制。引用传递避免了这些操作，因为它直接操作原始对象。

- 提高执行效率：由于避免了拷贝操作，函数调用的执行速度会更快，尤其是在处理大型数据或在需要频繁调用函数的情况下。

- 减少内存使用：引用传递不涉及额外的内存分配，因此可以减少程序的内存占用。

- 允许修改原始数据：引用传递允许函数直接修改原始数据，这在某些情况下非常有用，比如在排序函数中修改对象的内部状态。

- 保持数据一致性：引用传递确保函数内部对数据的任何修改都会反映到原始数据上，这有助于保持数据的一致性。


所以我们可以对以上的排序方法进行优化：

```
bool cmp_score(const Student& x, const Student& y) {
    double average_x = (x.score[0] + x.score[1] + x.score[2] + x.score[3]) / 4;
    double average_y = (y.score[0] + y.score[1] + y.score[2] + y.score[3]) / 4;
    return average_x > average_y;
}
```

#### 练习题C-D

[C-牛牛的三角形_牛客竞赛语法入门班数组栈、队列和stl习题](https://ac.nowcoder.com/acm/contest/19850/C)

```
#include<bits/stdc++.h>
using  namespace std;

int main(){
    int n;
    cin>>n;
    //不足三个元素
    if(n<3){
        cout<<"No solution";
        return 0;
    }
    vector<int> a(n);
    for(int i=0;i<n;i++){
        cin>>a[i];
    }
    //对三角元素进行排序
    sort(a.begin(),a.end());
    for(int i=2;i<n;i++){
    //构成三角形，两边之和大于第三边
        if(a[i-2]+a[i-1]>a[i]){
            cout<<a[i-2]<<" "<<a[i-1]<<" "<<a[i];
            return 0;
        }
    }
    cout<<"No solution";
    return 0;
}
```

[D-[NOIP1998\]拼数_牛客竞赛语法入门班数组栈、队列和stl习题](https://ac.nowcoder.com/acm/contest/19850/D)

```
#include<bits/stdc++.h>
using namespace std;

//拼接字符串，保证联成一排整数最大
bool cmp(string str1,string str2){
    return str1+str2>str2+str1;
}

int main(){
    int n;
    cin>>n;
    string str[n];
    for(int i=0;i<n;i++){
        cin>>str[i];
    }
    sort(str,str+n,cmp);
    for(int i=0;i<n;i++){
        cout<<str[i];
    }
    return 0;
}
```

> [!NOTE]
>
> **字符串拼接如何比较大小？**
>
> 使用“+‘‘可实现字符串拼接，字符串可以直接比较大小，无需转换为整形



### 字符串

由单引号括起来的一个字符被称作 char 型。

双引号括起来的零个或多个字符则构成字符串型。

**编译器在每一个字符串后面添加一个空字符（'\0'）**，因此**字符串的实际长度要比他的内容多1。**

如字面值 'A' 表示的就是单独字符 A ，而字符串 "A" 代表了一个包含两个字符的字符数组，分别是字母 A 和空字符。

**1、定义一个字符串**
使用标准库类型 string 声明并初始化一个字符串，需要包含头文件 string。可以初始化的方式如下：

    string s1;    // 初始化一个空字符串
    string s2 = s1;   // 初始化s2，并用s1初始化
    string s3(s2);    // 作用同上
    string s4 = "hello world";   // 用 "hello world" 初始化 s4，除了最后的空字符外其他都拷贝到s4中
    string s5("hello world");    // 作用同上
    string s6(6,'a');  // 初始化s6为：aaaaaa
    string s7(s6, 3);  // s7 是从 s6 的下标 3 开始的字符拷贝
    string s8(s6, pos, len);  // s7 是从 s6 的下标 pos 开始的 len 个字符的拷贝
**2、读写 string 操作**
输入时遇到空格或回车键将停止。

注意**只有按下回车键时才会结束输入执行，当按下空格后还能继续输入**

- 单字符串输入，读入字符串，遇到空格或回车停止；
- 多字符串的输入，遇到空格代表当前字符串赋值完成，转到下个字符串赋值，回车停止

```
#include <iostream>
#include <string>
using namespace std;
int main(void)
{
    string s1, s2, s3;    // 初始化一个空字符串
    // 单字符串输入，读入字符串，遇到空格或回车停止
    cin >> s1;  
    // 多字符串的输入，遇到空格代表当前字符串赋值完成，转到下个字符串赋值，回车停止
    cin >> s2 >> s3;  
    // 输出字符串 
    cout << s1 << endl; 
    cout << s2 << endl;
    cout << s3 << endl;   
    return 0;
}
```

// 运行结果 //
  abc def hig
abc
def
hig
如果希望在最终读入的**字符串中保留空格**，可以**使用 getline 函数**，例子如下：

```
#include <iostream>
#include <string>

using namespace std;

int main(void)
{
    string s1 ;    // 初始化一个空字符串
    getline(cin , s1); 
    cout << s1 << endl;  // 输出
    return 0;
}
```

// 结果输出 //
abc def hi
abc def hi

**3、查询字符串信息、索引**
可以用 **empty size/length** 查询字符串状态及长度，可以用下标操作提取字符串中的字符。 

```
#include <iostream>
#include <string>
using namespace std;
int main(void)
{
    string s1 = "abc";    // 初始化一个字符串
    cout << s1.empty() << endl;  // s 为空返回 true，否则返回 false
    cout << s1.size() << endl;   // 返回 s 中字符个数，不包含空字符
    cout << s1.length() << endl;   // 作用同上
    cout << s1[1] << endl;  // 字符串本质是字符数组
    cout << s1[3] << endl;  // 空字符还是存在的
    return 0;
}
```

// 运行结果 //
0
3
3
b

**4、拼接、比较等操作**

```
s1+s2          // 返回 s1 和 s2 拼接后的结果。加号两边至少有一个 string 对象，不能都是字面值
s1 == s2       // 如果 s1 和 s2 中的元素完全相等则它们相等，区分大小写
s1 != s2
<, <=, >, >=   // 利用字符的字典序进行比较，区分大小写
```

**5、cctype 头文件(判断字符类型：大/小写字母、标点、数字等)**
cctype 头文件中含有对 string 中字符操作的库函数，如下：

```
isalnum(c)  // 当是字母或数字时为真
isalpha(c)  // 当是字母时为真
isdigit(c)  // 当是数字是为真
islower(c)  // 当是小写字母时为真
isupper(c)  // 当是大写字母时为真
isspace(c)  // 当是空白（空格、回车、换行、制表符等）时为真
isxdigit(c) // 当是16进制数字是为真
ispunct(c)  // 当是标点符号时为真（即c不是 控制字符、数字、字母、可打印空白 中的一种）
isprint(c)  // 当时可打印字符时为真（即c是空格或具有可见形式）
isgraph(c)  // 当不是空格但可打印时为真
iscntrl(c)  // 当是控制字符时为真
tolower(c)  // 若c是大写字母，转换为小写输出，否则原样输出
toupper(c)  // 类似上面的
```

**6、for 循环遍历**
c++11 标准的 for(declaration: expression) 形式循环遍历，例子如下：

（如果想要改变 string 对象中的值，必须把循环变量定义为引用类型）

```
#include <iostream>
#include <string>
#include <cctype>
using namespace std;
int main(void)
{
    string s1 = "nice to meet you~";    // 初始化一个空字符串
    // 如果想要改变 string 对象中的值，必须把循环变量定义为引用类型。引用只是个别名，相当于对原始数据进行操作
    for(auto &c : s1)  
        c = toupper(c); 
    cout << s1 << endl; // 输出
    return 0;
}
```

// 运行结果 //
NICE TO MEET YOU~

> [!NOTE]
>
> **C++标准的`for(declaration:expression)`**
>
> **具体如何操作？**
>
> expression 的表示必须是一个序列，比如用花括号括起来的初始值列**表、数组、vector、string等类型的对象**。
>
> 这些类型的共同点是**拥有能返回迭代器的begin和end成员**。
>
> declaration定义一个变量，序列中的每一个元素都可以转换成该变量的类型。最简单的方法是使用auto类型说明符；
>
> ```
> void main() {
> 	vector<const char*> ch= { "ebb","string","seires","gallow" };
> 	for (auto sh : ch)  //或者 for (const char* sh : ch)
> 		cout << sh << endl;
> 	system("pause");
> }
> ```
>
> 
>

**7、修改 string 的操作**
在 pos 之前插入 args 指定的字符。

pos是一个下标或者迭代器。

接受下标的版本返回一个指向 s 的引用。

接受迭代器的版本返回一个指向第一个插入字符的迭代器 

```
s.insert(pos, args)  
// 在 s 的位置 0 之前插入 s2 的拷贝

s.insert(0, s2)  
```

删除从 pos 开始的 len 个字符。如果 len 省略，则删除 pos 开始的后面所有字符。返回一个指向 s 的引用。

```
s.erase(pos, len)  
```

将 s 中的字符替换为 args 指定的字符。返回一个指向 s 的引用。

```
s.assign(args)  
```

将 args 追加到 s ，返回一个指向 s 的引用。

args 不能是单引号字符，若是单个字符则必须用双引号表示。**如，可以是 s.append("A") 但不能是 s.append('A')**    

```
s.append(args)  
```

将 s 中范围为 range 内的字符替换为 args 指定的字符。range 或者是一个下标或长度，或者是一对指向 s 的迭代器。返回一个指向 s 的引用。

```
s.replace(range, args) 
// 从位置 3 开始，删除 6 个字符，并插入 "aaa".删除插入的字符数量不必相等
s.replace(3, 6, "aaa")  
```

**8、string 搜索操作**
搜索操作返回指定字符出现的下标，如果未找到返回 npos 

```
s.find(args)  // 查找 s 中 args 第一次出现的位置
s.rfind(args)  // 查找 s 中 args 最后一次出现的位置
```

在 s 中查找 args 中任何一个字符 最早/最晚 出现的位置

```
s.find_first_of(args)  // 在 s 中查找 args 中任何一个字符最早出现的位置
s.find_last_of(args)  // 在 s 中查找 args 中任何一个字符最晚出现的位置
```

例如：

```
string s1 = "nice to meet you~"; 
cout << s1.find_first_of("mey") << endl; // 输出结果为 3，'e' 出现的最早
```

在 s 中查找 第一个/最后一个 不在 args 中的字符的位置

```
s.find_first_not_of(args)  // 查找 s 中 第一个不在 args 中的字符的位置
s.find_last_not_of(args)  // 查找 s 中 最后一个不在 args 中的字符的位置
```

例如：

```
string s1 = "nice to meet you~";  
cout << s1.find_first_not_of("nop") << endl; // 输出结果为 1 ，'i' 不在 "nop" 里
```

**9、string、char 型与数值的转换**
将数值 val 转换为 string 。val 可以是任何算术类型（int、浮点型等）。

```
string s = to_string(val)
```

**字符串转换为整数并返回。**

返回类型分别是 int、long、unsigned long、long long、unsigned long long。

b 表示转换所用的进制数，默认为10，即将字符串当作几进制的数转换，最终结果仍然是十进制的表示形式 。

p 是 size_t  指针，用来保存 s 中第一个非数值字符的下标，默认为0，即函数不保存下标，该参数也可以是空指针，在这种情况下不使用。

```
// 函数原型 int stoi (const string&  str, size_t* idx = 0, int base = 10);
stoi(s, p, b)
stol(s, p, b)
stoul(s, p, b)
stoll(s, p, b)
stoull(s, p, b)
```

// 例如

```
string s1 = "11";    // 初始化一个空字符串
int a1 = stoi(s1);
cout << a1 << endl; // 输出 11
int a2 = stoi(s1, nullptr, 8);
cout << a2 << endl; // 输出 9
int a3 = stoi(s1, nullptr, 2);
cout << a3 << endl; // 输出 3
```

**转换为浮点数并返回。**

返回类型分别是 float、double、long double 。

p 是 size_t  指针，用来保存 s 中第一个非数值字符的下标，默认为0，即函数不保存下标，该参数也可以是空指针，在这种情况下不使用。

```
stof(s)
stof(s, p)
stod(s, p)
stold(s, p)
```

**char 型转数值。**

注意传入的参数是指针类型，即要对字符取地址

```
atoi(c)
// 函数原型 int atoi(const char *_Str)
atol(c)
atoll(c)
atof(c)
```

**字符串反转** 
使用 <algorithm> 头文件中的 reverse() 方法：

    string s2 = "12345";    // 初始化一个字符串
    reverse(s2.begin(), s2.end()); // 反转 string 定义的字符串 s2 
    cout << s2 << endl; // 输出 54321
**提取字串**
 使用  string ss = s.substr(pos, n) 。

从索引 pos 开始，提取连续的 n 个字符，包括 pos 位置的字符。

### 栈

c++栈的方法的基本用法： 

1. push(): 向栈内压入一个成员；

2. pop(): 从栈顶弹出一个成员；

3. empty(): 如果栈为空返回true，否则返回false；

4. top(): 返回栈顶，但不删除成员；

5. size(): 返回栈内元素的大小；

   ```
   #include<iostream>
   #include<stack>
   using namespace std;
   
   int main(){
   	stack <int> stk;
   	for(int i=0;i<10;i++){
   		stk.push(i);
   	}
   	cout<<stk.size()<<endl;
   	cout<<stk.top()<<endl;
   	stk.pop();
   	cout<<stk.empty()<<endl;
   	
   }
   ```

   

#### 练习题E-G-H-I

[E-好串_牛客竞赛语法入门班数组栈、队列和stl习题](https://ac.nowcoder.com/acm/contest/19850/E)

```
#include<bits/stdc++.h>

using namespace std;

int main(){
    string s;
    cin>>s;
    stack<int> st;
    for(int i=0;i<s.size();i++){
        //字符是'a'
        if(s[i]=='a'){
            st.push(s[i]);
        }else{//栈非空时有非a字符入栈或字符不为b
            if(st.empty()||s[i]!='b'){
                cout<<"Bad";
                return 0;
            }else{
                //入栈是b
                st.pop();
            }
        }
    }
    cout<<(st.empty()?"Good":"Bad");
    return 0;
}
```

[G-栈和排序_牛客竞赛语法入门班数组栈、队列和stl习题](https://ac.nowcoder.com/acm/contest/19850/G)

```
#include<bits/stdc++.h>
using namespace std;

int main(){
    int n;
    cin>>n;
    vector<int> a(n);
    for(int i=0;i<n;i++){
        cin>>a[i];
    }
    //计算每一个元素后续最大的元素
    //倒序计算最大
    vector<int> max_remaining(n+1,0);
    for(int i=n-1;i>=0;i--){
        max_remaining[i]=max(a[i],max_remaining[i+1]);
    }
    stack<int> st;
    vector<int> res;
    //将序列逐个压入栈中，若栈顶元素大于后续最大元素，可直接输出，否者入栈。
    for(int i=0;i<n;i++){
        st.push(a[i]);
        while(!st.empty()&&st.top()>=max_remaining[i+1]){
            res.push_back(st.top());
            st.pop();
        }
    }
    for(int i=0;i<res.size();i++){
        cout<<res[i];
        if(i!=res.size()-1){
            cout<<" ";
        }
    }
    return 0;
}
```

> [!NOTE]
>
> **如何计算数组元素后续的最大元素？**
>
> 倒序！
>
>     vector<int> max_remaining(n+1,0);
>     for(int i=n-1;i>=0;i--){
>         max_remaining[i]=max(a[i],max_remaining[i+1]);
>     }

[H-吐泡泡_牛客竞赛语法入门班数组栈、队列和stl习题](https://ac.nowcoder.com/acm/contest/19850/H)

```
#include<bits/stdc++.h>
using namespace std;

int main(){
    string s;
    while(cin>>s){
        stack<char> st;
        //注意这里需要处理多个连续字符串
        //OooO时：Ooo——>OO——>爆炸
        for(char c: s){
            char current=c;
            while(true){
                //如果栈空，直接入栈
                if(st.empty()){
                    st.push(current);
                    break;
                }else{
                    char top= st.top();
                    if(current=='o'&&top=='o'){
                        st.pop();
                        current='O';
                    }else if(current=='O'&&top=='O'){
                        st.pop();
                        current='\0';
                        break;
                    }else{
                        st.push(current);
                        break;
                    }
                }
            }
        }
        //栈只可用下标访问
        string res;
        while(!st.empty()){
            res+=st.top();
            st.pop();
        }
        //逆序输出堆栈字符
        reverse(res.begin(),res.end());
        cout<<res<<endl;
    }
    return 0;
}
```

> [!NOTE]
>
> **注意“泡泡”连续反应的情况：例OooO时：Ooo——>OO——>爆炸**
>
> 利用循环处理连续合并,可设置一个current表明当前处理的字符形式。
>
> **栈不能用下表访问，栈的访问形式只可通过push和pop实现。**

[I-牛牛与后缀表达式_牛客竞赛语法入门班数组栈、队列和stl习题](https://ac.nowcoder.com/acm/contest/19850/I)（后缀表达式求值）

```
class Solution {
public:
    /**
     * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
     *
     * 给定一个后缀表达式，返回它的结果
     * @param str string字符串 
     * @return long长整型
     */
    long long legalExp(string str) {
        // write code here
        stack<long long> st;
        long long num=0;
        for(char c : str){
            //数字
            if(c>='0'&&c<='9'){
                num=num*10+(c-'0');
            }else if(c=='#'){
                st.push(num);
                num=0;
            }else{
                //运算符
                long long a=st.top();
                st.pop();
                long long b=st.top();
                st.pop();
                long long res=0;
                if(c=='+'){
                    res=a+b;
                }
                if(c=='-'){
                    res=b-a;
                }
                if(c=='*'){
                    res=a*b;
                }
                st.push(res);
                }
            }
        return st.top();
        }
};
```



#### getline （配合 istringstream）分割字符串

C++ 标准库中的 `std::getline` 函数可以从输入流中读取一行内容，默认以换行符作为结束符，但它也**支持自定义分隔符。**

其函数原型为：

```cpp
istream& getline(istream &is, string &str, char delim);
```

- **is**：输入流，例如 `std::cin`、`std::ifstream` 或 `std::istringstream`。
- **str**：存储读取结果的字符串对象。
- **delim**：自定义的分隔符，读取会一直进行直到遇到该字符为止（该字符不会被存入字符串中）。

要分割一个字符串，常用的做法是：

1. 将待分割的字符串存入 `std::istringstream` 对象中。
2. 利用 `std::getline` 函数，并指定分隔符，对该流进行多次读取，依次提取出各个子串。

以下代码示例展示如何使用 `std::getline` 结合 `std::istringstream` 来分割一个用 `'#'` 分隔的字符串：

```cpp
#include <iostream>
#include <sstream>
#include <vector>
#include <string>
using namespace std;

int main() {
    // 示例字符串，假设 '#' 为分隔符
    string s = "123#456#789#";
    
    // 创建 istringstream 对象
    istringstream iss(s);
    
    // 用于存放分割后的子串
    vector<string> tokens;
    string token;
    
    // 使用 getline 来按 '#' 分割字符串
    while(getline(iss, token, '#')) {
        // 如果 token 为空字符串（例如遇到连续分隔符或者末尾有分隔符），可以选择跳过
        if(!token.empty()) {
            tokens.push_back(token);
        }
    }
    
    // 输出结果验证
    for(const auto &str : tokens) {
        cout << str << endl;
    }
    
    return 0;
}
```

1. **创建 istringstream 对象**
    将字符串 `s` 传入 `istringstream` 构造函数，构造出一个输入流对象 `iss`。这样可以像从文件或标准输入一样，从这个流中读取数据。
2. **分割过程**
    利用 `while(getline(iss, token, '#'))` 循环，每次调用 `getline` 都会从流 `iss` 中读取直到遇到 `'#'` 为止的内容，并将结果存入 `token`。
   - 当遇到分隔符时，`getline` 将停止读取，并丢弃这个分隔符，不会将其存入 `token`。
   - 如果两个 `'#'` 连续出现，或字符串以 `'#'` 结尾，那么可能会得到空字符串，为了避免不必要的空 token，代码中增加了判断 `if(!token.empty())`。
3. **保存和使用分割结果**
    将每次得到的 token 存入 `vector<string> tokens` 中，最后可以根据需要对分割后的子串进行进一步处理（例如将其转换为数字或作为表达式的操作数）。

### 队列

C++队列Queue类成员函数如下:

1. back()返回最后一个元素
2. empty()如果队列空则返回真
3. front()返回第一个元素
4. pop()删除第一个元素
5. push()在末尾加入一个元素
6. size()返回队列中元素的个数

#### 练习题J

[J-Keep In Line_牛客竞赛语法入门班数组栈、队列和stl习题](https://ac.nowcoder.com/acm/contest/19850/J)

优化前：

```
#include<bits/stdc++.h>
using namespace std;

int main(){
    int t;
    cin>>t;
    while(t--){
        int n;
        cin>>n;
        deque<string> q;
        string opt ,name;
        int cnt=0;//插队的人数
        for(int i =0;i<n;i++){
            cin>>opt>>name;
            if(opt=="in"){
                q.push_back(name);
            }
            if(opt=="out"){
                if(name==q.front()){
                    //不插队
                    q.pop_front();
                }else{
                    //出现插队
                    cnt++;
                    auto it=find(q.begin(),q.end(),name);
                    if(it!=q.end()){
                        q.erase(it);
                    }
                }
            }
        }
        cout<<n/2-cnt<<endl;
    }
    return 0;
}
```

> [!WARNING]
>
> **在队列中无法查找指定元素，改用双端队列进行查找指定元素并实现删除**
>
> ```
> auto it = find(q.begin(), q.end(), name);
> if(it != q.end()){
>     q.erase(it);
> }
> ```
>
> **`find` 和 `erase` 操作**：
>
> 在 `deque` 中查找插队同学时使用了 `find(q.begin(), q.end(), name)`，这会遍历整个队列，时间复杂度为 O(n)。
>
> 使用 `erase` 删除元素，这同样会涉及到移动操作，时间复杂度也是 O(n)。**总计O(2*n)。**
>
> 每次入队出队都要进行查找，**时间复杂度总计O(2n^2);**

> [!NOTE]
>
> 下面是 deque 容器的一些常用成员函数：
>
> | 函数名称                               | 功能描述                                          |
> | :------------------------------------- | :------------------------------------------------ |
> | `deque()`                              | 默认构造函数，创建一个空的 `deque` 容器。         |
> | `deque(size_type n)`                   | 创建一个包含 `n` 个默认值元素的 `deque` 容器。    |
> | `deque(size_type n, const T& value)`   | 创建一个包含 `n` 个值为 `value` 的 `deque` 容器。 |
> | `deque(initializer_list<T> il)`        | 使用初始化列表 `il` 构造 `deque` 容器。           |
> | `operator=`                            | 赋值操作符，赋值给 `deque` 容器。                 |
> | `assign()`                             | 用新值替换 `deque` 容器中的所有元素。             |
> | `at(size_type pos)`                    | 返回 `pos` 位置的元素，并进行范围检查。           |
> | `operator[](size_type pos)`            | 返回 `pos` 位置的元素，不进行范围检查。           |
> | `front()`                              | 返回第一个元素的引用。                            |
> | `back()`                               | 返回最后一个元素的引用。                          |
> | `begin()`                              | 返回指向第一个元素的迭代器。                      |
> | `end()`                                | 返回指向末尾元素后一位置的迭代器。                |
> | `rbegin()`                             | 返回指向最后一个元素的逆向迭代器。                |
> | `rend()`                               | 返回指向第一个元素之前位置的逆向迭代器。          |
> | `empty()`                              | 检查容器是否为空。                                |
> | `size()`                               | 返回容器中的元素个数。                            |
> | `max_size()`                           | 返回容器可容纳的最大元素个数。                    |
> | `clear()`                              | 清除容器中的所有元素。                            |
> | `insert(iterator pos, const T& value)` | 在 `pos` 位置插入 `value` 元素。                  |
> | **`erase(iterator pos)`**              | **移除 `pos` 位置的元素。**                       |
> | **`push_back(const T& value)`**        | **在容器末尾添加 `value` 元素。**                 |
> | **`pop_back()`**                       | **移除容器末尾的元素。**                          |
> | **`push_front(const T& value)`**       | **在容器前端添加 `value` 元素。**                 |
> | **`pop_front()`**                      | **移除容器前端的元素。**                          |
> | `resize(size_type count)`              | 调整容器大小为 `count`，多出部分用默认值填充。    |
> | `swap(deque& other)`                   | 交换两个 `deque` 容器的内容。                     |
> | `get_allocator()`                      | 返回一个用于构造双端队列的分配器对象的副本。      |

### 哈希集合unordered_set

**定义**

哈希表就是在关键字和存储位置之间建立对应关系，使得**元素的查找可以以O(1)的效率进行**， 其中关键字和存储位置之间是通过散列函数建立关系，记为:
**L o c ( i ) = H a s h ( k e y i ) 。**

```
unordered_set<int> hashset;  
```

**插入元素**

```
hashset.insert('a')
```

**删除元素**

```
hashset.erase('a');
```

**查询某元素是否存在**

```
   if (hashset.count('a') > 0) 
   {
        return true;
   }
   else
   {
        return false;
   }
```

**获取哈希集元素个数**

```
hashset.size()
```

**auto迭代**

```
   for (auto it = hashset.begin(); it != hashset.end(); it++) 
    {
        cout << (*it) << " ";
    }
```

**清空哈希集**

```
hashset.clear();
```

**判断哈希集是否为空**

```
   if (hashset.empty() ) 
   {
        return true;
   }
   else
   {
        return false;
   }
```

#### 练习题J—优化

```
#include<bits/stdc++.h>
using namespace std;

int main(){
    int t;
    cin>>t;
    while(t--){
        int n;
        cin>>n;
        queue<string> q;
        string opt ,name;
        unordered_set<string> cut;//记录插队的同学
        int cnt=0;//不插队的好同学人数
        for(int i =0;i<n;i++){
            cin>>opt>>name;
            if(opt=="in"){
                q.push(name);
            }
            else{
                if(name==q.front()){
                    //不插队
                    cnt++;
                    q.pop();
                    //后面插队的同学出去
                    while(!q.empty()&&cut.count(q.front())>0){
                        //出去一个队头元素，若后续队头元素是插队队列中的，亦出列
                        q.pop();
                    }
                }
                else{
                //出现插队
                cut.insert(name); 
                }
            }
        }
        cout<<cnt<<endl; 
    }
    return 0;                   
}
```

> [!NOTE]
>
> **哈希集合是无序的，添加集合元素使用insert**



### 素数-筛法

**埃拉托色尼筛选法**

  埃拉托色尼筛选法(the Sieve of Eratosthenes)简称埃氏筛法，是古希腊数学家埃拉托色尼(Eratosthenes 274B.C.～194B.C.)提出的一种筛选法。 是针对自然数列中的自然数而实施的，用于求一定范围内的质数。

**埃拉托色尼筛选法步骤：**

（1）先把1删除（现今数学界1既不是质数也不是合数）

（2）读取队列中当前最小的数2，然后把2的倍数删去

（3）读取队列中当前最小的数3，然后把3的倍数删去

（4）读取队列中当前最小的数5，然后把5的倍数删去

（5）读取队列中当前最小的数7，然后把7的倍数删去

（6）如上所述直到需求的范围内所有的数均删除或读取

	#define MAX_NUM (200)        //筛选200内的所有质数
	bitset<MAX_NUM + 1> bs; //bs[0] 不用，只有bs[1]~bs[200]
	bs.set(); //把bs所有的bits置1
	bs[1] = 0; //1不是质数
	for (int i(2); i < MAX_NUM+1; i++) //i从2开始
	{
		//埃拉托色尼筛选过程
		if (bs[i])
		{
			for (int j(i * 2); j < MAX_NUM + 1; j +=i )
				bs[j] = 0;
		}
	}

**算法优化**

**理论依据一：任何非质数，都会有一个因数不会大于他的算术平方根。**

```
#define MAX_NUM (200)        //筛选200内的所有质数
#define S_NUM  sqrt(MAX_NUM) //我们只需要筛选到sqrt(MAX_NUM) 就可以了
bitset<MAX_NUM + 1> bs; //bs[0] 不用，只有bs[1]~bs[200]
bs.set(); //把bs所有的bits置1
bs[1] = 0; //1不是质数
for (int i(2); i < S_NUM +1; i++) //i从2开始
{
	//埃拉托色尼筛选过程
	if (bs[i])
	{
		for (int j(i * 2); j < MAX_NUM + 1; j +=i )
			bs[j] = 0;
	}
}
```

**理论依据二：根据观察，每次筛选的时候从这个数的平方开始筛选就可以**

```
for (int i(2); i < S_NUM +1; i++) *//i从2开始*

{
	*//埃拉托色尼筛选过程*
	if (bs[i])
	{
		for (int j(i * i); j < MAX_NUM + 1; j +=i )
			bs[j] = 0;
	}
}
```



#### 练习题K

[K-Number_牛客竞赛语法入门班数组栈、队列和stl习题](https://ac.nowcoder.com/acm/contest/19850/K)

```
#include<bits/stdc++.h>
using namespace std;

const int max_n=50000000;

//初始化默认都是素数
vector<bool> isprime(max_n+1,true);
//储存素数
vector<int>primes;
//预处理素数-埃拉托色尼筛选法
//若一个素是素数，则它的倍数也是素数
void sieve(){
    //0和1不是素数
    isprime[0]=isprime[1]=false;
    //算法优化一：理论依据：任何非质数，都会有一个因数不会大于他的算术平方根。
    for(int i=2;i*i<max_n;i++){
        //若i是素数，则它的倍数全为素数
        if(isprime[i]){
            //算法优化二：根据观察，每次筛选的时候从这个数的平方开始筛选就可以。
            for(int j=i*i;j<max_n;j+=i){
                isprime[j]=false;
            }
        }
    }
    //添加记录到是素数中
    for(int i=2;i<max_n;i++){
        if(isprime[i]){
            primes.push_back(i);
        }
    }
}
//记录shuaishuai数
unordered_set<long long> shuaishuai;

int main(){
    int n;
    cin>>n;
    sieve();
    for(int i:primes){
        long long a=1LL*i*i;
        if(a>=n)break;
        for(int j :primes){
            long long b=1LL*j*j*j;
            if(b>=n)break;
            for(int k:primes){
                long long c=1LL*k*k*k*k;
                if(c>=n)break;
                long long res=a+b+c;
                if(res<=n)shuaishuai.insert(res);
            }
        }       
    }
    cout<<shuaishuai.size();
    return 0;
}
```

> [!NOTE]
>
> **算法复杂度过高？剪枝：提前跳出循环**



#### 练习题L

[L-指纹锁_牛客竞赛语法入门班数组栈、队列和stl习题](https://ac.nowcoder.com/acm/contest/19850/L)

```
#include<bits/stdc++.h>
using namespace std;

int main(){
//     // 关闭同步，使得cin和cout不再与C的stdio同步，提高效率
//     ios::sync_with_stdio(false);
//     // 解除cin和cout的绑定，进一步提高输入输出效率
//     cin.tie(NULL);
//     cout.tie(NULL);

int m,k;
cin>>m>>k;
//记录指纹锁内容
unordered_set<int> zhiwen;
string opt;
int x;
for(int i=0;i<m;i++){
    cin>>opt>>x;
    if(opt=="add"){
        if(zhiwen.size()==0){
            zhiwen.insert(x);
        }else{
            for(int a:zhiwen){
                if(abs(a-x)>k){
                    zhiwen.insert(x);
                }
            } 
        }
    }
    if(opt=="del"){
        vector<int> tmp;
        //注意：使用迭代器时不可直接删除元素
        for(int a:zhiwen){
            if(abs(a-x)<=k){
                tmp.push_back(a);
            }
        }
        for(int t:tmp){
            zhiwen.erase(t);
        }
    }
    if(opt=="query"){
        bool ison=false;
        for(int a:zhiwen){
            if(abs(a-x)<=k){
                cout<<"Yes"<<endl;
                ison=true;
                break;
            }
        }
        if(ison==false)cout<<"No"<<endl;
    }
}
return 0;

}
```

> [!WARNING]
>
> 当前代码每次操作都需要遍历整个集合，因此在最坏情况下，每个操作的时间复杂度都是 O(n)（其中 n 为集合中指纹的个数），整体上 m 次操作的最坏复杂度可达到 O(m·n)。在最坏情况下（例如连续的 add 操作使得集合越来越大，每次查询或删除都需要遍历所有元素），**总体时间复杂度可能接近 O(m²)**。

> [!CAUTION]
>
> 使用迭代器时不可直接删除元素，会影响迭代
>
> 可使用一个辅助容器保存要删除的元素

### set

set 内部通常采用平衡二叉搜索树（如红黑树）实现，这使得**所有存入的元素都会按顺序排列。**

- **begin()   　　 ,返回set容器的第一个元素**
- **end() 　　　　 ,返回set容器的最后一个元素**
- **clear()  　　   ,删除set容器中的所有的元素**
- **empty() 　　　,判断set容器是否为空**
- **max_size() 　 ,返回set容器可能包含的元素最大个数**
- **size() 　　　　 ,返回当前set容器中的元素个数**
- **rbegin　　　　 ,返回的值和end()相同**
- **rend()　　　　 ,返回的值和rbegin()相同**

**优势：**
这样可以利用二分查找的思想快速定位目标元素，降低搜索时间到 O(log n)。

**用 lower_bound 实现范围查找**

- **需求描述：**
  对于 add 和 query 操作，需要判断集合中是否存在一个元素 a 使得

  
  $$
  ∣a−x∣≤k⇔a∈[x−k,x+k]
  $$
  

- **实现方式：**
  利用 std::set 的 `lower_bound(x-k)`，可以快速获得**第一个不小于 (x-k) 的元素**。

  - 如果这个元素存在且其值不大于 (x+k)，就说明集合中存在满足条件的指纹。
  - 否则就不存在满足条件的指纹，从而可以执行插入或其他操作。

- **代码示例：**

```
auto it = fingerprints.lower_bound(x - k);
if (it == fingerprints.end() || *it > x + k) {
    // 没有元素在 [x-k, x+k] 区间内，可以插入 x
    fingerprints.insert(x);
}
```

**用 lower_bound 定位范围起点，然后只需要检查一个或少量元素即可判断是否存在满足条件的指纹，从而将查找时间复杂度从 O(n) 降低到 O(log n)。**

#### 练习题L-优化

```
#include<bits/stdc++.h>
using namespace std;

int main(){
    // 关闭同步，使得cin和cout不再与C的stdio同步，提高效率
    ios::sync_with_stdio(false);
    // 解除cin和cout的绑定，进一步提高输入输出效率
    cin.tie(NULL);
    cout.tie(NULL);
    int m,k;
    cin>>m>>k;
    //记录指纹锁内容
    set<int> zhiwen;
    string opt;
    int x;
    for(int i=0;i<m;i++){
        cin>>opt>>x;
        if(opt=="add"){
            //查找指纹中第一个不小于x-k的
            auto it=zhiwen.lower_bound(x-k);
            //若不满足条件，则插入新的指纹
            if(it==zhiwen.end()||*it>x+k){
                zhiwen.insert(x);
            }
        }
        if(opt=="del"){
            vector<int> tmp;
            auto it=zhiwen.lower_bound(x-k);
            //注意：使用迭代器时不可直接删除元素
            while(it!=zhiwen.end()&&*it<=x+k){
                tmp.push_back(*it);
                it++;
            }
            for(int t:tmp){
                zhiwen.erase(t);
            }
        }
        if(opt=="query"){
            auto it=zhiwen.lower_bound(x-k);
            if(it!=zhiwen.end()&&*it<=x+k){
                cout<<"Yes"<<endl;
            }else{
                cout<<"No"<<endl;
            }
        }
    }
    return 0;
}
```

#### 练习题-M

```
#include<bits/stdc++.h>

using namespace std;

int main(){
    int n;
    cin>>n;
    unordered_set<string> us;
    string s;
    while(n--){
        cin>>s;
        if(s!="younik"){
            us.insert(s);
        }else{
            cout<<us.size()+1;
            return 0;
        }
    }
    return 0;
}
```

