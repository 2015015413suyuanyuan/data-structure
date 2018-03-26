# 数据结构
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

## 第三章 栈和队列
* 栈的定义  
栈：线性表  
>>  限定仅在表尾进行插入或删除操作。  
>>  后进先出(LIFO结构)  

![](http://m.qpic.cn/psb?/V12SqnDn3ERdXU/4zWEvvOJNTEKULeqV4eP6hrguj7WYt5a3FOqcOmFng4!/b/dEQBAAAAAAAA&bo=TgEFAQAAAAARB3s!&rf=viewer_4)

* 顺序栈  
**顺序栈**：利用一组地址连续的存储单元依次存放自栈底到栈顶的数据元素，同时附设指针top指示栈顶元素在顺序栈中的位置。  
>> 栈空，再进行元素“出栈”操作，将产生“下溢”。  
>> 栈满，再进行元素“进栈”操作，将产生“上溢”。  

* ADT:  
```
    #define STACK_INIT_SIZE 100// 栈存储空间的初始分配量  
    #define STACKINCREMENT 10   // 栈存储空间的分配增量   
    typedefstruct{
    	SelemType *base; //栈底指针，它始终指向栈底的位置。
    	SelemType *top; //栈顶指针。
    	int stacksize; //当前分配的栈可使用的最大存储容量。
    }Sqstack;
```
    
**注意**：base的值为NULL,表明栈结构不存在。  
>> 判断栈为空的条件是： S.top == S.base  
>> 判断栈为满的条件是： S.top == S.base + m0

### 栈的应用
![](http://m.qpic.cn/psb?/V12SqnDn3ERdXU/tkXlj1cu*8WMXSHPVGmp4xmSO.JP7dxTNwcCcOw3WEU!/b/dEEBAAAAAAAA&bo=YAOAAgAAAAARF8E!&rf=viewer_4)

![](http://m.qpic.cn/psb?/V12SqnDn3ERdXU/TBJ.sw5oDjTRkePNaB7EbL4HA2DEOhqyjAs3VUmXArE!/b/dEQBAAAAAAAA&bo=jQNrAgAAAAARF8c!&rf=viewer_4)

* 栈与递归的实现   
**递归**：一个直接调用自己或通过一系列的调用语句间接调用自己的函数，称做递归函数  



### 队列
**队列**：线性表  
>> 限定在表的一端插入（对尾），另一端删除（对头）。  
>> 先进先出（FIFO结构）。  

![](http://m.qpic.cn/psb?/V12SqnDn3ERdXU/gT80DWftI4A8cQAJ1DGZHFveCCneNLZD7mo9rBHSrSY!/b/dAgBAAAAAAAA&bo=FwK3AAAAAAARB5I!&rf=viewer_4)

>>当队列中没有元素时，称为**空队列**。

#### 双端队列
**双端队列**：线性表  
>> 限定插入和删除在表的两端进行。  
>> 先进先出（FIFO结构）。  
> 输出受限的双端队列：一个端点可插入和删除，另一个端点仅可插入。  
> 输入受限的双端队列：一个端点可插入和删除，另一个端点仅可删除。  

#### 链队列——队列的链式表示和实现
**链队列**：  
> 用链表表示的队列。  
> 限制仅在表头删除和表尾插入的单链表。

**一个链队列由一个头指针和一个尾指针唯一确定**。  
（因为仅有头指针不便于在表尾做插入操作）。

  为了操作的方便，也给链队列添加一个头结点，因此，**空队列**的判定条件是：**头指针和尾指针都指向头结点**。 
 
![](http://m.qpic.cn/psb?/V12SqnDn3ERdXU/BAdQgZPT4ZCT4b4kjlMG91zdcUPJ*.BvMA9ukhYM9mE!/b/dFYBAAAAAAAA&bo=KQPlAAAAAAARB*8!&rf=viewer_4)

**用C语言定义链队列结构如下**：  

    typedef struct QNode 
    {  QElemtypedata; 
    struct QNode  *next; 
    } Qnode,  *QueuePtr;   // 定义队列的结点 
    typedef struct 
    {  QueuePtr   front;// 队头指针 
       QueuePtr   rear;  // 队尾指针 
    }LinkQueue; 
    

![](http://m.qpic.cn/psb?/V12SqnDn3ERdXU/Z8RBNxU6bz9zTzofHb3p.2dAs*D*oZzrjU0jHqgiRoA!/b/dJEAAAAAAAAA&bo=ZwNwAgAAAAARByY!&rf=viewer_4)
    

![](http://m.qpic.cn/psb?/V12SqnDn3ERdXU/dIBr7M6KSb19VGq.Gynge5NbYVvLmoeGVcAa1BolkcE!/b/dGgBAAAAAAAA&bo=RQOAAgAAAAARF.Q!&rf=viewer_4)


![](http://m.qpic.cn/psb?/V12SqnDn3ERdXU/TnR3nyjAtJiIsRowj9fHfWjCxe3q2YcM6uR7cpvsDd0!/b/dEUBAAAAAAAA&bo=KAOAAgAAAAARF4k!&rf=viewer_4)


### 循环队列

##### 顺序队列

> 是限制再表头删除和表尾插入的顺序表。  
>  利用一组**地址连续**的存储单元**依次存放**队列中的数据元素。  
>  因为：对头和对尾的位置是变化的，所以：设头、尾指针。  

**头尾指针**  
  
* 初始化时的初始值均应置为0。  
* 入队，尾指针增1  
* 出队，头指针增1  
* **头尾指针**相等时队列为空  
* 在非空队列里，头指针始终指向对头元素  
* 尾指针适中指向对尾元素的下一个位置 



![](http://m.qpic.cn/psb?/V12SqnDn3ERdXU/mE2kpnwE6D5UA36qVTA4u6rpON7ZonT4U8SNLLgqRTI!/b/dHMAAAAAAAAA&bo=KQPlAAAAAAARF.8!&rf=viewer_4)

 
**这样会出现溢出的问题**  

**解决 假溢出 的问题  所以提出了  循环队列**  

----------

#### 循环队列
* 少用一个元素的空间，约定入队前测试尾指针在循环移一下加1后是否等于头指针，若相等则认为队满；  


![](http://m.qpic.cn/psb?/V12SqnDn3ERdXU/664WkZT*76dOrB0Rfz*HKIuP4KQrFnCH26SSa1dirE0!/b/dAgBAAAAAAAA&bo=IgITAQAAAAARBwI!&rf=viewer_4)

* 循环意义下的加1操作可以描述为：  

    if(rear + 1 >= MAXQSIZE)  
    rear=0;  
    else  
    rear++;  

* 利用模运算可简化为： **rear = (rear +1)% MAXQSIZE**

* 判断循环队列，队满的条件是：**(rear +1)% MAXQSIZE == front**
 
*  判断循环队列，队空的条件是：**Q.front = Q.rear =0**
  
*  求循环队列的长度：**（Q.rear - Q.front + MAXQSIZE) % MAXQSIZE**
* 插入操作：**Q.rear =(Q.raer +1) % MAXQSIZE**

* 删除操作： **Q.front = (Q.front+1) % MAXQSIZE** 


#### 队列的应用
* 杨辉三角的计算  
* CPU资源的竞争问题  
* 主机与外部设备之间速度不匹配的问题


## 数组的定义
* 数组：按一定格式排列起来的，具有**相同类型**的数据元素的集合。  
* 一维数组：若线性表中的数据元素为非结构的简单元素，则称为一维数组。  
* 一维数组的逻辑结构：线性结构。定长的线性表。  
* 声明格式：  数据类型  变量名称[长度]；  
* 例如：int num[5]={0,1,2,3,4};  

* 二维数组：若一维数组中的数据元素又是一维数组结构，则称为二维数组。  
* 二维数组逻辑结构  

> 非线性结构：
>> 每一个数据元素既在一个行表中，又在一个列表中。  
> 线性结构:  
>> 定长的线性表，该线性表的每个数据元素也是一个定长的线性表。  

### 数组的顺序表示和实现  
* 一般都是采用**顺序存储**结构来表示数组。  
> 两种顺序存储方式  
>> 以行序为主序（低下标优先）  
>> 以列序为主序（高下标优先）  

#### 以行序为主序存放：
* 二维数组中任一元素aij的存储位置  
* LOC(i,j) = LOC(0,0)+(b2 * i + j ) *L  
> 某个元素的地址就是它前面所有行所占的单元加上它所在行前面所有列元素所占的单元数之和。  

#### 按列序为主序存放
* 二维数组中任一元素aij的存储位置  
* LOC(i,j) = LOC(0,0) + (b1*j+i)*L  
> 某个元素的地址就是它前面所有列所占的单元加上它所在列前面所有行元素所占的单元数之和。  

* 例 1：一个二维数组 A，行下标的范围是 1 到 6，列下标的范围是 0 到 7，每个数组元素用相邻的6个节存储，存储器按字节编址。那么，这个数组的体积是**288**个字节。  

* 答： Volume = m×n×L = (6 – 1 + 1) ×(7 – 0 + 1) ×6 = 48×6 = 288 

* 例 2：设数组 A[0…59, 0…69] 的基地址为 2048，每个元 素占 2 个存储单元，若以列序为主序顺序存储，则元素  A[31, 57] 的存储地址为**8950**。

* 答：LOC(i, j) = LOC(31, 57) = LOC(0, 0)+(b1×j＋i )×L = 2048 + (60×57＋31 )×2 = 8950 

### 广义表的定义

* 广义表是n>=0个元素  的 有限序列，其中每一个ai或者是原子，或者是一个子表。  
* 拓宽的线性表是广义表。  
* 表头：LS的第一个元素a1就是表头。  
* 表尾：除表头之外的其他元素组成的表。  
* 注意：表尾不是最后一个元素，而是一个子表。  

#### 广义表的性质
1. 广义表中的数据元素有相对次序；  
2. 广义表的长度定义为最外层所包含元素的个数;  
3. 广义表的深度定义为该广义表展开后所含括号的重数；A(b,c)的深度为1，B(A,d)的深度为2；  
4. 广义表可以为其他广义表共享；如：广义表B就共享广义表A。在B中不必列出A的值，而是通过名称来引用。  
5. 广义表可以是递归的表。注意：递归表的是无穷值，长度是有限值。  

## 数和二叉树

![](http://m.qpic.cn/psb?/V12SqnDn3ERdXU/Pp7aYbaqWU43M5UoXHpWoxLAsNiahG2kC114wVIdDP4!/b/dGoBAAAAAAAA&bo=ZwKlAQAAAAARB*E!&rf=viewer_4)

### 数的定义
> 树 是n个结点的有限集。  
>> 1.有且仅有一个特定的称为根的结点；  
>> 2.其余结点可以分为m个互不相交的有限集，其中每一个集合本身又是一棵树，并称为根的子树。
> 显然，树的定义是一个递归的定义。  

#### 基本术语
* 结点的度：结点的子树个数；  
* 树的度：树的所有结点中最大的度数；  
* 叶结点：度为0的结点；  
* 树的深度：树中所有结点中最大层次是这棵树的深度；  
* 森林是m棵互不相交的树的集合。  

### 二叉树
* 定义：二叉树是n个结点的有限集，它或者是空集（n=0）,或者由一个根结点及两棵互不相交的分别称作这个根的左子树和右子树的二叉树组成。  
* 特点：  
1. 每个结点最多有俩孩子（二叉树不存在度大于2的结点）。  
2. 子树有左右之分，其次序不能颠倒。  
3. 二叉树可以是空集合，根可以有空的左子树或空的右子树。

**注意**：二叉树不是树的特殊情况，它们是两个概念。  

#### 二叉树的性质
性质1： 在二叉树的第i层上，至多有2的i-1次方个结点  
性质2： 深度为 k 的二叉树至多有 2k－1 个结点（k ≥1)。  
性质3： 对任何一棵二叉树 T，如果其叶子数为 n0，度为2的结点数为 n2，则 n0 = n2 + 1。  
  
#### 满二叉树
* 一棵深度为 k 且有 2k- 1 个结点的二叉树,称为满二叉树。  

![](http://m.qpic.cn/psb?/V12SqnDn3ERdXU/f66hoV8VaStNEPdkKeh2QE2C6y5KFZ09Kgm5YxwlZA4!/b/dEMBAAAAAAAA&bo=AQGYAAAAAAARB6g!&rf=viewer_4)

#### 完全二叉树
* 深度为 k 的具有 n 个结点的二叉树，当且仅当其每一个结点都与深度为 k 的满二叉树中编号为 1~ n 的 结点一一对应时，称之为完全二叉树。                           

![](http://m.qpic.cn/psb?/V12SqnDn3ERdXU/Xvs8Yg5LeUiRRwGSfUOZyl2SGeAbhkEholYvHcOX4sc!/b/dFYBAAAAAAAA&bo=xwGwAAAAAAARB0Y!&rf=viewer_4)

#### 遍历二叉树
* 遍历概念  
> 顺着某一条搜索路径寻访二叉树中的结点，使得每个结点均被访问一次，而且仅被访问一次。（不破坏原来的数据结构。）  

* 遍历的目的：得到树中所有结点的一个线性排列。  
* 遍历的方法：先（根）序遍历、中序遍历、后序遍历  

![](http://m.qpic.cn/psb?/V12SqnDn3ERdXU/KtUDECIsPlPnDg.TdiaqCQDYdp750EN9SBmYtnuD2tA!/b/dEMBAAAAAAAA&bo=YQK.AQAAAAARB.w!&rf=viewer_4)

![](http://m.qpic.cn/psb?/V12SqnDn3ERdXU/4adgc.KMdHnxEJe6*dMhxx0opWZNOdhvcRipJeq60zw!/b/dFsBAAAAAAAA&bo=YQKxAQAAAAARB.M!&rf=viewer_4)

![](http://m.qpic.cn/psb?/V12SqnDn3ERdXU/oqyjM8pP.k.xqtY7yF6Jd*vkhVo4u69Hap4UZbLkuqk!/b/dGgBAAAAAAAA&bo=awK4AQAAAAARB.A!&rf=viewer_4)

![](http://m.qpic.cn/psb?/V12SqnDn3ERdXU/3iG*LprqPOyHjfawKkwmpXyLm9xVuILbmi.uXfT8svg!/b/dGoBAAAAAAAA&bo=SgKWAQAAAAARB.8!&rf=viewer_4)

1. 二叉树的前序遍历序列中，任意一个结点均处在其子女结点的前面， 这种说法（ A  ）（A）正确 

2. 由于二叉树中每个结点的度最大为 2，所以二叉树是一种特殊的树，这种说法（B   ） （B）错误
 
3. 已知某二叉树的后序遍历序列是 dabec。中序遍历序列是 debac，它的前序遍历序列是（ D  ）（D）cedba
 
4. 某二叉树的前序遍历结点访问顺序是 abdgcefh，中序遍历的结点访问顺序是 dgbaechf，则其后序遍历的结点访问顺序是（   D ）。（D）gdbehfca 

5. 在一非空二叉树的中序遍历序列中，根右边（A） （A）只有右子树上的所有结点

6. 任一二叉树的叶子结点在先、中和后序遍历序列中的相对次序 (  A )  。 （A）不发生改变


### 二叉树的存储结构
1. 顺序存储结构  
> 完全二叉树：用一组地址连续的存储单元一次自上而下、自左至右存储结点元素，即将编号为i的结点元素存储在一维数组中下标为i-1的分量中。  
> 一般二叉树：将其每个结点与完全二叉树上的结点相对照，存储在一维数组的相应分量中。

**此顺序结构仅适用于完全二叉树**  

2. 链式存储结构  
* 二叉树结点的构成  
* 存储方式  
**在n个结点的二叉链表中有n+1个空指针域**。  

C语言的类型描述如下：
    
    typedef struct BiTNode { // 结点结构
       TElemType  data;
       struct BiTNode  *lchild, *rchild; // 左右孩子指针
    } BiTNode, *BiTree;
 
### 线索二叉树
**线索化**:对二叉树按某种次序遍历使其变为线索二叉树的过程。

二叉树线索化的目的：利用线索化后的二叉树中的线索就可以直接找到某些结点在某种遍历序列中的前驱和后继结点。  
二叉树线索化的实质：在遍历过程中用线索取代空指针。

在线索树（中序）中找结点后继的方法：  
1. 若右链是线索，则直接指示后继  
2. 若右链是指针，则“右孩找左”。即：**中序后继右孩找左**。

在线索树（中序）中找结点前驱的方法：  
1. 若左链是线索，则直接指示前驱  
2. 若右链是指针，则“右孩找左”。即：**中序前驱左孩找右**。

在线索树上进行遍历的方法：  
1. 从序列中第一个结点起，依次找后继，直至后继为空。  
2. 从序列汇总最后一个结点起，依次找前驱，直至前驱为空。  


线索二叉树的存储表示：  

    typedef enum PointerTag { Link, Thread }; 
    // Link == 0：指针，Thread == 1：线索 
    typedef struct BiThrNode {
       TElemTypedata;  
       struct BiThrNode   *lchild,  *rchild; // 左右指针 
       PointerTagLTag,  RTag; // 左右标志 
    } BiThrNode,  *BiThrTree; 


课堂练习
选择题 
1. 在线索化二叉树中，t 所指结点没有左子树的充要条件是: t -> ltag==1且t -> lchild==NULL 

2. 二叉树按某种顺序线索化后，任一结点均有指向其前趋和后继的线索，这种说法 **错误**  
	> 只有空指针的地方才能加指向前驱或后继的线索，有左／右子女的结点，其左／右指针指向左／右子女。

### 哈夫曼树及其应用

问题：什么是哈弗曼树？  
>> 判别树：用于描述分类过程的二叉树。  

* 基本概念：  
* 路径：从树中的一个结点到另一个结点之间的分支构成这两个结点间的路径。  
* 结点的路径长度：两结点间路径上的分支树。  
* 树的路径长度：从树根到每个结点的路径长度之和。  

**完全二叉树是路径长度最短的二叉树**

* 权：将树中结点赋给一个有着某种含义的数值，则这个数值称为该结点的权值。  
* 结点的带权路径长度：从根结点到该节点之间的路径长度与该结点的权的乘积。  
* 树的带权路径长度：树中所有叶子结点的带权路径长度之和。  

哈夫曼树：最优树（带权路径长度最短的树）  

哈弗曼树：最优二叉树（带权路径长度最短的二叉树）  

* 满二叉树不一定是哈弗曼树。  
* 哈弗曼树中权越大的叶子离根越近。  
* 具有相同带权结点的哈夫曼树不唯一。  

* 满二叉树不一定是哈夫曼树。    
* 哈弗曼树中权越大的叶子离根越近。  
* 具有相同带权结点的哈弗曼树不唯一。  
* 包含n个叶子结点的哈弗曼树中共有2n-1个结点。  
* 哈弗曼树的结点度数为0或2，没有度为1的结点。  
* 包含n棵树的森林要经过n-1次合并才能形成哈夫曼树，共产生n-1个新结点。
* 
![](http://m.qpic.cn/psb?/V12SqnDn3ERdXU/C3xsx1UJbdw1rLj3.I3MweptXyfsf2id4UalxLL4F9o!/b/dEIBAAAAAAAA&bo=1QPcAdUD3AERGS4!&rf=viewer_4)

 ![](http://m.qpic.cn/psb?/V12SqnDn3ERdXU/1DXfwTv.Ba6ccb921hjSBdWplvdOtrt*VeSYPbpalTk!/b/dFsBAAAAAAAA&bo=ggKvAQAAAAARBx4!&rf=viewer_4)  

![](http://m.qpic.cn/psb?/V12SqnDn3ERdXU/qR4tpCDOdEpZ8mOmQZjuJDW8HKuxeGUhWYPSv7.aKXo!/b/dFsBAAAAAAAA&bo=hANtAgAAAAARF8g!&rf=viewer_4)

![](http://m.qpic.cn/psb?/V12SqnDn3ERdXU/T6Ieu0.lY4kz5MlNYwMnyBJkoFI.Vq.veDKQUqBsv24!/b/dEUBAAAAAAAA&bo=lAKVAQAAAAARFyI!&rf=viewer_4)

## 图
* 图时一种非线性结构。  

图的特点：  
* 顶点之间的关系是任意的。  
* 图中任意两个顶点之间都可能相关  
* 顶点的前驱和后继个数无限制  

* 定义  
>> 图是一种：数据元素间存在多对多关系的数据结构。  

* 基本术语：  
1. 顶点：图中的数据元素。  
2. 弧：<v,w>表示从v到w的一条弧，且称v为弧尾，称w为弧头，此时的图称为有向图。  
3. 边：(v,w)代表v和w之间的一条边，此时的图称为无向图。  

1.无向图中边的取值范围：0<=e<=n(n-1)/2  (n表示图中顶点数，e表示边的数目)
>> 完全图：有n(n-1)/2条边的无向图称为完全图。

2.有向图中弧的取值范围：0<=e<=n(n-1)  

>> 有向完全图：有n(n-1)条弧的有向图（即：每两个顶点之间都存在着方向相反的两条弧）称为有向完全图。  

* 权：与图的边或弧相关的数，这些数可以表示从一个顶点到另一个顶点的距离或耗费。

* 网：带权的图。  
* 子图：如果图 G = (V, E) 和 G´= (V ´, E´)，满足： 称 G´为G 的子图。  

* 度：无向图中顶点v的度是和v相关联的边的数目，记为：TD(V)    
* 入度：有向图中以顶点v为头的弧的数目称为v的入度，记为：ID(v)。m 
* 出度：有向图中以顶点v为尾的弧的数目称为v的出度，记为OD(v)  
* 度：入度和出度的之和，即：TD(v)=ID(v)+OD(v)  

回路（环）：第一个顶点和最后一个顶点相同的路径。



