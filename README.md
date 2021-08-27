# less
用于 less 的学习

less中的注释
以//开头的注释，不会被编译到css文件中去
以/**/包裹的注释会被编译到css文件中去

less中的变量
使用@来申明一个变量： @pink : pink;
作为一个普通属性值来使用：直接使用@pink
作为选择器和属性名： #@{selector的值}的形式
作为URL：@{url}
变量的延迟加载（会等一个代码框的内容加载完成）



less的嵌套规则
基本嵌套规则
$的使用 （$代表外面一层,嵌套的时候平级）

less中的混合
混合就是将一系列属性从一个规则集引入到另一个规则集的方式
普通混合
//重复的less代码块可以提取出来变为一个变量
.vable{
  margin: 10px;
}

.inner {
  .vable;
}

.inner2 {
  vable;
}

不带输出的混合
//在变量less代码块的选择器后加个括号，less将不会被编译
.vable(){
  margin: 10px;
}

.inner {
  .vable;
}

.inner2 {
  vable;
}

带参数的混合
//为混合添加参数
.vable(@margin-left-base){
  margin: 10px;
  margin-left: @margin-left-base;
}

.inner {
  .vable(10px);
}

.inner2 {
  vable(10px);
}

带参数且有默认值的混合
//为混合添加参数并拥有默认值
.vable(@margin-left-base:10px){
  margin: 10px;
  margin-left: @margin-left-base;
}

.inner {
  .vable(10px);
}

.inner2 {
  vable();
}

带多个参数的混合
//为混合添加参数并拥有默认值
.vable(@margin-left-base:10px,@margin-right-base:10px){
  margin: 10px;
  margin-left: @margin-left-base;
  margin-right: @marign-right-base;
}

.inner {
  .vable(10px,10px);
}

.inner2 {
  vable();
}

命名参数
//为指定属性值提供参数
.vable(@margin-left-base:10px,@margin-right-base:10px){
  margin: 10px;
  margin-left: @margin-left-base;
  margin-right: @marign-right-base;
}

.inner {
  .vable(10px,10px);
}
.inner2 {
  vable(@margin-right-base: 10px);
}

匹配模式
 //引入vable文件，每次使用.vable是会自动引入@_的.vable
 .vable(@_,@margin-left-base,@margin-right-base){
  margin: 10px;
 }
 
.vable(@margin-left-base:10px,@margin-right-base:10px){
  margin-left: @margin-left-base;
  margin-right: @marign-right-base;
}

@import './vable.less'
.inner {
  .vable(10px,10px);
}

.inner2 {
  vable(@margin-right-base: 10px);
}

arguments变量(实参列表)
//伪参数，可带代替多个参数
.vable(@width,@color,@border){
 border: @arguments;
}

.inner {
  .vable(10px,black,solid);
}





less的运算
//less的计算当中只需要一方带单位
.inner {
  .vable(100 + 100px);
}
less的继承
 //引入vable文件，使用extend继承vable 注意权重问题
 .vable(){
  margin: 10px;
 }


@import './vable.less'
.inner:extend(.vable) {
 .inner2 {
  border: 1px solid black;
 } 
  .inne32 {
  border: 1px solid black;
 } 
}

//两个是一样的
.inner {
  &:extend(.vable)
}

//继承vable相关的所有语法 :hover之类的
.inner {
  &:extend(.vable all)
}


less避免编译
//加~和""避免编译
*{
  padding:~"cacl(100px + 100)";
}
