# 什么是指针
* 1 变量的三要素：
    >变量的地址
    >变量的值
    >变量的名字
    
 * *通常把某个变量的地址称为“指向该变量的指针”* 
 
     **指针不是指针变量**
* 2 能不能拿到，看到一个变量的地址呢？

    >可以利用  取地址运算符 “&”实现
    
    > cout<<&c<<endl;
       可以打印出变量c在内存中的起始地址。
    > cout<<sizeof(&c)<<endl;
       可以看到一个变量的地址也就是指向这个变量的指针占几个字节的内存。
       
 * 3 变量地址（指针）的作用
        >我们可以通过资源地址（指针）访问网络资源
        
         计算机通过变量的地址（指针）操作变量
        
 * 4 通过变量的地址（指针）操作变量
      >可以利用指针运算符* 实现
      
      *&c 去访问变量c
      
      > cout<<*&c<<endl;
      
      和cout<<c<<endl;的意义是等价的。

# 什么是指针变量
 * 1 存放地址（指针）的变量
     >我们可以设置一个变量，来存放变量的地址（变量的指针）
     
 * 2 指针变量
     >专门用于存放指针（某个变量的地址）的变量
     
     >当一个指针变量的值是另外一个变量的地址是，那这个指针变量就被称为指向c（另外一个变量）的指针变量。
     
 * 3 定义一个指针变量
     >int *pointer;       （pointer是指针变量的名字;*代表变量的类型;int 用来指明指针变量的基类型;基类型：指针变量指向的变量的类型）
     
 * 4 指针变量的定义
     > int c=76;
     
       int*pointer;//定义名字为pointer的指针变量;
       
       pointer=&c;//将变量c的地址赋值给指针变量pointer;
       
                  //赋值后，称指针变量pointer指向了变量c
       ！！pointer 是存放地址的变量，所以只能存放地址。
       
 * 5 指针变量的使用
     > 若有 
     
        int c=76;
        int *pointer=&c;
        
    >   *pointer:
     
        为“pointer所指向的存储单元的内容”;
        “pointer所指向的存储单元的内容”是变量c;
        
 * 6 指针变量的地址
    >指针变量也是变量，是变量就有地址
    
        #include <iostream>
        using namespace std;
        int main()
        {
           int iCount=18;
           int *iPtr=&iCount;
           *iPtr=58;
           cout<<iCount<<endl;
           cout<<iPtr<<endl;
           cout<<&iCount<<endl;
           cout<<*iPtr<<endl;
           cout<<&iPtr<<endl;
           return 0;
        }
        
        输出：58:说明我们用*pointer这种方式可以对pointer指向的那个变量也就是iCount进行赋值。也就是我们可以利用*pointer的这种形式去操作原来的        iCount这个变量。
             0028FB10: ipointer中存放的是一个地址，他的地址就是iCount变量的地址。
             0028FB10:iCount变量的地址。
             58：
             &ipointer：ipointer这个指针变量的地址。
             
 # 指针变量示例
  
  * 1  >指针变量示例
 
 
       #include <iostream>
       
       using namespace std;
       
       int main()
       
       {
       
           int a=0,b=0,temp;
           
           int *p1=NULL,*p2=NULL;//对刚定义的指针变量进行了赋初值，NULL表示一个空指针。
           
           cin>>a>>b;
           
           p1=&a;
           
           p2=&b;
           
           if(*p1<*p2)
           
           {
           
              temp=*p1;*p1=*p2;*p2=temp;
              
           }
           
           cout<<"max="<<*p1<<",min="<<*p2<<endl;
           
           return 0;
           
       }
       
  * 2 &与*的运算优先级
  
          后置++  --
  
          前置++  --     逻辑非(!)   *   &
  
          算数运算符
  
          关系运算符
  
          “&&”和“||”
  
           赋值运算符
  
           同级从右到左。
  
  * 3 pointer++的含义
  
     int a=0;
     
     int *p2=NULL;
     
     p2=&a;
     
     p2++;
     
     pointer变量的基类型为整型，所以p2++时系统理解的是跨过一整个区域。
     体现了基类型的作用。
     
     > 程序示例：
     
     #include <iostream>
    
     using namespace std;
     
     int main()
     
     {
     
        int n=0;
        int *p=&n;
        cout<<p<<endl;
        p++;
        cout<<p<<endl;
        return 0;
     }
     
     输出:  
     
           00C6FED8
           
           00C6FEDC 
           
           跨过4个字节，int型变量32位，4个字节。
           
  * 4 iptr++的含义：
     > 假设iptr当前所存地址是0x00000100
     
       若iptr指向一个整型元素（占四个字节），则iptr++等于iptr+1*4=0x00000104
       
       若iptr指向一个实型元素（占四个字节），则iptr++等于iptr+1*4=0x00000104
       
       若iptr指向一个字符元素（占一个字节），则iptr++等于iptr+1*1=0x00000101
       
   # 数组与指针
   
   * 1 指向数组元素的指针
   
      > 程序示例：
      
         #include <iostream>
         using namespace std;
         int main()
         {
              int a[5]={1,2,3,4,5};
              int *p=&a[3];
              cout<<*p<<endl;
              *p=100;
              cout<<a[3]<<endl;
              return 0;
         }
         
        指向数组元素和指向一个普通变量没有区别。
        
        
    > 程序示例：
    
         #include <iostream>
         using namespace std;
         int main()
         {
              int a[5]={10,11,12,13,14};
              cout<<a<<endl;
              cout<<*a<<endl;
              cout<<&a[0]<<endl;
              cout<<a[0]<<endl;
              return 0;
         }
         
         输出：0017F754
              10
              0017F754
              10//当我们打印数组中第一个元素的地址时和我们使用数组名直接打出来的地址是一样的
              
   
   * 2 数组的地址（数组的指针）
   
      > 数字名代表数组首元素的地址：数组名相当于指向数组第一个元素的指针。
      
      > 注意：数组名a不是变量，是数组在内存中存储的地址。
      
  
  # 用指针访问数组
  
  * 1 指针与数组
     > 示例
     
          #include <iostream>
          using namespace std;
          int main()
          {
              int a[5]={10,11,12,13,14};
              int *p=NULL;
              cout<<a<<endl;
              p=a;
              cout<<p<<endl;
              cout<<*p<<endl;
              cout<<*p++<<endl;//++的含义是先使用前面的变量然后再进行++
              cout<<*p++<<endl;
              return 0;
          }
          
