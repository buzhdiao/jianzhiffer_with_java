考点    

举例让抽象具体化

热点指数    59617
通过率    30.98%
题目    

包含min函数的栈


具体题目    定义栈的数据结构，请在该类型中实现一个能够得到栈中所含最小元素的min函数（时间复杂度应为O（1））。
讨论    88
Ron
import java.uti  
查看全部
136
C/C++
武汉孙一峰
class Solution {
public:
    
    stack<int> stack1,stack2;
    
    void push(int value) {
        stack1.push(value);
        if(stack2.empty())
            stack2.push(value);
        else if(value<=stack2.top())
        {
            stack2.push(value);
        }
    }
    
    void pop() {
        if(stack1.top()==stack2.top())
            stack2.pop();
        stack1.pop();
        
    }
    
    int top() {
        return stack1.top();        
    }
    
    int min() {
        return stack2.top();
    } 
    
};
应用一个辅助栈，压的时候，如果A栈的压入比B栈压入大，B栈不压，，，，小于等于，AB栈同时压入，出栈，如果，AB栈顶元素不等，A出，B不出。
154
Follow
import java.util.Stack;
思路：用一个栈data保存数据，用另外一个栈min保存依次入栈最小的数
比如，data中依次入栈，5,  4,  3, 8, 10, 11, 12, 1
       则min依次入栈，5,  4,  3，no,no, no, no, 1
no代表此次不如栈
每次入栈的时候，如果入栈的元素比min中的栈顶元素小或等于则入栈，否则不如栈。
public class Solution {
	Stack<Integer> data = new Stack<Integer>();
    Stack<Integer> min = new Stack<Integer>();
    Integer temp = null;
    public void push(int node) {
        if(temp != null){
            if(node <= temp ){
                temp = node;
                min.push(node);
            }
            data.push(node);
        }else{
            temp = node;
            data.push(node);
            min.push(node);
        }
    }
    
    public void pop() {
        int num = data.pop();
        int num2 = min.pop();
        if(num != num2){
           min.push(num2); 
        }
    }
    
    public int top() {
        int num = data.pop();
        data.push(num);
        return num;
    }
    
    public int min() {
        int num = min.pop();
        min.push(num);
        return num;
    }
}
67
Python
Yannyezixin
  思路：利用一个辅助栈来存放最小值 
      栈  3，4，2，5，1
      辅助栈 3，3，2，2，1
  每入栈一次，就与辅助栈顶比较大小，如果小就入栈，如果大就入栈当前的辅助栈顶 
  当出栈时，辅助栈也要出栈 
  这种做法可以保证辅助栈顶一定都当前栈的最小值 
# -*- coding:utf-8 -*-
class Solution:
    def __init__(self):
        self.stack = []
        self.assist = []
        
    def push(self, node):
        min = self.min()
        if not min or node < min:
            self.assist.append(node)
        else:
            self.assist.append(min)
        self.stack.append(node)
        
    def pop(self):
        if self.stack:
            self.assist.pop()
            return self.stack.pop()
    
    def top(self):
        # write code here
        if self.stack:
            return self.stack[-1]
        
    def min(self):
        # write code here
        if self.assist:
            return self.assist[-1]
27
喵之秋
  题目描述    定义栈的数据结构，请在该类型中实现一个能够得到栈最小元素的min函数。     思路       看到这个问题, 我们最开始可能会想, 添加一个成员变量用于保存最小元素, 每次压栈时如果压栈元素比当前最小元素更小, 就更新最小元素.         但是这样会有一个问题, 如果最小元素被弹出了呢, 如何获得下一个最小元素呢?  分析到这里可以发现, 仅仅添加一个成员变量存放最小元素是不够的, 我们需要在最小元素弹出后还能得到次小元素, 次小的弹出后, 还要能得到次次小的.         因此, 用另一个栈来保存这些元素是再合适不过的了. 我们叫它最小元素栈.         每次压栈操作时, 如果压栈元素比当前最小元素更小, 就把这个元素压入最小元素栈, 原本的最小元素就成了次小元素. 同理, 弹栈时, 如果弹出的元素和最小元素栈的栈顶元素相等, 就把最小元素的栈顶弹出.     代码   class Solution {
public:
    void push(int value) {
        s.push(value);
        if(sMin.empty())
            sMin.push(value);
        else if(value <= sMin.top())
            sMin.push(value);
    }
    void pop() {
        if(s.top() == sMin.top())
            sMin.pop();
        s.pop();
    }
    int top() {
        return s.top();
    }
    int min() {
        return sMin.top();
    }
private:
    stack<int> s;
    stack<int> sMin;
}; 
28
Alex-大伟
import java.util.Stack;
public class Solution {
	Stack<Integer> dataStack = new Stack<Integer>();
	Stack<Integer> minStack = new Stack<Integer>();
    
        public void push(int node) {
		dataStack.push(node);
		if(minStack.isEmpty() || node < minStack.peek()){
			minStack.push(node);
		}
		else{
			minStack.push(minStack.peek());
		}
	}
	public void pop() {
		dataStack.pop();
		minStack.pop();
	}
	public int top() {
		return dataStack.peek();
	}
	public int min() {
		return minStack.peek();
	}
}
48
BeACoder
/*
* 1.dataStack为存储数据的栈，minStack为存储最小值的栈；
* 2.push的时候将value值与minStack中的top值比较，小则minStack push value，大则push top值
*/
class Solution {
public:
    stack<int> dataStack, minStack;
    void push(int value) {
        dataStack.push(value);
        if (minStack.empty()) {
            minStack.push(value);
        }
        else{
            int min = minStack.top();
            value<=min?minStack.push(value):minStack.push(min);
        }
        
    }
    void pop() {
        dataStack.pop();
        minStack.pop();
    }
    int top() {
        return  dataStack.top();
    }
    int min() {
        return minStack.top();
    }
};
10
JeffreyWxj
Python大法好 # -*- coding:utf-8 -*-
class Solution:
    def __init__(self):
        self.stack = []
        self.minList = []
    def push(self, node):
        if not self.minList:
            self.minList.append(node)
        else:
            self.minList.append(min(self.minList[-1], node))
        self.stack.append(node)
    def pop(self):
        if not self.stack:
            return None
        self.minList.pop()
        return self.stack.pop()
    def top(self):
        if not self.stack:
            return None
        return self.stack[-1]
    def min(self):
        if not self.minList:
            return None
        return self.minList[-1]
24
Python
华科平凡
python solution: # -*- coding:utf-8 -*-
class Solution:
    def __init__(self):
        self.arr=[]
    def push(self, node):
        # write code here
        self.arr.append(node)
    def pop(self):
        # write code here
        return self.arr.pop()
    def top(self):
        return self.arr[-1]
    def min(self):
        # write code here
        return min(self.arr)
24
马客(Mark)
  每个函数只需一句       first 元素    second 当前最小值      class Solution {
    typedef pair<int, int> pii;
    stack<pii> s;
public:
    void push(int value) {
        s.push(pii(value, ::min(value, s.empty() ? value : min())));
    }
    void pop() {
        s.pop();
    }
    int top() {
        return s.top().first;
    }
    int min() {
        return s.top().second;
    }
};  
8
Java
那就这样
  ArrayList实现 
import java.util.ArrayList;
public class Solution {
    ArrayList<Integer> list = new ArrayList<Integer>();
    
    public void push(int node) {
        list.add(0,node);
    }
    
    public void pop() {
        list.get(0);
        list.remove(0);
    }
    
    public int top() {
        return list.get(0).intValue();
    }
    
    public int min() {
        int temp = top();
        for(int i=1;i<list.size();i++){
            if(temp>list.get(i).intValue()){
                temp = list.get(i).intValue();
            }
        }
        return temp;
    }
}
12
Java
Now_
  简洁的方式：（minNum的即时实现会比延迟实现更方便，延迟实现需要一个额外的栈保存原有栈的内容） 
import java.util.Stack;
public class Solution {
    //记得指定泛型，以免后续需要强制类型转换
	Stack<Integer> stack=new Stack<>();
    Stack<Integer> minNum=new Stack<>();
    
    public void push(int node) {
        stack.push(node);
        if(minNum.isEmpty()) minNum.push(stack.peek()); //Java中获取栈顶:peek()
        else if(stack.peek()<minNum.peek()) minNum.push(stack.peek());
        else minNum.push(minNum.peek());
    }
    
    public void pop() {
        stack.pop();
        minNum.pop();//同步弹出元素
    }
    
    public int top() {
        return stack.peek();
    }
    
    public int min() {
       return  minNum.peek();
    }
}
9
亦心谷
/*
  解题思路： 
  我们可以设计两个栈：StackDate和StackMin，一个就是普通的栈，另外一个存储push进来的最小值。 
首先是push操作： 
  每次压入的数据newNum都push进StackDate中，然后判断StackMin是否为空，如果为空那也把newNum同步压入
  StackMin里；如果不为空，就先比较newNum和StackMin中栈顶元素的大小，如果newNum较大，那就不压入StackMin里，否则
  就同步压入StackMin里。如： 
接着是pop操作 
  先将StackDate中取出的数据value与StackMin的栈顶元素比较，因为对应push操作，value不可能小于
  StackMin中的栈顶元素，最多是相等。如果相等，那么StackMin中也取出数据，同时返回value，否则只是返回value就可以了。 
最后是getMin操作 
　　由上就可知，StackMin中存储的数据就是当前最小的，所以只要返回StackMin中的栈顶元素就可以了。
*/
import java.util.Stack;
public class Solution {
    private Stack<Integer> stackDate;
    private Stack<Integer> stackMin;
    
    public Solution(){
    	stackDate = new Stack<>();
    	stackMin = new Stack<>();
    }
    public void push(int node) {
    	stackDate.push(node);
    	if(stackMin.isEmpty()){
    		stackMin.push(node);
    	}else if(node <= stackMin.peek()){
    		stackMin.push(node);
    	}
    }
    
    public void pop() {
    	 if(stackDate.isEmpty()){
         	throw new RuntimeException("This stack is empty!");
         }
    	 if(stackDate.peek() == stackMin.peek()){
    		 stackMin.pop();
    	 }
    	 stackDate.pop();
    }
    
    public int top() {
    	if(stackDate.isEmpty()){
         	throw new RuntimeException("This stack is empty!");
         }
    	int value = stackDate.pop();
    	 if(value == stackMin.peek()){
    		 stackMin.pop();
    	 }
    	return value;
    }
    
    public int min() {
        if(stackMin.isEmpty()){
        	throw new RuntimeException("This stack is empty!");
        }else{
        	return stackMin.peek();
        }
    }
}
4
C/C++
卷积神经网络哦
两个栈实现 辅助栈放所有的最小值们 class Solution {
public:
    stack<int> s;
    stack<int> s_min;
    void push(int value) {
        if(s.empty() || value <= s_min.top()) s_min.push(value);
        s.push(value);
    }
    void pop() {
        if(s.top() == s_min.top()) s_min.pop();
        s.pop();
    }
    int top() {
        return s.top();
    }
    int min() {
        return s_min.top();
    }
};
6
neuxs
import java.util.Stack;
public class Solution {
    Stack s1=new Stack();
    Stack min=new Stack();
    public void push(int node) {
        if(min.empty()){
            min.push(node);
        }else{
            int top=(int)min.peek();
            if(node<top){
               min.push(node); 
            }else{
                min.push(top);
            }
        }
        s1.push(node);
    }
    
    public void pop() {
        if(!(s1.empty())){
            s1.pop();
            min.pop();
        }
    }
    
    public int top() {
        return (int)s1.peek();
    }
    
    public int min() {
       if(min.empty()){
    	   return 0;
       }
       return (int)min.peek();     
    }
}
3
C/C++
还有个太阳
https://blog.csdn.net/qq_41822235/article/details/82468584本博客对剑指offer经典解法利用两个栈来回倒，辅助栈内存在大量冗余的最小值的情况做下处理。
3
C/C++
东方小龙2129360
class Solution {
public:
    void push(int value) {
        stk.push(value);
        if(smin.empty())
            smin.push(value);
        if(value<smin.top())
            smin.push(value);
    }
    void pop() {
        if(stk.top()==smin.top())
            smin.pop();
        stk.pop();
    }
    int top() {
        return stk.top();
    }
    int min() {
        return smin.top();
    }
    private:
    stack<int> stk;
    stack<int> smin;
};
 
3
溺人深海
让定义栈然后使用栈的相关方法的话感觉怪怪的，所以纯用数组实现了这个
   import java.util.Stack;  
   public class Solution {  
       int data[]=new int[10000];  
       int min[]=new int[10000];  
       int index=0;  
         
       public void push(int node) {  
           data[index]=node;  
           if(index==0){  
               min[index]=node;  
           }else{  
               if(node<min[index-1]){  
                   min[index]=node;  
               }else{  
                   min[index]=min[index-1];  
               }  
           }  
           index++;  
       }  
         
       public void pop() {  
           index--;  
           if(min[index]==data[index]){  
               min[index]=min[index-1];  
           }  
       }  
         
       public int top() {  
           return data[index-1];  
       }  
         
       public int min() {  
           return min[index-1];  
       }  
   }  
2
Java
我去个地方啊
题目描述 定义栈的数据结构，请在该类型中实现一个能够得到栈中所含最小元素的min函数（时间复杂度应为O（1））。 解题思路 思路：利用一个辅助栈来存放最小值 栈 3，4，2，5，1 辅助栈 3，3，2，2，1 每入栈一次，就与辅助栈顶比较大小，如果小就入栈，如果大就入栈当前的辅助栈顶； 当出栈时，辅助栈也要出栈 这种做法可以保证辅助栈顶一定都当前栈的最小值 我的答案 import java.util.Stack;
public class Solution {
    //存放元素
    Stack<Integer> stack1 = new Stack<Integer>();
    //存放当前stack1中的最小元素
    Stack<Integer> stack2 = new Stack<Integer>();
    //stack1直接塞，stack2要塞比栈顶小的元素，要不然就重新塞一下栈顶元素
    public void push(int node) {
        stack1.push(node);
        if(stack2.isEmpty() || stack2.peek() > node){
            stack2.push(node);
        }else{
            stack2.push(stack2.peek());
        }
    }
    //都要pop一下
    public void pop() throws Exception{
        if(stack1.isEmpty()){
           throw new Exception("no element valid"); 
        }
        stack1.pop();
        stack2.pop();
    }
    public int top(){
        if(stack1.isEmpty()){
           return 0;
        }
        return stack1.peek();
    }
    public int min(){
        if(stack2.isEmpty()){
           return 0;
        }
        return stack2.peek();
    }
}
2
C/C++
idea201802062116815
骚套路...
class Solution {
public:
    void push(int value) {
        deq.push_back(value);
    }
    void pop() {
       deq.pop_back(); 
    }
    int top() {
        return deq.front();
    }
    int min() {
        return *std::min_element(deq.begin(),deq.end());
    }
    deque<int> deq;
};
 
2
虵乡遇故知
  使用两个栈，一个栈用作正常接收数据，另外一个栈作为辅助栈记录每次添加数据时候的最小值，可以实现从栈中以O(1)的时间复杂度得到栈中的最小值，需额外空间O(N)。  import java.util.Stack;
public class Solution {
    Stack<Integer> stack = new Stack<Integer>();
    Stack<Integer> help = new Stack<Integer>();
    
    public void push(int node) {
        if (!stack.isEmpty() && !help.isEmpty()) {
            stack.push(node);
            if (node < help.peek()) {
                help.push(node);
            } else {
                help.push(help.peek());
            }
        } else {
            stack.push(node);
            help.push(node);
        }
    }
    
    public void pop() {
        if (!stack.isEmpty() && !help.isEmpty()) {
            stack.pop();
            help.pop();
        }
    }
    
    public int top() {
        int res = 0;
        if (!stack.isEmpty() && !help.isEmpty()) {
            res = stack.peek();
        }
        return res;
    }
    
    public int min() {
        int min = Integer.MAX_VALUE;
        if (!stack.isEmpty() && !help.isEmpty()) {
            min = help.peek();
        }
        return min;
    }
}
 
