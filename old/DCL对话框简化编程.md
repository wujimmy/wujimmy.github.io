在程序中对于对话框是很麻烦的事情.
如果全部用LISP来写对话框就方便了.
以下就是个例子.

每一行就是一个控件
(list 变量名 提示语 变量类型)
例1:
 (list "is_wpj" "wpj*.dwg" "bool")
例2:
(list "other-scale" "放大倍数" "int")

当变量名为nil 时表示一个对话框控制字符(这个要了解相关语法 )
例1: 注,下面的要成对出现,而且然后把其他的东西(编辑框等)放在里面
 (list nil "" ": boxed_row{");;横向排列各控件
 (list "is_wpj" "wpj*.dwg" "bool").......
 (list nil nil "}")

例2:
 (list nil "" ": boxed_column{");;竖向排列各控件
 (list "is_wpj" "wpj*.dwg" "bool").......
 (list nil nil "}")
`
  [FONT=courier new]
例子1:

(setq initlist
       (list
	 (list nil "" ": boxed_row{")
	 (list "filedir" "工程路径" "str")
	 (list nil ">" "button" "(select-dir)")
	 (list nil nil "}")
	 (list "is_for_plt" "生成用于配筋计算书(否则为打印用计算书)" "bool")
	 
	 (list nil "" ": boxed_column{")
	 ;(list nil "" ": boxed_row{")
	 (list "is_wpj" "wpj*.dwg" "bool")
	 (list "block_pre_name" "块名加前缀" "str")
	 (list "is_on_one_point" "是否插入同一点" "bool")
	 ;(list nil nil "}")
	 (list "floor-str" "层号范围(空格分开,全部留空)" "str")
	  (list nil nil "}")
	 (list "is_bpj" "*板计算结果*.dwg" "bool")
	 (list "is_flr" "FLR*.dwg" "bool")
	 (list "is_load" "第??层梁、墙柱节点输入及楼面荷载平面图.DWG" "bool")
	 (list "is_jccad" "*wdcnl*.dwg" "bool")
	 (list nil "" ": boxed_column{")
	 (list "is_other" "插入其他DWG文件" "bool")
	 (list "other-str" "通配符" "str")
	 (list "other-scale" "放大倍数" "int")
	 (list nil nil "}")
	 )
       )
       
(init initlist)

;;例子2
(defun c:tt()
  (setq INITLIST (list
		   (list "is_save_windows_rt" "rt时是否保存窗口" "bool")
		   (list "change_color_rt" "rt时改变颜色" "bool")
		   (list "is_princ_tip_rt" "是否打开提示" "bool")
		   (list "replacs_char" "输入替代字符" "str")
	   ))
  (init initlist "dlg")
  )
  [/FONT]
`