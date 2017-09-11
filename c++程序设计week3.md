# 内联成员函数：
* 1.定义：

        （1）inline+成员函数
        （2）整个函数体出现在类定义内部
            class B{
              inline void func1();
              void func2()
              {

              };
            };
            void B::func1(){}

# 重载成员函数：

  成员函数可以进行重载，另一方面成员函数自身是可以带有缺省参数的。

      #include <iostream>
      using namespace std;
      class Location
      {
        private:
          int x,y;
        public:
          void init(int x=0,int y=0);
          void valueX(int val){x=val;}
          int valueX(){return x;}
      };
      void Location::init(int X,int Y)
      {
        x=X;
        y=Y;
      }
      int main()
      {
        Location A;
        A.init(5);//5被赋给了x，y就使用y的缺省值
        A.valueX(5);
        cout<<A.valueX();
        return 0;
      }

使用缺省参数要避免有函数重载时的二义性：

    class Location
    {
      private；
        int x,y;
      public:
        void init(int x=0,int y=0);
        void valueX(int val=0){x=val;}
        int valueX(){return x;}
    };
     Location A;
     A.valueX();//错误，编译器无法判断调用哪个valueX

# 构造函数：
* 概念:

      成员函数的一种：
      (1)名字与类名相同，可以有参数，不能有返回值（void也不行）。
      (2)作用是对对象进行初始化，如给成员变量赋初值。
      (3)如果定义类时没写构造函数，则编译器生成一个默认的无参数的构造函数。
      (4)对象生成时构造函数自动被调用，对象一旦生成，就再也不能在其上执行构造函数。
      (5)一个类可以有多个构造函数。

例子：

    (1) class Complex
        {//定义了一个Complex类
          private:
                  double real,imag;//定义了实部虚部
          public:
                  void Set(double r,double i);
        };//编译器自动生成默认构造函数
        Complex c1;//默认构造函数被调用
        Complex * pc=new Complex;//默认构造函数被调用



    (2）class Complex
        {
                  private:
                          double real,imag;
                  public:
                          Complex(double r,double i=0);
        };
        Complex::Complex(double r,double i)
        {
          real=r;imag=i;
        }

        这时：
        Complex c1;//error,缺少构造函数的参数
        Complex * pc=new Complex;//error,没有参数
        Complex c1(2);//OK

* 一个类可以有多个构造函数，只要参数个数或类型不同

# 构造函数在数组中的使用

例：

    class CSample
    {
            int x;
      public:
            CSample()
            {
              cout<<"Constructor 1 Called"<<endl;//没有参数的构造函数
            }
            CSample(int n)
            {
              x=n;
              cout<<"Constructor 2 Called"<<endl;//有参数的构造函数
            }
    };

例：

       class Test
       {
         public；
             Test(int n）{}//(1)
             Test(int n,int m){}//(2)
             Test(){}//(3)
       };
       Test array1[3]={1,Test(1,2)};//array1里面有三个对象，我们给出了前两个对象的初始化参数，所以array1分别用（1）（2）（3）初始化
       Test array2[3]={Test(2,3),Test(1,2),1};//三个元素分别用（2）（2）（1）初始化
       Test * pArray[3]={new Test(4),new Test(1,2)};//是指针数组，不是一个对象数组，指针可以不初始化，这里对指针进行了初始化，new出来了两个对象，new表达式的返回值是指针，用new出来的对象的地址来初始化这个数组里面的元素
