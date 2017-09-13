# 字符数组和字符串
> char a[10]={'a','b','c','d','e'};

       前面5个元素被初始化好了,其他元素将被初始化为'\0';

> char c[]={'C','h','i','n','a'};

> char c[]="china"

       得到的结果是在数组的最后面多了一个'\0';
       程序自动把六个字符赋给了数组;
       所有的字符串都是以'\0'结尾的;
       所有以'\0'结尾的字符数组都可以当做字符串;
       char c[5]="China";是不可以的

# 关于赋值
    char c[6]="China";
    char c[]={'C','h','i','n','a'};
    只有在初始化字符数组的时候才能用赋值运算符.
    不能用赋值语句将一个字符串常量或字符数组直接赋给另一个字符数组。
    不是在字符串定义的时候，是不可以直接赋值的。
    str1[]="China";不合法
    str1="China";不合法
    str2=str1;不合法

> 正确的赋值方式：


    ＃include <iostream>
    using namespace std;
    int main()
    {
      char str1[]="C++language",str2[20];
      int i=0;
      while(str[i]!='\0')
      {
        str2[i]=str1[i];
        i++;
      }
      str2[i]='\0';
      cout<<"String1:"<<str1<<endl;
      cout<<"String2:"<<str2<<endl;
      return 0;
    }

# 利用二维数组存储多个字符串

> 例：

    　　char　weekday[7][11]={"Sunday","Monday","Tuesday","Wednesday","Thursday","Friday","Saturday"};

# 字符字符数组字符串的输入和输出

> 输入缓冲区：


      键盘上输入之后，进入输入输入缓冲区，程序来输入缓冲区提取，利用cin>>str;语句提取；

      输入缓冲区有个指针标记哪些字符被读取了，指针只能往后移动；

      对于cin而言会把空格的回车都当做输入命令；

> 利用cin 流读取数据：

    　　　 #include <iostream>
          using namespace std;
          int main(){
            float grade;
            cout<<"enter grade:";
            while(cin>>grade)
            {
              if(grade>=85)
                  cout<<grade<<"GOOD!"<<endl;
              if(grade<60)
                  cout<<grade<<"fail"<<endl;
            }
            return 0;
          }

    意味着只要能从键盘上读入一个合法的数字，就能把它赋给了grade就能不断的进行这个循环，如果不能成功的读到合法的数字时就跳出这个循环。

# 一个字符的输入

* 1.直接用cin输入：


       　#include <iostream>
         using namespace std;
         int main()
         {
           char c;
           cout<<"enter a sentence:"<<endl;
           while (cin>>c)
           cout<<c;
           return 0;
         }
     用cin，他会把所有空格和回车当做输入字符之间的间隔符，当做只是用来区分不同的数据的。
     当你想要终止输入，^Z（ctrl加z)是一个输入结束标志；

* 2.用cin.get()函数输入字符
> cin.get()函数

  　　可以用于读入一个字符；

  　　两种形式：cin.get();cin.get(char);

      　#include <iostream>
      using namespace std;
      int main()
      {
        char c;
        cout<<"enter a sentence:"<<endl;
        while((c=cin.get())!=EOF)
        cout<<c;
        return 0;
      }

      cin.get()是一个函数就像一个功能一样，只要调用，就会从缓冲区读一个字符把它赋给c,如果这个赋值的部分不等于EOF：文件结束标志，就是输入的结束；

      cin.get()不会跳过空格也不会跳过回车；

* 3.
> cin.get(char)


         #include<iostream>
         using namespace std;
         int main()
         {
           char c;
           cout<<"enter a sentence:"<<endl;
           while(cin.get(c))//读取一个字符赋给字符变量c
           cout<<c;
           return 0;
         }

     cin.get(c)相当于从键盘上读入一个字符并把它赋值给c，而且如果读入的是错误的时候，cin.get(c)函数就返回一个0；

* 4 用getchar()输入字符


         #include <iostram>
         using namespace std;
         int main()
         {
           char c;
           cout<<"enter a sentence:"<<endl;
           while(c=getchar())//不跳过任何字符
           cout<<c;
           return 0;
         }

# 一串字符的输入输出
>　一串字符的输出：

    　　　#include <iostream>
         using namespace std;
         int main()
         {
           char a[10]="Computer";
           cout<<a;
           return 0;
         }         

     cout 一个字符数组是为了不输出乱码，要确保字符数组是以‘\0’结尾的。

>　二维输出

    　　　#include <iostream>
         using namespace std;
         int main()
         {
           char weekday[7][11]={"Sunday","Monday","Tuesday","Wednesday","Thursday","Friday","Saturday"};
           for(int i=0;i<7;i++)
           cout<<weekday[i]<<endl;
           return 0;
         }

          weekday[i]只有一个下标，定义一个二维数组实际上就相当于定义多个一维数组，所以可以把某个一维数组输出，就相当于输出了七行中的某一行。

> int a[8]={1,2,3，4,5,6}；时，可以cout<<a<<endl;吗

      a 对于普通的数组而言，代表了数组的起始地址。

## 一串字符的输入
* 1.直接用cin输入字符串

  　　　#include <iostream>
       using namespace std;
       int main()
       {
         char str[10];
         cout<<"enter a sentence:"<<endl;
         while(cin>>str)
         cout<<str<<endl;
         return 0;
       }

* 2.用cin.get()函数输入

> 有３个参数的get函数

    cin.get(ch,10,'\n');//ch是字符数组的名字，10为要从输入缓冲区读取的字符个数
    (1)读取10-1个字符（包括空格），赋给制定的字符数组；
    (2)如果在读取10-1个字符之前，遇到指定的终止字符'\n'，则提前结束读取，如果第3个参数没有指定，则默认为'\n'；
    (3)读取成功返回非零值，如失败则返回0值；

> 例子:

      #include <iostream>
      using namespace std;
      int main()
      {
        char ch[20];
        cout<<"enter a sentence:"<<endl;
        cin.get(ch,10,'o');指定终止符为'o';
        cout<<ch<<endl;
        return 0;
      }
* 3.用cin.getline()函数输入

> 一个特别需要关注的程序：

      #include<iostream>
      using namespace std;
      int main()
      {
        char a[10][10];
        int n=0;
        cin>>n;
        for(int i=0;i<n;i++)
          cin.getline(a[i],10);
        for(int i=0;i<n;i++)
          cout<<a[i]<<endl;
          return 0;
      }

      因为在程序中首先使用了cin读取了数据7，然后又使用getline去读取后面的字符串。

> 纠正：

      在cin>>n后面，加上cin.get();可以读走多余的换行符号。

# 字符串例题

> 字符串连接

      #include <iostream>
      #include <string>
      using namespace std;
      int main()
      {
        char str1[20],str2[20];
        cin.getline(str1,20);
        strcpy(str2,str1);
        cout<<str1<<endl;//数字名就是字符串名
        cout<<str2<<endl;
      }

> 不用系统函数：

       #include <iostream>
       using namespace std;
       int main()
       {
         int len1,len2;char str1[40],str2[40];
         cin.getline(str1,20);cin.getline(str2,20);
         for(len1=0;str[len1]!='\0';len1++);
         for(len2=0;str2[len2]!='\0';len2++);
         if(len1>=len2)
         {
           for(len2=0;str2[len2]!='\0';len2++)
            str1[len1++]=str2[len2];
            str1[len1]='\0';
         }
         else
         {
           for(len1=0;str2[len1]!='\0';len1++)
           str2[len2++]=str1[len1];
           str2[len2]='\0';
         }
         cout<<str1<<endl;
         cout<<str2<<endl;
         return 0;
       }

> 统计单词数：

       #include<iostream>
       using namespace std;
       int main()
       {
         char str[80];
         int num=0;flag=0;//flag用来记录当前单词之前我读到的是单词还是空格
         cin.getline(str,80);
         for(int i=0;str[i]='\0';i++)
         {
           if(str[i]=='')
              flag=0;
           else if(flag==0)//当前读到的不是空格而且在当前字符之前我读到的是空格，意味着发现了一个新的单词
           {
             flag=1;num++;
           }
         }
         cout<<"字符串中有"<<num<<“个单词”<<endl;
         return 0;
       }
