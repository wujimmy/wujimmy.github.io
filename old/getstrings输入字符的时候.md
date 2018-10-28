内部测试版,3.0基础上的优化版
[file=uploads/200706/09_234755_checkbeamv3.0r.rar]梁配筋校对程序内测版[/file]有的时候,想修改一个字符串,可以又不想全部输入.
这时候如果想不用对话框的话,就可以试试以下的办法.
用SENDKEYS这个函数,可以事先输入一些字符串.
当时,如果是中文的话,可能还有点问题. 

[quote]
(defun c:tt()
 (SENDKEYS "aabb")
  (GETSTRING "\ntest:")
  )
[/quote]

[quote]
如果是中文的话,可以先放入剪贴板,然后用
(SENDKEYS "^v") 就可以显示在命令行了

放入剪贴板的方法,晓东CAD里面有
[/quote]

[quote]
;|
功能  
在程序运行过程中按下功能建  
语法  
(SendKeys keys )  
参数  
keys：键名  
样例  
，(sendkeys "{F3}") 相当于按下F3键
(sendkeys "{CAPSLOCK}") 相当于按下大小写键
