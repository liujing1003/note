# const关键字的用法
* 1.定义常量

       const int MAX_VAL=23;
       const double Pi=3.14;
       const char * ScHOOL_NAME="Peking Univwesity";

* 2.定义常量指针：

（1）不可通过常量指针修改其指向的内容,不可通过指针去修改而不是它指向的内容不可修改。

       int n,m;
       const int * p=& n;
       * p=5;//试图通过p去修改它指向的内容，是不允许的；
       n=4;//n的值可以被修改；
       p=& m;//常量指针的指向可以变化；

（2）不能把常量指针赋值给非常量指针，反过来可以

      const int * p1;int * p2;
      p1=p2;//可以把一个非常量指针赋值给一个常量指针
      p2=p1;//不可以把一个常量指针赋值给一个非常量指针
      p2=(int * )p1;//强制把p1变成一个int型的指针，然后再赋值给p2

（3）函数参数为常量指针时，可避免函数内部不小心改变参数指针所指地方的内容

      void MyPrintf(const char * p)
      {
        strcpy(p,"this");//编译出错，strcpy会修改p指向的内容
        printf("%s",p)
      }

* 3.定义常引用

  （1）不能通过常引用修改其引用的变量
