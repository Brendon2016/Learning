Matlab System
# Introduction
用于使用matlab语言创建simulink模型，优点如下：  
* 在 MATLAB 和 Simulink 中共享同一个 System object
* 实现 System object 与 Simulink 的集成
* 在 Simulink 中使用您的算法之前，先在 MATLAB 中对算法进行单元测试
* 自定义对话框的自定义设置
* 通过更好的初始化进行高效仿真
* 处理状态
* 使用端口标签自定义模块图标
* 访问两种仿真模式
MATLAB System基于System object, 因此需先学习这种特殊的matlab类。System object 专为实现和仿真输入随时间变化的动态系统而设计。
# System object
```
dft = dsp.FFT();		%创建对象实例；
dft(x)；				   %运行，输入参数为x
step(dft , x);			%等同于dft(x)
```
## 常用函数
```
step					%运行system object算法
clone					%创建重复的System object
isLocked				%确定实例是否正再使用；
reset
release
```
## 定义基本的system object类
### 创建
在 MATLAB 的“编辑器”选项卡中，选择新建 > System object > 基本。此时将打开一个简单的 System object 模板。
### 定义属性
可定义不可调属性和可调属性，这两种又有数值、字符串、逻辑类型，和C++类基本一致。
### 初始化
system object有构造函数，也有一个初始化函数setupimpl，一个用name:value作为参数传递给构造函数，然后再setupimpl中做初始化工作，setupimpl只在第一次调用stepimpl时调用。
### 定义算法：
实现stepImp1函数，其第一个参数默认为system object句柄（obj）,也可使用~指示函数不使用对象句柄，及不需要传入句柄
### 辅助函数
* infoimpl : 可用与返回system object 的一些信息，如状态、属性，可自定义需要返回的数据。
* resetimpl : 复位函数；