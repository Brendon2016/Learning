1. Boost安装
```
sudo apt-get install boost-all-dev
or 指定版本
sudo apt-get install boost1.68-all-dev	
```
2. Boost库分lib库和[Header Only Boost](https://stackoverflow.com/questions/13604090/which-boost-libraries-are-header-only)
- 添加lib库时，要用
```
find_package(Boost REQUIRED COMPONENTS
  thread
)
include_directories(
	${Boost_INCLUDE_DIRS}
)
target_link_libraries(mytarget
  ${Boost_LIBRARIES}
)
```

- 添加Header only Boost时，只需要
```
find_package(Boost)
include_directories(${Boost_INCLUDE_DIRS})
```
3. property_tree 解析XML文件

教程：[Five Minute Tutorial](https://www.boost.org/doc/libs/1_69_0/doc/html/property_tree/tutorial.html)

