在调用command命令的时候,先调用一下(command)
这样可以解决一些意想不到的问题.

主要是把R14下面的一些程序用到cad2002的时候,会出现一些问题.
比如先选择,后执行命令,就有可能出错.
参见CAD2002的readme文件:

[quote]
AutoLISP

在包含在此 ObjectARX SDK 版本中的 AutoCAD 版本中，如果 AutoLISP 开发人员通过 *error* 机制来替换自己的错误处理程序，并且在该错误处理程序中发出 (command ...) 调用，则可能出现问题。AutoCAD 没有正确地清除 AutoLISP (command ...) 所使用的 acedCommand() 函数的状态。解决此问题有一个简单的办法：在发出有用的 (command ...) 调用之前发出一个空的 (command) 调用。以下是可能发生此现象的情况样例：

(defun c:bug ()
(setq *error* bug_err)
(nentsel "\nPress escape to show the defect...")
)
(defun bug_err (s)
(command "._undo" "_end") 

)

解决办法在下面的错误处理程序中示例：

(defun bug_err (s)  (command)            ; 清除 (command ...) 状态
(command "._undo" "_end") 

)
[/quote]