# 复制构造函数
* 1.基本概念：

        （1）只有一个参数，即对同类对象的引用。
        （2）形如 X::X( X& )或X::X(const X &),二者选一后者能以常量对象作为参数
        （3）如果没有定义复制构造函数，那么编译器生成默认复制构造函数。默认的复制构造函数完成复制功能。

* 2.例子：

         class Complex
         {
           private:
                   double real,imag;
         };
         Complex c1;//强调缺省无参构造函数
         Complex c2(c1);//调用缺省的复制构造函数，将c2初始化成和c1一样

* 3.如果定义的自己的复制构造函数，则默认的复制构造函数不存在

        class Complex
        {
          public:
                  double real,imag;
          Complex(){}
          Complex(const Complex & c)
          {
            real=c.real;
            imag=c.imag;
            cout<<"Copy Constructor called";
          }
        };
        Complex c1;
        Complex c2(c1);//调用自己定义的复制构造函数，输出Cop Constructor called

# 复制构造函数起作用的三种情况

     （1）当用一个对象去初始化同类的另一个对象时。

            Complex c2(c1);
            Complex c2=c1;//初始化语句，非赋值语句

     （2）如果某函数有一个参数是类A的对象，那么该函数被调用时，类A的复制构造函数将被调用。

           class A
           {
             public:
             A(){};
               A(A&a)
               {
                 cout<<"Copy Constructor called"<<endl;
               }
           };
           void Func(A a1){}
           int main()
           {
               A a2;
               Func(a2);
               return 0;
           }
          输出结果：Copy Constructor called

      (3) 如果函数的返回值是类A的对象时，则函数返回时，A的复制构造函数被调用：

            A Func()
            {
              A b(4);
              return b;
            }
            int main()
            {
              cout<<Func().v<<endl;return 0;
            }
            class A
            {
              public:
              int v;
              A(int n){v=n;};
              A(const A&a)
              {
                v=a.v;
                cout<<"Copy Constructor called"<<endl;
              }
            };
          输出结果：
          Copy Constructor called
          4

# 类型转换构造函数

* 1.目的：实现类型的自动转换

* 2.特点：

       （1）只有一个参数
       （2）不是复制构造函数

* 3.编译系统会自动调用->转换构造函数->建立一个临时对象/临时变量

        class Complex//一个复数类
        {
          public:
              double real,imag;//定义实部虚部两个成员变量
              Complex(int i)
              {//类型转换构造函数
                cout<<"IntConstructor called"<<endl;
              }
              Complex(double r,double i)//定义了一个传统的构造函数
              {
                real=r;imag=i;
              }
        };
        int main()
        {
          Complex c1(7,8);
          Complex c2=12;//对c2进行初始化
          c1=9;//9被自动转换成一个临时Complex对象
          cout<<c1.real<<","<<c1.imag<<endl;
          return 0;
        }

        输出：IntConstructor called
             IntConstructor called
             9,0

# 析构函数：
* 1.回顾构造函数：

      （1）他是一种特殊的成员函数
      （2）名字与类名相同
      （3）可以有参数，不能有返回值
      （4）可以有多个构造函数
        ->  用来初始化对象

* 2.析构函数：

        （1）也是成员函数的一种
        （2）名字与类名相同
        （3）在前面加‘～’
        （4）没有参数和返回值
        （5）一个类最多只有一个析构函数
        -> 在对象消亡时会自动的被调用到，在对象消亡前做善后工作，释放分配的空间等

* 3.例子：

        class String
        {
          private:
              char * p;
          public:
              string ()
              {
                p=new char[10];
              }
              ~String();
        };
        String ::~String()
        {
          delete [] p;
        }
# 析构函数和数组
* 对象数组生命周期结束时，对象数组的每个元素的析构函数都会被调用

例子：

       class Ctest
       {
         public:
             ~Ctest()
             {
               cout<<"destructor called"<<endl;
             }
       };
       int main()
       {
         Ctest array[2];
         cout<<"End Main"<<endl;
         return 0;
       }

     输出：
         End Main
         destructor called
         destructor called

* delete 运算导致析构函数调用

       Ctest * pTest;
       pTest=new Ctest;//构造函数调用
       delete pTest;//析构函数调用
       pTest=new Ctest[3];//构造函数调用3次
       delete [] pTest;//析构函数调用3次

# 构造函数和析构函数调用时机的例题

     class Demo
     {
       int id;
       public:
            Demo(int i)
            {
              id=i;
              cout<<"id="<<id<<"Constructed"<<endl;
            }
            ~Demo()
            {
              cout<<"id="<<id<<"Destruced"<<endl;
            }
     };
     Demo d1(1);
     void Func()
     {
       static Demo d2(2);
       Demo d3(3);
       cout<<"Func"<<endl;
     }
     int main()
     {
       Demo d4(4);
       d4=6;
       cout<<"main"<<endl;
       { Demo d5(5);}
       Func();
       cout<<"main ends"<<endl;
       return 0;
     }

     输出：
         id=1 Constructed
         id=4 Constructed
         id=6 Constructed
         id=6 Destruced
         main
         id=5 Constructed
         id=5 Destruced
         id=2 Constructed
         id=3 Constructed
         Func
         id=3 Destruced
         main ends
         id=6 Destruced
         id=2 Destruced
         id=1 Destruced
