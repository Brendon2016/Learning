* terminate called after throwing an instance of 'boost::exception_detail::clone_impl<boost::exception_detail::error_info_injector<boost::system::system_error> >'
  what():  open: No such file or directory
	solution : you may have used a wrong devive name or have no permit 


* CMakeFiles/process.dir/src/read_usb_data.cpp.o: In function `boost::system::system_category()':
read_usb_data.cpp:(.text._ZN5boost6system15system_categoryEv[_ZN5boost6system15system_categoryEv]+0x5): undefined reference to `boost::system::detail::system_category_ncx()'
CMakeFiles/process.dir/src/read_usb_data.cpp.o: In function `boost::system::generic_category()':
read_usb_data.cpp:(.text._ZN5boost6system16generic_categoryEv[_ZN5boost6system16generic_categoryEv]+0x5): undefined reference to `boost::system::detail::generic_category_ncx()'
collect2: error: ld returned 1 exit status
make[2]: *** [process] Error 1
make[1]: *** [CMakeFiles/process.dir/all] Error 2
make: *** [all] Error 2
	solution : add libboost_system.so to target link

* not found等错误，有可能是权限问题，比如.py 文件，设备文件
