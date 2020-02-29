### SCSS

1. 简介  css不是真正意义上的编程语言 不具有编程语言的变量 循环 遍历和集成等特性 为了解决CSS的这些缺点 能够对css进行预处理的中间语言就产生了 并以此来实现某些编程特性 也就是在编写中间语言过程中 可以使用编程方式和思维 中间语言不能直接被浏览器解析 最后这些中间语言编译成真正的css 这样就能功能浏览器解析 就好像typescript和JavaScript的关系一样

2. SASS是最早的css预处理语言之一 为了适应编程风格的需求 sass在风格上做了一些修改 称之为现在的SCSS，SCSS增加了一些新的功能 增强了对css3的支持，语法完全兼容css3  并且集成了SASS的强大功能 任何css3语法都能再SCSS中使用  另外SCSS还能识别大部分css hack和特定于浏览器的语法 

   ```scss
   SCSS语法
   $nav-color:red;
   nav{
    $width:100px;
    width:$width;
    color:$nav-color
   }
   编译后
   nav{
     width:100px;
     color:red;
   }
   ```

3. SCSS和SASS的区别  SASS是最初定义的语法 一个主要的特征是对缩进敏感 不过很快 开发者觉得采用一种叫做SCSS的语法 弱化了SASS和CSS之间的语法区别 SCSS是对SASS的扩展 不用再关心SASS的语法

   ```SAS
   SASS 语法  没有花括号 缩进敏感 注意点多
    #sidebar
    	width:30%
    	background-color:#faa
   ```

   ```
   SCSS语法  只要加上大括号就把SASS语法变成了SCSS语法  SCSS对空格不敏感 书写起来比较接近css风格
    #sliderbar{
     width:30%
     background-color:#faa
    }
   ```

4. SCSS是基于ruby语言开发而成 因此安装SCSS前需要安装

   ------

   1. 安装ruby   ruby-v检测是否安装成功

   2. 安装SCSS  要使用gem 但是gem安装速度比较慢  所以要把gem的源切换成国内镜像然后再安装

      ```
      删除gem源      gem sources --remove https://rubygems.org/
      添加国内淘宝源  gem sources -a https://ruby.taobao.org/
      打印是否切换成功 gem sources -l 如果切换成功 会打印出淘宝镜像的网站https://ruby.taobao.org/
      ```

   3. 使用gem安装SCSS

      ```
      gem install sass  
      sass-v  检验是否安装成功
      gem update sass 更新SASS
      ```

      ------

5. 编译SCSS  

   ------

   

   - 把sass目录下的sass.scss文件编译成style.css并存放在css文件目录下

   ```scss
   sass  sass\sass.scss  css\stye.css
   ```

   - 单文件监听 也就是只要SCSS文件代码被修改 就立马编译到指定的文件

   ```scss
   sass -watch sass\sass.scss:css\style.scc
   ```

   - 整个目录监听

   ```scss
   sass -catch sass:css
   ```

   - css文件转换成SCSS文件

   ```scss
   sass -convert css\style.css sass\sass.scss
   sass -convert css\style.css sass\sass.sass
   
   
   ```

   - css转换成sass代码后的风格也是可以设置的

   ```scss
   sass --watch sass\sass.scss:css\style.css --style compact
   .nested: 风格
   @media print {
     .parent {
       color: red; }
       .child {
         width: 200px;
         height: 50px; } }
    .compact风格
    @media print{.parent{color:red}.child{width:200px;height:50px}}
   ```

6. 变量的声明 使用$可以声明一个变量 以前用！换成$的原因是$好看

   ------

   - 变量声明 和css属性的书面非常类似

     ```scss
     $highlight-color:#f90; 
     声明了一个变量 这个变量的值为#F90 任何在使用css属性值的地方都可以使用变量值 甚至是空格风格的多个属性值
     $basic-border:1px solid blacj;
     或者是以逗号分割的多个属性值
     $plain-font:sans-serif; sans-serif;
     ```

   - 变量的引用

     ```scss
     一个原则 标准css属性值存在的地方 变量就可以存在 当编译成css文件的时候 变量就会被变量值所代替 藏要修改一个css属性值时候 只要修改对应的变量值就可以 没有必要处处修改 这是SCSS的优点之一
     $highlight-color: #F90;
     .selected {
       border: 1px solid $highlight-color;
     }
     
     声明变量的时候概念使用其他变量做为当前变量的值
     $highlight-color: #F90;
     $highlight-border: 1px solid $highlight-color;
     .selected {
       border: $highlight-border;
     }
     
     ```

7. 变量分割符 SCSS变量名可以和css中的属性名和选择器名称相同 包括中划线和下划线  使用中划线还是下划线进行变量分割完全根据个人爱好 SCSS认为中划线和下划线是相等的

   ------

   ```scss
   scss代码
   $link-color:blue;
   a{
   	color:link_color;
   }
   编译后的css
   a{
   	color:blue
   }
   ```

8. SCSS变量的作用域 默认情况下 定义在选择器内的变量为全局变量  定义在选择器外的变量为全局变量

   ------

   - 全局作用域  

     ```scss
     $bg-color:green;   //定义在选择器外 全局变量 在整个文件中都是有效的
     div{
     	color:$bg-color;
     }
     ```

   - 局部作用域

     ```scss
     $bg-color:green;
     div{
     	 $border-width:5px;
       	 color:$bg-color;
      	 border:$border-width solid red;
     }
     p{
     	border:$border-width(报错 因为这个变量是上班div选择器内定义的) solid red 
     }
     ```

   - 选择器内定义的变量可以在子选择器内使用

     ```scss
     div{
     	$color:red;  //定义
     	p{
     		color:$color  //自选择器内使用
     	}
     }
     ```

   - 全局变量和局部变量可以同名 但是局部变量会覆盖全局变量的值

     ```scss
     $color:red
     div{
     	$color:green;
     	color:$color;   //最终的颜色为green
     }
     ```

9. SCSS 的！global !global可以改变一个局部变量的作用域范围

   ------

   ```
   @mixin button-style {
     $btn-bg-color: lightblue !global;  //本来在一个混合器内声明的局部变量 但是在最后加上！global就编程了全局变量 这样就可以在任何地方使用了
     color: $btn-bg-color;
   }
   button {
     @include button-style;
   }
   .wrap {
     background: $btn-bg-color;         //在这个地方可以使用
   }
   ```

10. ！default    如果在此之前变量已经复制 那么就不使用默认值 如果没有复制就使用默认值

    ------

    ```
    $content: "antzone" !default;
    #main {
      content: $content;    //此时content的值为antzone   如果之前定义过$content 那么就用之前的值
    }
    ```

11. scss的注释

    ------

    ```
    因为SCSS兼容原生的css 所以原生的css注释符号也在SCSS中可以使用 但是原生注释会在编译的时候把注释也保留在生成的css文件中 
    如果只想要注释在scss中起作用 那么使用scss的注释    //注释内容
    ```

### SCSS的基础规则

1. 嵌套规则(选择器嵌套)

   ------

   使用css的时候 经常会有代码重复书写的情况  非常繁琐  使用scss可以解决这个问题 那就是使用大括号作为层级分区 一层一层实现嵌套 在编译的时候再一层一层的剥离出来

   ```scss
   css的群组
   .container h1, .container h2, .container h3 { margin-bottom: .8em }  
   
   scss的嵌套优化
   .container {
   	h1,h2,h3{
   		margin-bottom: .8em 
   	}
   }
   ```

2. 嵌套属性

   ------

   使用scss不仅可以实现选择器的嵌套 属性也可以进行嵌套  规则 

   - 把属性名从中划线的地方断开
   - 在根属性（border）后边添加一个冒号  ( ：)紧跟一个块 把子属性(style width color)部分写在这个{}块中

   ```css
   css的属性  {}里面重复书写了border
   nav {
     border-style: solid;
     border-width: 1px;
     border-color: #ccc;
   }
   scss的优化
   nav{
      border:{
      style:solid;
      width:10x;
      color:red;
      }
   }
   
   ```

3. 父选择器标识符

   ------

4. @import

   ------

   在CSS中存在@import命令 它可以引入一个外部CSS文件  在SCSS中也存在一个@import命令 它的功能也和引入文件有关

   1. 命令基本用法 

      - 在原生css的@import中  有一个缺陷 会造成多的http请求 导致效率低下 因为是在解析执行css代码遇到次命令的时候 才会去下载此命名引入的文件 很明显这不够优化 所以在实际中并不推荐使用

      - scss中不用担心这个问题 他虽然和css中使用的方式比较类似  但是最终scss要编译成一个目标css文件 被引入的scss文件中的css代码会被合并到目标css中  所以不会产生一次额外的请求![aid[3022]](https://www.softwhy.com/data/attachment/portal/201902/28/234348ztth2mzwlddjhddz.png)

        ```
        左侧粉色标识一个main.scss文件 这个文件一次引入三个scss文件 也就是右侧的三个scss文件  假设最终生成main.css文件 这个main.css文件是代码中四个文件代码遵循某种规则合并的产物
        @import "colors.scss";
        @import "mixins.scss";
        @import "grids.scss";
        ```

   2. 删除无用的css文件  默认情况下 上述四个scss文件会生成四个对应的css文件  但是在实际应用中 很有可能最终的目标文件才是我们需要的 其他三个被导入的文件生成的css文件有点多余 scss已经对此问题给出了解决方案 

   3. 规则块内导入scss文件 scss的@import 命名更加灵活一些 它还可以在规则块内导入外部文件 此种导入方式下 生成对应的css文件时 局部文件会被直接插入到css规则内导入它的地方 假设我们有blue-theme.scss文件 代码如下

      ```
      aside {
        background: blue;
        color: white;
      }
      ```

      把文件导入到另一个scss文件制定的规则块中 代码如下

      ```
      .blue-theme {@import "blue-theme"}
      ```

      最终编译成css代码如下

      ```
      .blue-theme aside {
        background: blue;
        color: #fff;
      }
      ```

      被导入的文件编译成的css代码直接被插入到对应的位置

   4. partial部分文件 被导入的文件所生成的css文件也许是不必要的 那些专门为@import命令而编写的sass文件 并不需要对应的独立的css文件 这样的sass文件被称为局部文件 对此sass有一个页数的约定来命名这些文件  规定如下

      ```
      局部文件的文件名以下划线开头
      _night-sky.scss   
      这样以下划线开头的文件在编译的时候就不会产生对应的css文件 只会单纯的作为一个导入文件 这种部分文件的引用也可以省略掉扩展名
      ```

5. 原生css的导入   由于scss兼容css 所以在scss文件中也可以使用原生的方式@import  在下面几种情况下scss会以原生的方式使用@import

   1. 杯导入的文件名以.css结尾

   2. 被导入的文件名是一个url地址 例如:http://www.softwhy..com/css.css。

   3. 被导入的文件的名字是CSS url()值

      ```
      @import "grids.css";
      $padding: 50px;
      div {
       //antzone
        padding:$padding;
      }
      
      编译后
      @import url(grids.css);
      div{
        padding: 50px; 
      }
      如果我们不想以原生的方式导入css文件，也就不能够直接导入以css为扩展名的文件。
      
      又由于scss完全兼容css语法，所以我们可以直接将css扩展名修改为scss扩展名即可。
      
      ```

### SCSS的数据类型

1. 数字 1 2 13 10px  

   ```scss
   在scss中 数值加上单位也认为是数字类型
   ```

   

2. 字符串 有引号的字符串和无引号的字符串  ’foo‘  'bar'  ba

   ```scss
   在编译成css的时候不会改变其类型 s
   ```

   

3. 颜色  blue  #04a39f  rgba(255,234,231,0.4)

   ```scss
   十六进制符号、rgb、rgba、hsl、hsla和使用关键词
   ```

   

4. 布尔型 true false

   ```scss
   在scss中 只有自身是false和null才会返回false 其他一切都返回true
   
   $i-am-true: true; 
   $a-number: 2; 
   body { 
     @if not $i-am-true { 
       background: rgba(255, 0, 0, 0.6); 
     } @else { 
       background: rgba(0, 0, 255, 0.6); // expected 
     } 
   } 
   .warn { 
     @if not $a-number { 
       color: white; 
       font-weight: bold; 
       font-size: 1.5em; 
     } @else { 
       display: none; // expected 
     }
   }
   ```

   

5. 空值 null

6. 数组 list 用空格或者逗号作分隔符

   ```scss
   $list-space: "item-1" "item-2" "item-3";
   $list-space: "item-1","item-2","item-3";
   列表项与项之间可以用空格或者逗号分隔。
   列表的规则如下
   除非列表太长不能写在80字符宽度的单行中，否则应该始终单行显示。
   除非适用于CSS，否则应该始终使用逗号作为分隔符。   尽量用逗号分割
   除非为空或者嵌套在另一个列表中，否则始终不要使用括号 不要加括号 除非作为另一个列表的元素
   始终不要添加尾部的逗号。
   
   ```

   

7. maps  相当于JavaScript的对象直接量

   ```scss
   $map: ( 
     $key1: value1, 
     $key2: value2, 
     $key3: value3 
   )
   规则如下
   （1）.map名称前要有一个$。
   （2）.名称后面是一个冒号。
   （3）.冒号后面是小括号。
   （4）.小括号中的数据是以key:value键值对的形式存在的。
   （5）.键值对之间使用逗号分隔，最后一个后面无需逗号。
   
   map可以嵌套map
   $theme-color: ( 
     default: ( 
       bgcolor: #fff, 
       text-color: #444, 
       link-color: #39f
     ), primary:( 
       bgcolor: #000, 
       text-color:#fff, 
       link-color: #93f
     ), negative: ( 
       bgcolor: #f36, 
       text-color: #fefefe, 
       link-color: #d4e
     ) 
   )
   
   ```

### @mixin

1. 如果存在可大段重复使用的css代码 使用混合器可以方便的引用他  混合器使用@mixin命令标识

   ```scss
   @mixin rounded-corners {
     -moz-border-radius: 5px;
     -webkit-border-radius: 5px;
     border-radius: 5px;
   }
   上面是一个关于圆角功能的混合器 我们可以使用@include来引用这个混合器 
   notice {
     background-color: green;
     border: 2px solid #00aa00;
     @include rounded-corners;       //在这个地方引入了混合器的重复代码
   }
   
   编译后的代码如下
   notice{
        background-color: green;
    	 border: 2px solid #00aa00;
        -moz-border-radius: 5px;
     	 -webkit-border-radius: 5px;     //@include把混合器的代码插入在了这个指定的位置
     	 border-radius: 5px;
   }
   
   
   也可以在外部使用混合器
   @mixin silly-links {
     a {
       color: blue;
       background-color: red;
     }
   }
   @include silly-links;
   
   结果
   a {
       color: blue;
       background-color: red;
     }
   
   混合器也可以嵌套使用
   @mixin child-corners {
     border-radius: 5px;
   }
   @mixin rounded-corners {
     -moz-border-radius: 5px;
     -webkit-border-radius: 5px;
     @include child-corners;
   }
   notice {
     background-color: green;
     border: 2px solid #00aa00;
     @include rounded-corners;
   }
   
   结果
   @mixin child-corners {
     border-radius: 5px;
   }
   @mixin rounded-corners {
     -moz-border-radius: 5px;
     -webkit-border-radius: 5px;
     @include child-corners;
   }
   notice {
     background-color: green;
     border: 2px solid #00aa00;
      -moz-border-radius: 5px;
     -webkit-border-radius: 5px;
      border-radius: 5px;
   }
   ```

   

