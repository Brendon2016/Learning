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
Matlab System是simulink中的一个模块，它通过加载一个system object来实现模块的功能。system object即可在simulink中使用，也可在.m文件等脚本中使用，是专为实现和仿真输入随时间变化的动态系统而设计的。当system object别用来加载到Matlab system中时，可以新增一些方法，如改变Matlab system外观、设置采样周期。
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
## 定义适用于Matlab system的system object类
适用于Matlab system的system object类是基于基本的system object，新增如下方法：
### 模块外观
```
getIconImpl	            //Name to display as block icon
getHeaderImpl	          //Header for System object display
getInputNamesImpl	      //Names of MATLAB System block input ports
getOutputNamesImpl	    //Names of MATLAB System block output ports
getPropertyGroupsImpl	  //Property groups for System object display
getSimulateUsingImpl	  //Specify value for Simulate using parameter
showSimulateUsingImpl	  //Visibility of Simulate using parameter
showFiSettingsImpl	    //Fixed point data type tab visibility for System objects
```
### 采样时间
```
createSampleTime	      //Create sample time specification object
getSampleTimeImpl	      //Specify sample time type, offset time, and sample time
getSampleTime	          //Query sample time
getCurrentTime	        //Current simulation time in MATLAB System block
setNumTicksUntilNextHit //Set the number of ticks in Simulink sample time
```
[specify sample time](https://ww2.mathworks.cn/help/simulink/ug/specify-sample-time-for-matlab-system-block-system-objects.html)
## matlab与simulink数据交互
### simulink读取matlab数据
1. simulink可以直接读取workspace中的数据；
2. 当需要每个运行周期读取workspace矩阵中一个行向量时，可以用From workspace模块，值得注意的是，当数据维数大于1时，需要将矩阵改成特定[structure](https://www.mathworks.com/help/simulink/ug/load-data-using-the-from-workspace-block-.html)
### 保存simulink数据到workspace
1. 添加To Workspace模块；
2. 添加out模块；
3. 直接用Scope输出。
## 在matlab中启动并运行simulink模型
1. 打开模型
```
open_system('模型名')      %不打开模型也可以运行，示波器等也会自动弹出
```
2. [运行模型](https://ww2.mathworks.cn/help/simulink/slref/sim.html?searchHighlight=sim&s_tid=doc_srchtitle)
```
[ t, x, y ] = sim( model, timespan, options, ut)
```
