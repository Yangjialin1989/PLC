# SCL

[toc]

## 一	运算符与表达式

> Structured Control Language

> 数据管理,过程优化,配方管理,统计任务

### 1.算数表达式

> 数值,带有算数表达式组合
>
> INT +  DINT = DINT (隐式转换)
>
> USINT + UDINT = UDINT
>
> SINT + USINT = INT
>
> REAL + LREAL = LREAL
>
> 设置IEC检查,不能使用数据类型检查

"Scl1DB".幂运算.C := "Scl1DB".幂运算.A ** "Scl1DB".幂运算.B; 
//2.加运算
"Scl1DB".加运算.C := "Scl1DB".加运算.A + "Scl1DB".加运算.B;
//3.模运算
"Scl1DB".模运算.C := "Scl1DB".模运算.A  MOD  "Scl1DB".模运算.B;

### 2.关系表达式

> 两个操作数的值或数据类型进行比较,得到一个布尔值
>
> 只能比较相同类型的变量
>
> ==  <>  >= <= > < 
>
> 字符串  a > A  ,比较左边到右边,第一个
>
> 数组比较,元素类型必须相同,维度必须相同

### 3.逻辑表达式

> and or xor not 

> 两个操作数比较,由最高操作数类型决定
>
> 一个bool类型,另一个字节型,bool要先转字节型

> 位字符串:能转换为2进制的数据,不是浮点数,负数,只有数字
>
> byte       0000 0001       1
>
> word
>
> dword

> 

#### 1.取反(求反码)	NOT

#### 2.与	AND  (&)

#### 3.或	OR

#### 4.异或	XOR

0  1   1

0  0   0

1  0   1

1  1   0

### 4.赋值运算

> 变量 =  表达式
>
> 数据类型取决于左边变量的数据类型

#### 1.单赋值运算

#### 2.组合赋值运算

#### 3.特殊赋值

![image-20210926172405939](C:\Users\72985\AppData\Roaming\Typora\typora-user-images\image-20210926172405939.png)

![image-20210926172801624](C:\Users\72985\AppData\Roaming\Typora\typora-user-images\image-20210926172801624.png)



### 5.运算符优先级

#### 1.算数运算符 > 关系运算符 > 逻辑运算符

#### 2.同等优先级: 从左到右

#### 3.赋值运算:从右到左  (:=)

#### 4.括号中的运算优先级最高()

### 6.浮点数使用

> 7位前正常显示,8位后变化

![image-20210927071228449](C:\Users\72985\AppData\Roaming\Typora\typora-user-images\image-20210927071228449.png)

## 二    流程控制语句

### 1.使用区间和注释

```scss
REGION _name_
    // Statement section REGION
    
END_REGION
```

### 2.IF...Then

```scss
 REGION 2.IF...THEN
        //2.1 IF...THEN
        IF "Scl1DB".Btn THEN
            "Scl1DB".d := 1;
        END_IF;
        
        
        //2.2 IF...THEN   ELSE...  END IF
        IF "Scl1DB".Btn1 THEN
            "Scl1DB".e := 2;
            
        ELSE
            "Scl1DB".e := 3;
        END_IF;
        
        //2.3 IF...THEN  ELSEIF...THEN  ELSE...END_IF
        IF "Scl1DB".f = 3 THEN
            "Scl1DB".g := 20;
        ELSIF "Scl1DB".f = 4 THEN
            "Scl1DB".g := 21;
        ELSE
            "Scl1DB".g := 22;
        END_IF;
        
    END_REGION
```



### 3.CASE...OF...

```scss
    REGION 3.CASE...OF...
        // 创建多路分支,表达式的值必须是整数
        // 
        CASE "Scl1DB".case1 OF
            1:
                "Scl1DB".g := 100;
               
            2:
                "Scl1DB".g := 101;
            3..9:
                "Scl1DB".g := 200;
                
            ELSE
                "Scl1DB".g := 1000;
        END_CASE;
            
        
    END_REGION
```



### 4.FOR...TO...DO

> 循环指令,明确循环次数
>
> 把一组变量批量传送到另一组变量

```scala
    REGION 4.FOR 
        //1.没有长度
        //
        FOR #for1 := 0 TO 10 DO
            
            "Scl1DB".x[#for1] := "Scl1DB".y[#for1];
        END_FOR;

         //2.有BY跨越长度 
        //0   2   4   6  8 传送
        FOR #for1 := 0 TO 10 BY 2 DO
            
            "Scl1DB".x[#for1] := "Scl1DB".y[#for1];
        END_FOR;
        //3.嵌套使用
        //
        FOR #for2 := 0 TO 5 DO
            // Statement section FOR
            FOR #for3 := 0 TO 5 DO
                "Scl1DB".q1[#for2,#for3] :="Scl1DB".q2[#for2,#for3];
            END_FOR;

        END_FOR;
    END_REGION


```

### 5.WHILE...DO

> 满足条件执行,可重复执行,循环次数不知道的情况可以使用

```scala
REGION _name_
    // Statement section REGION
    IF "Scl1DB".按钮 THEN
        "Scl1DB".循环次数 := 0;
        WHILE "Scl1DB".循环次数 < 10 DO
            "Scl1DB".A["Scl1DB".循环次数] := "Scl1DB".B["Scl1DB".循环次数];
            "Scl1DB".循环次数 += 1;
        END_WHILE;
        "Scl1DB".按钮 := 0;//不会死循环
        
    END_IF;
    
END_REGION
```

### 6.CONTINUE  复查

> 可以结束当前循环程序,,

continue 复查上面的,下面的中断不会执行,上面的完整执行

当i> 5 ,执行continue,跳出if语句,返回for语句,下面的for2不会继续加,但是上面的for1会继续.

```scala
"Scl1DB".A[4] := 10;
IF "Scl1DB".for按钮 THEN
        FOR #i := 0 TO 10 DO
            "Scl1DB".for1 += 1;
            IF #i > 5 THEN
                CONTINUE;
            END_IF;
            "Scl1DB".for2 += 1;
        END_FOR;
        "Scl1DB".for按钮 := 0;
END_IF;
```





### 7.EXIT	立即退出循环

死循环:

```scala
// Statement section REGION
    "Scl1DB".循环 := 0;
    WHILE "Scl1DB".循环 < 10 DO
        // Statement section WHILE
        "Scl1DB".A[5] := 10;
    END_WHILE;
    "Scl1DB".A[4] := 10;
```

添加EXIT语句:

```scala
// Statement section REGION
    "Scl1DB".循环 := 0;
    WHILE "Scl1DB".循环 < 10 DO
        // Statement section WHILE
        "Scl1DB".A[5] := 10;
        EXIT;
    END_WHILE;
    "Scl1DB".A[4] := 10;
END_REGION
```

但是这时候cpu报故障

### 8.直接寻址,间接寻址

SCL特有:

> PEEK:读取存储器地址
>
> POKE:写入存储器地址

直接寻址:在指令格式的地址的字段中直接指出操作数在存储的地址,例如:I0.0,QB0

间接寻址:指令地址字段的形式地址D不是操作数的真正地址,而是操作数的指示器,是D单元的内容才是操作数的有效地址(间接的通过index访问)

![image-20210927205554404](C:\Users\72985\AppData\Roaming\Typora\typora-user-images\image-20210927205554404.png)



![image-20210927210450754](C:\Users\72985\AppData\Roaming\Typora\typora-user-images\image-20210927210450754.png)

|      |      |
| ---- | ---- |
|      |      |

![image-20210927211544439](C:\Users\72985\AppData\Roaming\Typora\typora-user-images\image-20210927211544439.png)

```scala
   REGION 间接寻址
        // 1.普通间接寻址
        "Scl1DB".间接寻址.f["Scl1DB".间接寻址.index] :="Scl1DB".间接寻址.A;
        // 2.
        // 
        "Scl1DB".scl.b := PEEK_WORD(area := 16#84,
                                    dbNumber := 2,
                                    byteOffset :="Scl1DB".scl.a);
    END_REGION
```

## 三	自定义实用块 

### 1.批量传送

#### 1.1	数组传送

```scala
//比较 
//
IF #源_结束地址 - #源_开始地址 = #目的_结束地址 - #目的_开始地址 THEN
    
    //传送长度
    #length := #源_结束地址 - #源_开始地址;
    
    FOR #i := 0 TO #length DO
        
        //读取存储数据
        #数据暂存 := PEEK(area := 16#84, dbNumber := #源_数据块, byteOffset := #i + #源_开始地址);
        
        //写入数据
        //
        POKE(area := 16#84,
             dbNumber := #目的_数据块,
             byteOffset := #i + #目的_开始地址,
             //写入DB1.DBB1中
             value := #数据暂存);
        
    END_FOR;

ELSE
    #error := 1;
    
END_IF;
```

![image-20210928095227379](C:\Users\72985\AppData\Roaming\Typora\typora-user-images\image-20210928095227379.png)

填写偏移量的时候,int数据,加1 ,写21

![image-20210928095315974](C:\Users\72985\AppData\Roaming\Typora\typora-user-images\image-20210928095315974.png)









#### 1.2	结构传送

偏移量填写完整,数据结构对应

![image-20210928095650735](C:\Users\72985\AppData\Roaming\Typora\typora-user-images\image-20210928095650735.png)

#### 1.3	传送一次

![image-20210928100259858](C:\Users\72985\AppData\Roaming\Typora\typora-user-images\image-20210928100259858.png)

### 2.数据填充

> 实现数组的填充,任何一个位删除,则下一个数据进行补充

需求:把填充数据填充到填充数组里面,依次下填

![image-20210928114306333](C:\Users\72985\AppData\Roaming\Typora\typora-user-images\image-20210928114306333.png)

```scala
IF #填充数据 <> 0 THEN  // 节省循环扫描的时间,且减少数组使用量
    FOR #index := 0 TO #数组长度 DO
        // Statement section FOR
        
        IF "数据填充_1".填充数组[#index] = 0 THEN
            "数据填充_1".填充数组[#index] := #填充数据;
            EXIT;
        END_IF;
        
    END_FOR;
    
    //填充数据清零
    #填充数据 := 0;
END_IF
```

### 3.数据排列

> 实现对根据数组长度X,中的内容进行排列
>
> 冒泡排序: 比较相邻的元素,如果第一个比第二个大,就交换他们

#### 1.冒泡排序

![image-20210928132141416](C:\Users\72985\AppData\Roaming\Typora\typora-user-images\image-20210928132141416.png)

> 正序排列:(for内不允许出现两个相同的index

```scala
FOR #index_1 := 0 TO 5 DO   //控制总的排序次数
    FOR #index := 0 TO 4 DO  // 控制一次排序的个数
        // Statement section FOR
        IF "数据排列_1".A[#index] > "数据排列_1".A[#index + 1] THEN
            // Statement section IF
            #tempArray := "数据排列_1".A[#index];
            "数据排列_1".A[#index] := "数据排列_1".A[#index + 1];
            "数据排列_1".A[#index + 1] := #tempArray;
        END_IF;
        
    END_FOR;
END_FOR;
```



### 4.数据转换

> 整数转浮点数

```SAS
//数据转换
//
FOR #i := #start TO #end DO
    // Statement section FOR
    "数据转换_2".B[#i] := INT_TO_REAL("数据转换_1".A[#i]);
END_FOR;
```

### 5.数码显示

```scala
// 0  16#6F 0110 1111
// 1  16#24 
// 2  16#5e
// 3  16#76
// 4  16#35
// 5  16#73
// 6  16#7b
// 7  16#26
// 8  16#7f
// 9  16#77
// .  bool
//1.整合,拆分
// 12345 
// 5  12345 %10  
// 4  12345/10 %4
// 3  12345/100 %3 
// 2  12345/1000 %2
// 1  12345/10000 %1
// 
#p1 := #input MOD 10;
#p21 := #input / 10;
#p2 := #p21 MOD 10;
#p31 := #input / 100;
#p3 := #p31 MOD 10;
#p41 := #input / 1000;
#p4 := #p41 MOD 10;
#p51 := #input / 10000;
#p5 := #p51 MOD 10;
//2.对应关系,确定数据
//
////3.赋值5分,分段显示
CASE #p1 OF
    0:
        "DB".p1 := 16#6F;
    1:
        "DB".p1 := 16#24;
    2:
        "DB".p1 := 16#5E;
    3:
        "DB".p1 := 16#76;
    4:
        "DB".p1 := 16#35;
    5:
        "DB".p1 := 16#73;
    6:
        "DB".p1 := 16#7B;
    7:
        "DB".p1 := 16#26;
    8:
        "DB".p1 := 16#7F;
    9:
        "DB".p1 := 16#77;
        
END_CASE;
CASE #p2 OF
    0:
        "DB".p2 := 16#6F;
    1:
        "DB".p2 := 16#24;
    2:
        "DB".p2 := 16#5E;
    3:
        "DB".p2 := 16#76;
    4:
        "DB".p2 := 16#35;
    5:
        "DB".p2 := 16#73;
    6:
        "DB".p2 := 16#7B;
    7:
        "DB".p2 := 16#26;
    8:
        "DB".p2 := 16#7F;
    9:
        "DB".p2 := 16#77;
        
END_CASE;
CASE #p3 OF
    0:
        "DB".p3 := 16#6F;
    1:
        "DB".p3 := 16#24;
    2:
        "DB".p3 := 16#5E;
    3:
        "DB".p3 := 16#76;
    4:
        "DB".p3 := 16#35;
    5:
        "DB".p3 := 16#73;
    6:
        "DB".p3 := 16#7B;
    7:
        "DB".p3 := 16#26;
    8:
        "DB".p3 := 16#7F;
    9:
        "DB".p3 := 16#77;
        
END_CASE;
CASE #p4 OF
    0:
        "DB".p4 := 16#6F;
    1:
        "DB".p4 := 16#24;
    2:
        "DB".p4 := 16#5E;
    3:
        "DB".p4 := 16#76;
    4:
        "DB".p4 := 16#35;
    5:
        "DB".p4 := 16#73;
    6:
        "DB".p4 := 16#7B;
    7:
        "DB".p4 := 16#26;
    8:
        "DB".p4 := 16#7F;
    9:
        "DB".p4 := 16#77;
        
END_CASE;
CASE #p5 OF
    0:
        "DB".p5 := 16#6F;
    1:
        "DB".p5 := 16#24;
    2:
        "DB".p5 := 16#5E;
    3:
        "DB".p5 := 16#76;
    4:
        "DB".p5 := 16#35;
    5:
        "DB".p5 := 16#73;
    6:
        "DB".p5 := 16#7B;
    7:
        "DB".p5 := 16#26;
    8:
        "DB".p5 := 16#7F;
    9:
        "DB".p5 := 16#77;
        
END_CASE;

//4.确定小数点位置
CASE #save OF
    1:
        "DB".p2_dot := 1;
        "DB".p3_dot := 0;
        "DB".p4_dot := 0;
        "DB".p5_dot := 0;
        
    2:
        "DB".p2_dot := 0;
        "DB".p3_dot := 1;
        "DB".p4_dot := 0;
        "DB".p5_dot := 0;
    3:
        "DB".p2_dot := 0;
        "DB".p3_dot := 0;
        "DB".p4_dot := 1;
        "DB".p5_dot := 0;
    4:
        "DB".p2_dot := 0;
        "DB".p3_dot := 0;
        "DB".p4_dot := 0;
        "DB".p5_dot := 1;
  
END_CASE;

```



### 6.区域查询与修改

> 仓储
>
> 货位1个,建立三维数组(4 5 5)
>
> 

#### 1.新建PLC数据类型   物料

![image-20210929072920936](C:\Users\72985\AppData\Roaming\Typora\typora-user-images\image-20210929072920936.png)

#### 2.新建数据库DB1,根据物料数据类型建立 4 5 5三维数组

![image-20210929073255432](C:\Users\72985\AppData\Roaming\Typora\typora-user-images\image-20210929073255432.png)

#### 3.新建物料管理FC,编程逻辑

```SAS
//1.根据物料编码查询
//123,124,等位置信息  拆分成 1,2,3 1,2,4 
//2.拆分物料编码为数组格式
//
IF "DB".货位号 > 455 OR "DB".货位号 < 111  THEN
    // Statement section IF
    // 
    "DB".货位号 := 111;
END_IF;

#货位编号Z := "DB".货位号 MOD 10;//3
#货位编号Y := ("DB".货位号/10) MOD 10;// 12%10 2
#货位编号X := "DB".货位号 / 100;//1
"DB".缺省信息.物料编号 := "DB".物料信息[#货位编号X, #货位编号Y, #货位编号Z].物料编号;
"DB".缺省信息.物料条码 := "DB".物料信息[#货位编号X, #货位编号Y, #货位编号Z].物料条码;
"DB".缺省信息.托盘ID := "DB".物料信息[#货位编号X, #货位编号Y, #货位编号Z].托盘ID;
"DB".缺省信息.件数 := "DB".物料信息[#货位编号X, #货位编号Y, #货位编号Z].件数;
"DB".缺省信息.补充信息 := "DB".物料信息[#货位编号X, #货位编号Y, #货位编号Z].补充信息;

//3.修改
//
IF "DB".修改货位号 > 455 OR "DB".修改货位号 < 111 THEN
    // Statement section IF
    // 
    "DB".修改货位号 := 111;
END_IF;

#货位编号Z := "DB".修改货位号 MOD 10;//3
#货位编号Y := ("DB".修改货位号 / 10) MOD 10;// 12%10 2
#货位编号X := "DB".修改货位号 / 100;//1
IF "DB".修改按钮 = 1 THEN
    "DB".物料信息[#货位编号X, #货位编号Y, #货位编号Z].物料编号 := "DB".修改源缺省.物料编号;
    "DB".物料信息[#货位编号X, #货位编号Y, #货位编号Z].物料条码 := "DB".修改源缺省.物料条码;
    "DB".物料信息[#货位编号X, #货位编号Y, #货位编号Z].托盘ID := "DB".修改源缺省.托盘ID;
    "DB".物料信息[#货位编号X, #货位编号Y, #货位编号Z].件数 := "DB".修改源缺省.件数;
    "DB".物料信息[#货位编号X, #货位编号Y, #货位编号Z].补充信息 := "DB".修改源缺省.补充信息;
    
END_IF;
```

#### 4.建立物料中文对应数据块

```SAS
//1.根据物料编码查询
//123,124,等位置信息  拆分成 1,2,3 1,2,4 
//2.拆分物料编码为数组格式
//
IF "DB".货位号 > 455 OR "DB".货位号 < 111  THEN
    // Statement section IF
    // 
    "DB".货位号 := 111;
END_IF;

#查询货位号Z :=#货位编号Z := "DB".货位号 MOD 10;//3
#查询货位号Y :=#货位编号Y := ("DB".货位号/10) MOD 10;// 12%10 2
#查询货位号X := #货位编号X := "DB".货位号 / 100;//1
"DB".缺省信息.物料编号 := "DB".物料信息[#货位编号X, #货位编号Y, #货位编号Z].物料编号;
"DB".缺省信息.物料条码 := "DB".物料信息[#货位编号X, #货位编号Y, #货位编号Z].物料条码;
"DB".缺省信息.托盘ID := "DB".物料信息[#货位编号X, #货位编号Y, #货位编号Z].托盘ID;
"DB".缺省信息.件数 := "DB".物料信息[#货位编号X, #货位编号Y, #货位编号Z].件数;
"DB".缺省信息.补充信息 := "DB".物料信息[#货位编号X, #货位编号Y, #货位编号Z].补充信息;



//移动
//
IF "DB".移动货位号 > 455 OR "DB".移动货位号 < 111 THEN
    // Statement section IF
    // 
    "DB".移动货位号 := 111;
END_IF;

#货位编号Z := "DB".移动货位号 MOD 10;//3
#货位编号Y := ("DB".移动货位号 / 10) MOD 10;// 12%10 2
#货位编号X := "DB".移动货位号 / 100;//1
IF "DB".移动按钮 = 1 THEN
    "DB".物料信息[#货位编号X, #货位编号Y, #货位编号Z].物料编号 := "DB".移动数据源.物料编号;
    "DB".物料信息[#货位编号X, #货位编号Y, #货位编号Z].物料条码 := "DB".移动数据源.物料条码;
    "DB".物料信息[#货位编号X, #货位编号Y, #货位编号Z].托盘ID := "DB".移动数据源.托盘ID;
    "DB".物料信息[#货位编号X, #货位编号Y, #货位编号Z].件数 := "DB".移动数据源.件数;
    "DB".物料信息[#货位编号X, #货位编号Y, #货位编号Z].补充信息 := "DB".移动数据源.补充信息;
    
END_IF;




//3.修改
//
IF "DB".修改货位号 > 455 OR "DB".修改货位号 < 111 THEN
    // Statement section IF
    // 
    "DB".修改货位号 := 111;
END_IF;

 #货位编号Z := "DB".修改货位号 MOD 10;//3
 #货位编号Y := ("DB".修改货位号 / 10) MOD 10;// 12%10 2
#货位编号X := "DB".修改货位号 / 100;//1
IF "DB".修改按钮 = 1 THEN
    "DB".物料信息[#货位编号X, #货位编号Y, #货位编号Z].物料编号 := "DB".修改源缺省.物料编号;
    "DB".物料信息[#货位编号X, #货位编号Y, #货位编号Z].物料条码 := "DB".修改源缺省.物料条码;
    "DB".物料信息[#货位编号X, #货位编号Y, #货位编号Z].托盘ID := "DB".修改源缺省.托盘ID;
    "DB".物料信息[#货位编号X, #货位编号Y, #货位编号Z].件数 := "DB".修改源缺省.件数;
    "DB".物料信息[#货位编号X, #货位编号Y, #货位编号Z].补充信息 := "DB".修改源缺省.补充信息;
    
END_IF;




//5.删除
//
IF "DB".删除货位号 > 455 OR "DB".删除货位号 < 111 THEN
    // Statement section IF
    // 
    "DB".删除货位号 := 111;
END_IF;

#货位编号Z := "DB".删除货位号 MOD 10;//3
#货位编号Y := ("DB".删除货位号 / 10) MOD 10;// 12%10 2
#货位编号X := "DB".删除货位号 / 100;//1
IF "DB".删除按钮 THEN
    "DB".物料信息[#货位编号X, #货位编号Y, #货位编号Z].物料编号 := 0;
    "DB".物料信息[#货位编号X, #货位编号Y, #货位编号Z].物料条码 := 0;
    "DB".物料信息[#货位编号X, #货位编号Y, #货位编号Z].托盘ID := 0;
    "DB".物料信息[#货位编号X, #货位编号Y, #货位编号Z].件数 := 0;
    "DB".物料信息[#货位编号X, #货位编号Y, #货位编号Z].补充信息 := 0;
    
END_IF;


//物料中文名称对应
//托盘重复报警
////每个托盘信息比较
FOR #A := 1 TO 4 DO
    FOR #B := 1 TO 5 DO
        FOR #C := 1 TO 5 DO
            
            
            //得到所有的托盘信息
            FOR #D := 1 TO 4 DO
                FOR #E := 1 TO 5 DO
                    FOR #F := 1 TO 5 DO
                        
                        //不允许自己作比较
                        IF #A * 100 + #B * 10 + #C <> #D * 100 + #E * 10 + #F THEN
                            IF "DB".物料信息[#A, #B, #C].托盘ID<>0 AND  "DB".物料信息[#D, #E, #F].托盘ID<>0 THEN
                                IF "DB".物料信息[#A, #B, #C].托盘ID = "DB".物料信息[#D, #E, #F].托盘ID THEN
                                    "DB".ID重复报警 := 1;
                                END_IF;
                            END_IF;
                        END_IF;
                    END_FOR;
                END_FOR;
            END_FOR;
            
            
        END_FOR;
    END_FOR;
END_FOR;


```

### 7.学生成绩管理系统

> 姓名:string,  不重复
>
> 学号:int  ,      不重复
>
> 专业:int
>
> 班级:int 
>
> 分数:real       (保留小数点一位)
>
> 

#### 1.	建立工程制作界面图表

##### 1.创建数据类型info,包含基本信息

![image-20210930091501318](C:\Users\72985\AppData\Roaming\Typora\typora-user-images\image-20210930091501318.png)

##### 2.创建数据块,生成多个info

![image-20210930091550982](C:\Users\72985\AppData\Roaming\Typora\typora-user-images\image-20210930091550982.png)

##### 3.创建指针,每页显示20条数据





#### 2.	制作修改界面连接



#### 3.	制作查询界面的连接

##### 1.制作HMI 下拉菜单

> 文件和图像列表

![image-20211001082028578](C:\Users\72985\AppData\Roaming\Typora\typora-user-images\image-20211001082028578.png)

