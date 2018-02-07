# Dart笔记
 
###   一个基本dart程序:
     
        printNumber(num aNumber){
         print('The number is $aNumber .')
        }

        // 和Java一样main方法入口 ;
        main(){
         var number = 44 ;
         printNumber(number);
        }
  上面用到的类型 :

   - //  - 注释 
   - num - 数字,一些其他的内置类型是String，int和bool ;
   - 44 - 数字文字,数字文字是一种编译时常量 ;
   - print() - 打印 ;
   - 'sss' or "sss" - 定义字符串 ;
   - $ variableName  or ${expression} - 字符串中引用代码块和变量,和kotlin类似 ;
   - var - 声明变量而不指定其类型的一种方法 ;
  
###  一些重要的概念 ;
   - 放在变量中的所有东西都是一个对象，每个对象都是一个类的实例。 偶数，函数和null都是对象。 所有对象都从Object类继承。
     
   - 指定静态类型（例如前面的例子中的num）将阐明您的意图，并启用工具进行静态检查。 （你可能注意到当你调试你的代码时，没有指定类型的变量会得到一个特殊的类型：dynamic。）在Dart 1.x中指定静态类型是可选的，但是Dart正在转向一种完全安全的语言。
     
   - 在强模式下，静态和运行时检查确保您的代码是类型安全的，帮助您捕获开发中的错误，而不是在运行时。 在Dart 1.x中强模式是可选的，但在Dart 2中不可选。

   - Dart在运行之前解析所有的代码。 您可以向Dart提供提示（例如，使用类型或编译时常量）来捕获错误或帮助您的代码更快地运行。

   - Dart支持顶层函数（如main（）），以及绑定到类或对象的函数（分别是static和instance方法）。 你也可以在函数内部创建函数（嵌套或局部函数）。
     
   - 同样，Dart支持顶层变量，以及绑定到类或对象（静态和实例变量）的变量。 实例变量有时被称为字段或属性。

   - 与Java不同，Dart没有关键字public，protected和private。 如果一个标识符以下划线（_）开头，则它是私有的。 

   - 标识符可以以字母或_开头，然后是这些字符和数字的任意组合。
 
   - Dart工具可以报告两种问题：警告和错误。 警告只是表明您的代码可能无法正常工作，但它们并不妨碍您的程序执行。 错误可以是编译时或运行时。 编译时错误会阻止代码执行; 运行时错误导致代码执行时引发异常。

   - Dart 1.x有两种运行模式：生产和检查。 我们建议您在检查模式下进行开发和调试，并部署到生产模式。 生产模式是Dart程序的默认运行模式，针对速度进行了优化。 生产模式会忽略断言和静态类型。 选中模式是一种开发人员友好模式，可帮助您在运行时捕获某些类型的错误。 例如，如果将一个非数字赋给一个声明为num的变量，那么checked模式会抛出一个异常。
     
### variables
         
        //变量是引用。 名为name的变量包含对值为的String对象的引用
        var name = 'Bob';
 
### 默认值 
  
   **未初始化的变量的初始值为null。 即使数字类型的变量最初为空，因为数字是对象。**

        int lineCount;
        assert(lineCount == null);
     
     注意：assert()调用在生产模式下被忽略。 在检查模式下，除非条件为true，否则assert（condition）将引发异常。 
     Dart2中将不包含检查模式 ;


### Final 和 const
   如果你不打算改变一个变量，可以使用final或const，而不是var或者除了一个类型。 最后一个变量只能设置一次; 一个const变量是一个编译时常量。 （Const变量隐含地是最终的。）最后的顶层或者类变量在第一次被使用时被初始化。
   
     final name = 'Bob'; //没有类型注释
     // name = 'Alice';  // 取消注释会导致错误
     final String nickname = 'Bobby';
   将const用于想要成为编译时常量的变量。 **如果const变量处于类级别，则将其标记为static const。** 在声明变量的地方，将该值设置为一个编译时常量，例如数字或字符串文字，常量变量或常数上算术运算的结果：
    
    const bar = 1000000; // Unit of pressure (dynes/cm2)
    const double atm = 1.01325 * bar; // Standard atmosphere

   const关键字不仅用于声明常量变量。 您也可以使用它来创建常量值，以及声明创建常量值的构造函数。 任何变量可以有一个常数值。
   
    // Note: [] creates an empty list.
    // const [] creates an empty, immutable list (EIL).
    var foo = const []; // foo is currently an EIL.
    final bar = const []; // bar will always be an EIL.
    const baz = const []; // baz is a compile-time constant EIL.

    // You can change the value of a non-final, non-const variable,
    // even if it used to have a const value.
    foo = [];

    // You can't change the value of a final or const variable.
    // bar = []; // Unhandled exception.
    // baz = []; // Unhandled exception.

### 构建类型
  - numbers
  - strings
  - booleans
  - lists (也被称为数组)
  - maps 
  - runes (用在字符串中表示Unicode字符)
  - symbols

### Numbers 数字
  - int : 整型值,范围为 -2^53 to 2^53 ;
  - double : 64位（双精度）浮点数，按照IEEE 754标准的规定 ;
  
   int和double都是num的子类型。 num类型包括基本运算符（如+， - ，/和*），还有其他方法可以找到abs（），ceil（）和floor（）。 （按位运算符，如>>，在int类中定义。）如果num和它的子类型没有你要找的东西，dart：math类库可能会这样。
  
   警告：**-2^53至2^53范围以外的整数在Dart代码生成的JavaScript中的行为与在Dart VM中运行相同的Dart代码时的行为不同。 原因是Dart被指定为具有任意精度的整数，但JavaScript不是**。 详情请参阅问题1533。

    int x = 1;
    int hex = 0xDEADBEEF;
    int bigInt = 34653465834652437659238476592374958739845729;
    double y = 1.1;
    double exponents = 1.42e5;

   类型之间的转换 ;

      // String -> int
      var one = int.parse('1');
      assert(one == 1);

       // String -> double
       var onePointOne = double.parse('1.1');
       assert(onePointOne == 1.1);

       // int -> String
       String oneAsString = 1.toString();
       assert(oneAsString == '1');

       // double -> String
       String piAsString = 3.14159.toStringAsFixed(2);
       assert(piAsString == '3.14');
   int类型指定传统的按位移（<<，>>），AND（＆）和OR（|）运算符。

     assert((3 << 1) == 6); // 0011 << 1 == 0110
     assert((3 >> 1) == 1); // 0011 >> 1 == 0001
     assert((3 | 4) == 7); // 0011 | 0100 == 0111

   文字数字是编译时常量。 许多算术表达式也是编译时常量，只要它们的操作数是编译时常量，并计算为数字。

     const msPerSecond = 1000;
     const secondsUntilRetry = 5;
     const msUntilRetry = secondsUntilRetry * msPerSecond;

