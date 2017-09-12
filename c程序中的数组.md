# 一维数组
> 定义:
     类型   数组名[常量表达式]


> 补充说明:

      (1)const int i=4;//定义了一个符号常量
      int a[i]={};//可以的,但并不是一个可变长数组

      (2)define N 4//在程序里我定义了一个N,在程序中出现N,就把它当成4,写在main函数之前.后面可以用int a[N]={};

# 二维数组
> 定义

      int a[3][4];
      得到了三个一维数组;

> 输出:
通过两个互相嵌套的for循环:
cout<<setw(3)<<a[i][j];//设置了后面输出的量占三个字符位.

# 三维数组
> 定义:

       int a[5][3][4];//片行列

# 数组的作用

> 例1:数字统计;

      #include<iostream>
      using namespace std;
      int main()
      {
        int num,count[10]={0};
        for(int i=0;i<20;i++)
        {
          cin>>num;
          for(int j=0;j<10;j++)
          {
            if(num==j)   count[j]++;
          }
        }
        for(int i=0;i<10;i++)
        {
          if(count[i]!=0)
          cout<<i<<"输入了"<<count[i]<<"次"<<endl;
        }
        return 0;
      }

> 方法2:switch语句

> 3.更简单的方法:

      #include <iostream>
      using namespace std;
      int main()
      {
        int num,count[10]={0};
        for(int i=0;i<20;i++)
        {
          cin>>num;
          count[num]++;
        }
        for(int i=0;i<10;i++)
        {
          if(count[i]!=0)
          cout<<i<<"输入了"<<count[i]<<"次"<<endl;
        }
        return 0;
      }

 > 例2:老师统计:

        #include<iostream>
        #include<iomanip>
        using namespace std;
        int main()
        {
          int teacher[21][13];
          int school,department;
          int i,j;
          char name[30];
          for(i=0;i<1000;i++)
          {
            cin>>name>>school>>department;
            teacher[school][department]++;
          }
          for(i=1;i<21;i++)
          for(j=1;j<13;j++)
          cout<<setw(4)<<teacher[i][j];
          cout<<endl;
          return 0;
        }

> 例3:找出素数:

      #include <iostream>
      using namespace std;
      int main()
      {
        bool prime=true;
        for(int i=0;i<100;i++)
        {
          prime=true;
          for(int j=2;j<i;j++)
          {
            if(i%j==0)
            prime=false;
          }
          if(prime==true)
          cout<<i<<endl;
        }
        return 0;
      }

> 2.

      #include<iostream>
      using namespace std;
      int main()
      {
        int sum=0;a[100]={0};
        for(int i=2;i<100;i++)//i<sqrt(100.0)
        {
          sum=i;
          while(sum<100)
          {
            sum=sum+i;
            if(sum<100)
            a[sum]=1;
          }
        }
        for(int i=2;i<100;i++)
        {
          if(a[i]==0)
          cout<<i<<" ";
        }
        return 0;
      }
