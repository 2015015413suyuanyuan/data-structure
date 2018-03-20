# 数据结构复习
## 第一章 绪论

数据结构的研究内容:   
>   **逻辑结构**：研究对象的特性及其相互之间的关系  
>   **存储结构**：有效地组织计算机存储  
>   **算法**:有效地实现对象之间的“运算”关系  

《数据结构》是一门研究非数值计算的程序设计问题中计算机的**操作对象**以及它们之间的**关系**和**操作**的一门学科。


数据结构： **线性表（一般线性表、操作受限线性表、数据受限线性表、线性表的扩展）  树（二叉树）  图**

算法： **查找  排序**

四类基本数据结构：**集合结构 线性结构  树形结构  图状结构**

关系、关联的表示用（**序偶**）表示。 三种基本的关系： *1:1   1:n  n:m*

+ 物理结构（存储结构）：数据结构在计算机中的表示（映像）称为数据的物理结构。

* 顺序映像 ： 顺序映像的特点是借助元素在储蓄器中的相对位置来表示数据元素之间的逻辑关系。

* 非顺序映像 ： 非顺序映像的特点是借助指示元素存储地址的指针表示数据元素之间的逻辑关系。 


**数据类型**： 是一组性质相同的**值的集合**以及定义于这个值集合上的一组操作的总称。

**数据类型的作用**：约束变量的**内存空间**   约束变量或常量的**取值范围、操作**

* 抽象数据类型（abstract data type ADT）  
    是指一个数学模型以及定义在该模型上的一组操作。抽象数据类型的定义仅取决于它的一组逻辑特性，而与其在计算机内部如何表示和实现无关。  
含义： 一种数据类型，其数据对象和对象操作的规格说明独立于对象的存储表示和对象上操作的实现。

**抽象数据类型的定义**  
* 和数据结构的形式定义相对应，抽象数据类型可以用三元组来刻画:(D,S,P)。其中D是数据对象，S是D上的关系集，P是对D的基本操作。  
```
     ADT  抽象数据类型名{
               数据对象：<数据对象的定义>
               数据关系：<数据关系的定义>
               基本操作：<基本操作的定义>
     } ADT  抽象数据类型名
              其中，数据对象和数据关系的定义用伪码描述，基本操作的定义格式为：
     基本操作名(参数表)
              初始条件：<初始条件描述>
              操作结果：<操作结果描述>
```

二元组定义的例子：  
```
ADT Compare{
     数据对象：D={e1,e2| e1,e2为可比较的同类型的元素}
     数据关系：R={< e1,e2 >}
     基本操作：
     InitCom(&C,ee1,ee2)
     操作结果：构造一个二元组c，元素e1,e2分别被赋成ee1,ee2。
     FirElemBig(C)
     初始条件：二元组已经存在。
     操作结果：如果首元素大，则返回1，否则返回0。
     ...
   } ADT Compare

```

**抽象数据类型的表示**  
* 抽象数据类型的表示就是要将该类型映射到计算机中，也就是确定抽象数据类型的存储结构以及给出基于该结构上的基本操作的函数原型。  
```
       typedef  int   ElemType; //整形元组
       typedef  ElemType  * Compare; //动态顺序存储结构
       //初始化二元组
       InitCom(Compare  &C, ElemType  ee1, ElemType  ee2)

       //判断二元组的首元素是否比次元素大
       FirElemBig(Compare  C)
       ……
```
**抽象数据类型的实现**  
* 抽象数据类型的实现就是基于特定存储结构之上的基本操作的实现。  
初始化二元组例子：  
```
       Status InitCom(Compare  &C, ElemType  ee1, ElemType  ee2)
        {
               C = (ElemType *)malloc(2*sizeof(ElemType));
               if(!C) exit (OVERFLOW);
                C[0] = ee1;  C[1] = ee2;
                return OK;
        }

        //判断二元组的首元素是否大
       Status FirElemBig(Compare  C)
       {
                 if(C[0] > C[1])  return  TRUE;
                 else  return  FALSE;
       }

```

### 算法的基本概念  
算法是对特定问题求解步骤的一种描述，它是指令的有限序列，其中每一条指令表示一个或多个操作。  
* 算法的五个特性 ：**有穷性 确定性 可行性 0个或多个输入 1个或多个输出**  
* 算法的设计要求 ： **正确性  可读性  健壮性  高效率  低存储**  

算法的含义与程序十分相似，但二者是有区别的。  
1. 一个程序不一定满足有穷性
2. 程序中的指令必须是机器可执行的，而算法中的指令则无此限制。算法若用计算机语言来书写，则它就可以是程序。  
    一个算法可以用自然语言或约定符号来描述，也可以用流程图、计算机高级程序语言（如C语言）或伪代码等来描述。

#### 算法的表现形式  
**冒泡排序**
```
void   bubble_sort(int   a[] , int  n)
{    
//将a中整数序列按从小到大的顺序排序
	  for(i = n-1;i>=1; i--)
	  {
             for(j = 0; j<i;j++)
		       if(a[j] > a[j+1])
		       {
			a[j]<--->a[j+1];
		       } 
}
```

**优化冒泡排序**
```
void   bubble_sort(int   a[] , int  n)
{    //将a中整数序列按从小到大的顺序排序
	  for(i = n-1, change = TURE;i>=1 && change; i--)
	  {
            change = FALSE;//交换标识
             for(j = 0; j<i;j++)
		       if(a[j] > a[j+1])
		       {
			a[j]<--->a[j+1];
                           change = TRUE;
                   } 
}
```
#### 算法效率的度量  
* 事后统计法
* 事前分析法
* 只考虑问题规模（基本操作）  
        一般情况下，算法中基本操作重复执行的次数是问题规模 n 的某个函数f(n),记作：T(n) = O (f(n)),它表示随着问题规模n的增大，算法执行时间的增长率和f(n)的增长率相同。  
* 频度的概念  基本操作的执行次数。  


```
例：{++x; s=0;}
        包含 “x 增 1” 基本操作的语句的频度为１，即时间复杂度 
为O(1)。O(1) 表示算法的运行时间为常量。即：常量阶。


例：for(i =1; i <=n; ++i)
               {++x;  s += x;}
        包含 “x 增 1” 基本操作的语句的频度为：n，其时间复杂度 
为：O(n)，即：线性阶。


例：for(i =1; i <= n;  ++i )
　　　　for(j =1; j <= n; ++j )
                      {++x;  s += x;}
        包含 “x 增 1” 基本操作的语句的频度为：n2，其时间复杂度 
为：O(n2)，即：平方阶。


例：for( i =2; i <= n; ++i )
              for( j =2; j <= i - 1; ++j )
                    {++x;  a[ i, j]=x;}
包含 “x 增 1” 基本操作的语句的频度为：
 1+2+3+…+n-2 = (1+n-2)×(n-2)/2 = (n-1)(n-2)/2  
其时间复杂度为：O(n2)，即：平方阶。 
```

**f(n)的求法**
算法的时间 复杂度常见的有：  
        常数阶 O(1)，对数阶 O(log n)，线性阶 O(n)，线性对数阶 O(nlog n)，平方阶 O(n2)，立方阶 O(n3)，…， k 次方阶O(nk)，指数阶 O(2n)，阶乘阶 O(n!)。


f(n)一般用频度表达式中增长最快的项表示，并将其常数去掉。    
         例如： 假设某元操作的频度：100*2n+8n2  
                          则：T(n)=O(2n)  

  常见的算法的时间 复杂度之间的关系为：  
     O(1)<O(log n)<O(n)<O(nlog n)<O(n2)<O(2n)<O(n!)<O(nn)  
#### 时间复杂度的三种具体情况  
```
Void bubble-sort(int a[]，int n) 
 {   //将 a 中整数序列重新排列成自小至大有序的整数序列。 
      for(i = n-1, change = TURE; i > 1 && change; --i)
            change = false;
             for ( j = 0;  j < i; ++j)
                 if (a[ j] > a[ j +1]) {a[ j]←→a[ j +1];  change = TURE} 
 }// bubble-sort
```

最好情况： 0 次  

最坏情况： 1 + 2 + …… + n-1 = n(n-1)/2

平均时间复杂度为 ： O(n^2)

**在本课程中讨论的时间复杂度，均指最坏的时间复杂度。**  


#### 算法的存储空间需求
**空间复杂度** ： 算法所需存储空间的度量，记作：S(n) = O (f(n))    （其中 n 为问题的规模）

**一个算法所需存储空间** ：算法本身的存储空间 输入数据的存储空间  算法在运行过程中临时占用的存储空间  

若所需临时空间不随问题规模的大小而改变，则称次算法为 **原地工作**  

## 第二章 线性表

一个线性表是 n 个数据元素的有限序列。

* 线性表：最常用且最简单的一种数据结构。

* 线性结构的特点：4个“唯一”。  
  >       存在唯一的一个被称作 “第一个”的数据元素  
  >       存在唯一的一个被称作“最后一个”的数据元素  
  >       除第一个之外的数据元素均只有一个前驱  
  >       除最后一个之外的数据元素均只有一个后继  
### 线性表的ADT定义  

{**销毁结构**}

   DestroyList(&l）  
    初始条件：线性表L已存在。  
    操作结果：销毁线性表L。 
	```
	bool SqList::DestoryList()
	{
	 delete []p;
	 p=NULL;
	    return true;
	}
	```
	
{**引用型操作**}  

操作的结果不改变线性表中数据元素，也不改变数据元素之间的关系。  

##### ListEmpty(L)
   初始条件：线性表L已存在。
   
   操作结果：若L为空表，则返回TRUE，否则返回FALSE。
   
 {**加工型操作**}
 
 操作的结果或修改表中数据元素，或修改元素之间的关系。
 
 ##### ClearList(&L)
 
   初始条件：线性表L已存在。  
   
   操作结果：将L重置为空表。
   
	```
	bool SqList::ClearList()
	{
	 length=0;
	 return true;
	}
	```
	
**思考：clearList(L) 与 DestroyList(L) 的区别**
	
  > 清空线性表，只要里面没有元素就可以。线性表还存在，可以继续操作。L.elem = 0 只是让线性表的元素个数为0。  
  
  > 销毁线性表的操作一般是释放整个线性表的内存空间。销毁后就不能再使用了。

#### 线性表ADT基本操作的简单应用  

##### 例 2-1 已知集合A和B，求这两个集合的并集，使 A= A U B , 且  B 不再单独存在。  

要在计算机中求解，首先要确定 “**如何表示集合**”  --- 用线性表表示  

以线性表LA 和 LB 分别表示集合 A 和 B ，两个线性表的数据元素分别为集合A 和 B 中的成员。

由此，上述集合求并的问题便可演绎为：

扩大线性表LA，将存在于线性表LB中，而不存在于线性表LA中的数据元素插入到线性表LA中去。

```
void union (List &La , List Lb){
    La_len = ListLength(La); Lb_len = ListLength(Lb);
    for(i=1;i<=Lb_len;i++)
    {
    	GetElem(Lb,i,&e);//取Lb中第i个数据元素赋给e
	if(!LocateElem (La,e,equal()))//执行时间与表长成正比
	ListInsert(&La,++La_len,e);
	//La中不存在和e相同的数据元素，则插入之
    }
    DestroyList(Lb);//销毁线性表Lb
}//union
```

时间复杂度 : O(ListLength(La) * ListLenght(Lb))

##### 例 2.2 合并两个有序表  
   LA =(3,5,8,11)  LB=(2,6,8,9,11,15,20)  

**思路**  

1. 分别从La和Lb中取得当前元素ai和bj;
2. 若ai<=bj , 则将ai插入到Lc中，否则将bj插入到lc中。

```
void MergeList(List La, List Lb, List &Lc) {
   InitList(&Lc);
   i = j = 1; k = 0;
   La_len = ListLength(La);     Lb_len = ListLength(Lb);
   while ((i  La_len) && ( j  Lb_len)) {   // La 和 Lb 均未取完 
        GetElem(La, i, ai ); GetElem(Lb, j, bj );
        if (ai  bj ) {ListInsert(Lc, ++k, ai ); ++i; }
        else { ListInsert(Lc, ++k, bj  ); ++j; }
   }
   while (iLa_len) {GetElem(La, i++, ai);  ListInsert(Lc, ++k, ai);} 
   while (jLb_len) {GetElem(Lb, j++, bj);  ListInsert(Lc, ++k, bj);} 
}  
```
**时间复杂度： O（ListLength(La) + ListLength(Lb)）** 

在实际的程序设计中**要使用**线性表的基本操作，必须**先实现**线性表类型。  
	**确定存储结构，实现基本操作**  
	
### 线性表的顺序表示和实现
**线性表的顺序存储结构**  
* 在计算机中用一组**地址连续**的存储单元**依次存储**线性表的个个数据元素，称作线性表的**顺序存储结构**或**顺序映像**。用这种方法存储的线性表称作**顺序表**。

由此，所有数据元素的存储位置均可通过基地址得到：

##### LOC(ai+1) = LOC(ai)+l     LOC(ai)=LOC(a1) + (i-1)*l 

##### 特点：以物理位置相邻表示逻辑关系；任一元素均可随机存取。

**结论**: 已知位置、获取该位置上的元素非常方便，与该线性表的长度无关。

**静态顺序存储**
```
#define LIST_INIT_SIZE 100 //线性表存储空间的初始分配量
typedef struct{
	ElemType elem[LIST_INIT_SIZE];
	int length;//当前长度
}SqList;
```
**动态顺序存储**

考虑到线性表因插入元素而使存储空间不足的问题，应允许数组容量进行动态扩充。

```
#define LIST_INIT_SIZE 100 //线性表存储空间的初始分配量
#define LISTINCREMENT 10   //线性表存储空间的分配增量
typedef struct{
	ElemType *elem;//数组指针，指示线性表的基地址
	int length;//当前长度
	int listsize;//当前分配的存储容量（以sizeof（elementtype）为单位）
}SqList;
```
**注意**C语言中的数组下标从‘0’开始，因此若L是Sqlist类型的顺序表，则表中第i个元素是L.elem[i-1]。

#### 线性表的操作举例

**初始化操作**

**插入操作**

线性表的插入运算是指在表的第i个位置上，插入一个新结点b

>> **算法思想**  
>> 检查i是否超出允许范围（1<= i <=n+1）；  
>> 将第i个元素和它后面所有的元素均后移一个位置；  
>> 将新元素写道空出的第i个位置上；使线性表的长度增1。
```
//往数组尾部增加一个数据
function add_data_to_arry_last(data_arrays,data){
	data_arrays.push(data);
}
//往数组开头增加一个数据
function add_data_to_array_first(data_arrays,data){
	data_arrays.unshift(data);
}
//往数组的任意位置插入一个数据
function add_data_to_array(data_arrays,i,data){
	var len=data_arrays.length;
	if( i<1 || i>len){return false;}
	else{
	  data_arrays.splice(i-1,0,data);
	  return data_arrays;
	}
}
add_data_to_array([1,2,3,4],1,'232');
```
**在顺序表上做插入运算 平均要移动表上一半元素**。当表长n较大时，算法的效率相当低。算法的平均时间复杂度为O(n).

**删除操作**

```
function delete_data_from_array(data_arrays,i){
	var len=data_arrays.length;
	if( i<1 || i>len){return false;}
	else{
	  data_arrays.splice(i-1,1);
	  return data_arrays;
	}
}
delete_data_from_array([1,2,3,4],1);
```
**在顺序表上做删除运算 平均约要移动表上一半元素**。当表长n较大时，算法的效率相当低。算法的平均时间复杂度为O(n).

#### 练习
* 对于顺序存储的线性表，访问结点和删除结点的时间复杂度分别为(**O(1)  O(n)**)。

### 线性表的链式表示和实现

**线性表的链式存储——链表**

   用一组物理位置任意的存储表单来存放线性表的数据元素。这组存储单元既可以是连续的，也可以是不连续的，甚至是零散分布在内存中的任意位置上的。因此链表中元素的逻辑次序和物理次序不一定相同。
   
 结点：数据域  指针域 头指针
 
 单链表是由头指针唯一确定，因此单链表可以用头指针的名字来命名。
 
头结点；在单链表的一个结点之前人为地附设一个结点。

**头结点**： 数据域 指针域  
>> 数据域：不存放任何数据  存放附加信息（链表的结点个数等）  
>> 指针域：存放第一个结点的地址  
**头指针**存放**头结点**的地址。  
**注**：  以后没有特别说明，都是带头结点的单链表。

#### 单链表的基本操作

#### 1. 查找运算
* 按序号查找（GetElem(L,i,&e)在链表中的实现）  
>   在单链表中，即使知道被访问结点的序号i，也不能象顺序表中那样直接按序号i访问结点，而只能从头指针出发，顺着链域next 逐个结点往下搜索，直到搜索到第i个结点为止。因此，**单链表是非随机存取的存储结构**。  
>  算法的时间复杂度为：O(n)

```
function ListNode(data)
{
	this.data = data;
	this.next =null;
	return this;
}
function LinkedList()
{
	this.list_header = null;
}
LinkedList.create_list_from_array = function(array_data)
{
	var list = new LinkedList();
	for(var i=0;i<array_data.length;i++){
		var node = new ListNode(array_data[array_data.length-i-1]);
		node.next = list.list_header;
		list.list_header = node;
	}
	return list;
}

LinkedList.prototype.insert_node_to_list_index =function(index,data)
{
	if(index == 0) return this.insert_node_to_list_first(data);
	var temp = this.get_nodes_from_index_in_list(index);
	this.insert_between_nodes(temp.last,temp.current,data);
	return this.list_header;
};
LinkedList.prototype.insert_node_to_list_first=function(data)
{
	var new_node = new ListNode(data);
	new_node.next = this.list_header;
	this.list_header = new_node;
	return this.list_header;
}
LinkedList.prototype.get_nodes_from_index_in_list=function(index)
{
	var first_node =null;
	var second_node = this.list_header;
	for(var i=0; i!=index;i++)
	{
		first_node = second_node;
		second_node=second_node.next;
	}
	return {
		last:first_node;
		current:second_node
	};
};

LinkedList.prototype.insert_between_nodes = function(first_node,second_node,data)
{
	var new_node = new ListNode(data);
	new_node.next =second_node;
	if(first_node != null) first_node.next = new_node;
	return new_node;
};
```

* 按值查找  
>  算法的时间复杂度为：O(n)  
```
function ListNode(data)
{
    this.data = data;
    this.next = null;
    return this;
}
function LinkedList()
{
    this.list_header = null;
}
LinkedList.create_list_from_array = function(array_data)
{
    //在这里写入代码
    var list = new LinkedList();
    for(var i=0;i<array_data.length;i++){
        //var node = new ListNode(array_data[i]);//这样写的话，链表顺序是如何的，输出测试一下
        var node = new ListNode(array_data[array_data.length-i-1]);
        node.next = list.list_header;
        list.list_header = node;
    }
    return list;
};

LinkedList.prototype.get_node_index_from_data = function(data)
{
    var index = 0;
    //在这里写入代码
    var current_node = this.list_header;
    while(current_node.data!=data){
        currentNode = currentNode.next;
        index++;
        if(currentNode == null){return index=-1;}
    }
    return index;
};

//测试代码如下
var list = LinkedList.create_list_from_array([1,2,3,"x"]);
console.log(list);
list.get_node_index_from_data(3);
```

#### 2、插入运算
##### s->next = p->next;   p->next = s;
#####算法的时间复杂度：O(n)
```
function ListNode(data)
{
	this.data = data;
	this.next =null;
	return this;
}
function LinkedList()
{
	this.list_header = null;
}
LinkedList.create_list_from_array = function(array_data)
{
	var list = new LinkedList();
	for(var i=0;i<array_data.length;i++){
		var node = new ListNode(array_data[array_data.length-i-1]);
		node.next = list.list_header;
		list.list_header = node;
	}
	return list;
}

LinkedList.prototype.insert_node_to_list_index =function(index,data)
{
	if(index == 0) return this.insert_node_to_list_first(data);
	var temp = this.get_nodes_from_index_in_list(index);
	this.insert_between_nodes(temp.last,temp.current,data);
	return this.list_header;
};
LinkedList.prototype.insert_node_to_list_first=function(data)
{
	var new_node = new ListNode(data);
	new_node.next = this.list_header;
	this.list_header = new_node;
	return this.list_header;
}
LinkedList.prototype.get_nodes_from_index_in_list=function(index)
{
	var first_node =null;
	var second_node = this.list_header;
	for(var i=0; i!=index;i++)
	{
		first_node = second_node;
		second_node=second_node.next;
	}
	return {
		last:first_node;
		current:second_node
	};
};

LinkedList.prototype.insert_between_nodes = function(first_node,second_node,data)
{
	var new_node = new ListNode(data);
	new_node.next =second_node;
	if(first_node != null) first_node.next = new_node;
	return new_node;
};
```



#### 3、删除运算
##### p->next = p->next->net;
#####算法的时间复杂度：O(n)
```
function ListNode(data)
{
    this.data = data;
    this.next = null;
    return this;
}
function LinkedList()
{
    this.list_header = null;
}
LinkedList.prototype.find_nodes_from_data_list = function(data)
{
    var last_node = null;
    var current_node = this.list_header;
    while(current_node.data != data)
    {
        last_node = current_node;
        current_node = current_node.next;
        if (current_node == null) return null;
    }

    return {
        last:last_node,
        current:current_node
    };
};
LinkedList.prototype.find_nodes_from_index_list = function(index)
{
    var first_node = null;
    var second_node = this.list_header;
    for (var i = 0 ; i != index; i++)
    {
        first_node = second_node;
        second_node = second_node.next;
        if (second_node == null) return null;
    }
    return {
        last:first_node,
        current:second_node
    };
};
LinkedList.prototype.remove_node_from_list = function(data)
{
    //在这里写入代码
    var temp = this.find_nodes_from_data_list(data);
    if (temp == null) return null;
    if (temp.last != null)
        temp.last.next = temp.current.next;
    else
        this.list_header = temp.current.next;

    return temp.current;
};
LinkedList.prototype.remove_node_index_from_list = function(index)
{
    //在这里写入代码
    var temp = this.find_nodes_from_index_list(index);
    if (temp == null) return null;
    if (temp.last != null)
        temp.last.next = temp.current.next;
    else
        this.list_header = temp.current.next;
    return temp.current;
};


//测试代码如下
//创建链表的静态方法
LinkedList.create_list_from_array = function(array_data)
{
    var list = new LinkedList();
    for(var i=0;i<array_data.length;i++){
        //var node = new ListNode(array_data[i]);//这样写的话，链表顺序是如何的，输出测试一下
        var node = new ListNode(array_data[array_data.length-i-1]);
        node.next = list.list_header;
        list.list_header = node;
    }
    return list;
};
//测试链表 list
var list = LinkedList.create_list_from_array([1,2,3,"x","y","z"]);
console.log(list);
```
**在链表上实现插入和删除运算 无序移动结点 仅需修改指针**。

#### 头节点的作用作用是对链表进行操作时，可以对空表、非空表的情况以及对首元结点进行统一处理，编程更方便。

### 静态链表  
>  链表具有最大的表长  

### 循环链表  
>  循环链表：是一种头尾相接的链表（即：表中最后一个结点的指针域指向头结点，整个链表形成一个环）。  
>  **优点**：从表中任意结点出发均可找到表中其他结点。  
>  由于循环链表中没有NULL指针，故涉及遍历操作时，其**终止条件**就不再像**非循环链表**那样**判断** p 或 p->next 是否为空，而是**判断它们是否等于头指针**。  
>  单循环链表：  
>>  a1的存储位置是：R->next->next  O(1)
>>  an的存储位置是: R  
### 双向链表
### 双向循环链表
**双向链表的结构可定义如下**  
```
typedef struct DuLNode{
	Elemtype data;
	struct DuLNode *prior,*next;//有前驱指针和后继指针
}DuLNode,*DuLinkList;
```

**双向链表结构的对称性 设指针p指向某一结点**  
>>  p->prior->next = p = p->next->prior  

**双链表的删除结点过程**  
>>  p->prior->next = p->next; p->next->prior = p->prior;  

**双链表的插入结点过程**  
>>  s->prior = p->prior;  
>>  p-prior->next=s;  
>>  s->next=p;  
>>  p->prior = s;  

### 四种存储方式的比较
* {顺序、链式}，{静态、动态}  
1. 顺序存储的固有特点：  
>> 逻辑顺序与物理顺序一致，本质上是用数组存储线性表的各个元素（即随机存取）；存储密度大，存储空间利用率高。  
2. 链式存储的固有特点:  
>> 元素之间的关系采用这些元素所在的节点的“指针”信息表示（插、删不需要移动）  
3. 静态存储的固有特点:  
>> 在程序运行的过程中不用考虑追加内存的分配问题。  
4. 动态存储的固有特点:  
>> 可动态分配内存；有效的利用内存资源，使程序具有可扩展性。  

#### 问：动态顺序表和动态链式表各有哪些优缺点？
>> 动态顺序存储：  
>>> 优点：存储密度大，存储空间利用率高，可**随机存取**。结点空间可动态申请追加。  
>>> 缺点：**插入或删除**元素时**不方便**。  

>> 动态链式存储:  
>>> 优点：**插入或删除**元素时很**方便**，使用灵活。**结点空间**可以**动态申请和释放**；  
>>> 缺点：存储密度小，存储空间利用率低，非随机存取。  

#### 事实上，链表插入、删除运算的快捷是以空间代价来换取时间。  
-------------------------------------------------------------
#### 问：顺序表、链表各自的使用场合?  
>> 顺序表适宜于做**查询**这样的静态操作；  
>> 链表宜于做**插入、删除**这样的动态操作。  
>> 若线性表的长度变化不大，且其主要操作是查找，则采用**顺序表**；  
>>若线性表的长度变化较大，且其主要操作是插入、删除操作，则采用**链表**。  














