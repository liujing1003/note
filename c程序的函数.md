# 函数的定义：
> 常用的函数：


    已知一个函数，求其平方根：
       r=sqrt(100.0);

    已知底数x，幂指数y,求x^y：
       k=pow(x,y);

    求一个字符串的长度：
       i=strlen(str1);

    比较两个字符串的大小：
       v=strcmp(str1,str2)

    把字符串转换为相应的整数:
       n=atoi(str1);
* 定义一个函数：

       int absolute(int n)
       {
         if(n<0)
             return(-n);
         else
             return n;
       }
       括号里会写输入参数，前面指定返回值的类型。

# 函数调用的方式：
* 1.函数调用作为独立语句：
      stringPrint();

      调用函数完成某项功能，没有任何的返回值。
* 2.函数作为表达式的一部分：
      number=max(numA,numB)/2;
* 3.以实参形式出现在其他函数的调用中：
      number=min(sum(-5,100),numC);

> 例1.定义一个没有参数的函数：

      int get_int()
      {
        int n=0;
        cout<<"Please input an integer:"<<endl;
        cin>>n;
        return n;
      }

> 定义一个没有返回值的函数:

     void delay(int n)
     {
       for(int i=0;i<n*100000;i++);
       return;
     }
     //延时函数

> 既不需要参数也不需要返回值

    void show()
    {
      cout<<"***********"<<endl;
      cout<<"* System error has occurred. *"<<endl;
      cout<<"***********"<<endl;
    }

> main函数：
   * 一个程序里有多个文件：

         #include <iostream>
         #include"max.h"//max.h是另外的文件

> 函数的原型：

      函数的原型=返回值类型+函数名+参数类型

      其中参数可以不写名字：bool checkPrime (int)

# 函数的执行过程：

      首先在内存中开辟一片空间把main函数放进去，然后开始执行main函数，当我们执行到要调用别的函数时，内存新开辟一片内存空间把调用的函数放进去，之后main把两个参数传递到调用的函数在的内存空间，当接收到参数后开始运行函数一直运行到函数结束，返回一个返回值到main函数里，之后，被调用函数所在的内存空间被释放掉。

> 函数参数的传递：

       （1）实参和形参具有不同的存储空间，实参与型参变量的数据传递是“值传递”
       （2）函数调用时，系统给形参分配存储单元，并将实参对应的值传递给形参；
       （3）实参和形参的类型要相同或可以兼容

# 变量的作用范围

>例子：

     #include <iostream>
     using namespace std;
     int a=0,b=0;
     void change()
     {
       int p;
       if(a<b)
       {
         p=a;a=b;b=p;
       }
     }
     int main()
     {
       cin>>a>>b;
       exchange();
       cout<<a<<" "<<b<<endl;
       return 0;
     }

分析：

    定义了两个全局变量，不在任何函数里面，main函数开始运行，cin>>a>>b;这个a,b指的是全局变量a,b，要在mian 函数里伸出一只手来改变main函数外的a和b；main函数继续执行到了exchange，exchang开始执行，他要判定全局变量a和b的大小，并对伸出一只手对全局变量ab进行操作，ab就进行了互换,打印的ab也是全局变量ab.
* 当全局变量与局部变量同名时，局部变量将在自己作用域内有效，他将屏蔽同名的全局变量。

# 数组做函数参数

> 数组元素做函数参数：

       #include <iostream>
       using namespace std;
       void change(int a,int b)
       {
         a=30;b=50;
       }
       int main()
       {
         int a[2]={3,5};
         change(a[0],a[1]);
         cout<<a[0]<<" "<<a[1]<<endl;
         return 0;
       }

    输出：3 5

>
    #include<iostream>
    using namespace std;
    void change(int a[])
    {
     a[0]=30;a[1]=50;
    }
    int main()
    {
    int a[2]={3,5};
    change(a);
    cout<<a[0]<<" "<<a[1]<<endl;
    return 0;
    }

    想把数组传递给某一个函数时，就可以按这种方式定义函数的形式参数。

    输出：30 50
* 数组的名字不是变量是一个常量代表着数组的地址

* 当数组名作为参数访问change函数时，就相当于change函数伸出了一双手到存储数组的内存空间进行运行。
