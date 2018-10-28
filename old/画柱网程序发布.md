作者wujimmy  出自www.wujimmy.com  专贴请注明出处.

对于TSSD的填充功能不大好用,存在好多的限制,
比如要求是柱图层,要求是随层的颜色.

使用方法我就不说了.
命令mybh
[quote]
(Defun c:mybh (/ e e1 la ps si smx ss ssh)

  (command "_undo" "be" "")
  (command "layer" "m" "HATCH" "")
  (if (and 	   
	   (princ "\n选择要填实的柱子<退出>：")
	   (setq
	     ss	(ssget (list  '(0 . "lwpolyline") ))
	   )
      )
    (progn 
	   (setq smx (sslength ss)
		 si  0
	   )
	   (while (< si smx)
	     (setq e  (ssname ss si)
		   si (1+ si)
	     )
	     (if t 
	       (progn 
		      (if nil;(setq e1 (entnext e))
			(command ".-bhatch" "p" "s" "s" e e1 "" "")
			(command ".-bhatch" "p" "s" "s" e "" "")
		      )
		      ;(@htas nil)
	       )
	     )
	   )
    )
  )
(command "_undo" "e" "")
)
[/quote]
[file=uploads/200705/12_073201_mybh.rar]点击下载[/file]