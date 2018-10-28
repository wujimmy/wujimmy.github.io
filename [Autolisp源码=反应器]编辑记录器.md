本文用于学习交流用.
主要是用了一个反应器技术,使用该技术可以完成很多功能,比如面积标注,
比如图层自动切换,等等.
本程序只是完成了一个框架,里面的部分函数没有给出,请自行修改.

[b] 作者wujimmy
出自www.jgcad.com 专贴请注明出处.

本程序使用了反应器技术,因为CAD的反应器功能不稳定.
所以程序可能出错,请随时做好图纸备份工作.

如果你是程序开发人员,请做好程序测试工作.
反应器的测试不同于其他的程序,程序出错时会直接导致
突然的CAD程序自动关闭.所以为了你的客户的资料安全,
请你做好程序测试工作.[/b]

[quote]
;创建记录器,其实就是一个反应器
(defun C:jl () 
(if (= jlqer nil) (progn
(setq jlqer
       (vlr-acdb-reactor
	 nil
	 '(	  
	   (:vlr-objectModified . jlqCallbackFun)
	   )
	 ))

(setq jlqerOther
       (VLR-Editor-Reactor
	 nil
	 '(
	   ;(:vlr-commandWillStart . jlqCallbackFun)
	   (:vlr-commandEnded . jlqCallbackFun)
	   )
	 ))
)

(princ "已有记录器")
)
  (setvar "MODEMACRO"  "记录器已打开")
)
[/quote]
;;该函数用于解除记录器.
(defun c:ujl ()
  (if jlqer (progn
  (vlr-remove jlqer)
  (vlr-remove jlqerOther)  
  (setq jlqer nil
	jlqerOther nil)
  (setvar "MODEMACRO"  "")
    ))
)

[quote]
;;;记录器回调函数
(defun jlqCallbackFun (notifier-reactor notifier-object / ent str vlrtype *error* )
  (setq olderror *error*)
  (defun *error* (msg)
    ;(command)
    (princ "编辑记录出现错误: ")
    (princ msg)
    (princ)
  )

  (setq vlrtype (vlr-type notifier-reactor))
  (cond
    ((= vlrtype :VLR-Editor-Reactor)
;;;     (if (and (not GetAllList_Reactor) g_uin)
;;;       (progn (setq catchit (vl-catch-all-apply 'GetAllList))
;;;	      (if (vl-catch-all-error-p catchit)
;;;		(progn (princ "\n记录器回调时捕捉到错误:")
;;;		       (princ (vl-catch-all-error-message catchit))
;;;		)
;;;	      )
;;;       )
;;;     ) ;_QQ收取消息列函数
     (if (and (/= jlq_entity nil)
	      (/= jlq_area nil)
	      (/= jlq_now nil)
	      (not (member "MOVE" notifier-object))
	 )
       (progn
;;;	 (vla-put-HyperlinkDisplayTooltip jlq_entity jlq_area)
	 (setq catchit (vl-catch-all-apply 'mySetXData (list jlq_entity (strcat jlq_now jlq_area))))
	 (if(vl-catch-all-error-p catchit) (progn (princ "\n记录器回调时捕捉到错误:")(princ (vl-catch-all-error-message catchit))))
	 (setq jlq_entity nil)
       )
     )
    )
    ((= vlrtype :Vlr-Acdb-Reactor)

;;;(princ (cadr notifier-object))
     (setq jlq_now (menucmd "M=$(edtime,$(getvar,date),YYYY/M/D-HH:MM)"))
     (setq ent (entget (cadr notifier-object)))
     (if (eq "TEXT" (cdr (assoc 0 ent)))
       (progn
	 (setq str (cdr (assoc 1 ent)))
	 (cond
	   (
	    (wcmatch str wjm_箍筋) ;_判断是不是箍筋标注
	    (progn
	      (setq
		jlq_area (strcat "\n箍筋加密区面积:"
				 (rtos (/(cadr(str-to-area str))1) 2 2)
				 "\n  非加密区面积:"
				 (rtos (/(car(str-to-area str))1) 2 2)
			 )
	      )
	      (princ jlq_area)
	    )
	   ) ;_wcmatch箍筋
	   (
	    (or (wcmatch str wjm_纵筋)(wcmatch str wjm_板筋)) ;_判断是不是纵筋标注
	    (progn
	      (setq
		jlq_area (strcat "\n面积:" (rtos (str-to-area str)))
	      )
	      (princ jlq_area)
	    )
	    
	   ) ;_wcmatch纵筋1
	   (t (setq jlq_area nil))
	 ) ;_cond
	 (setq jlq_entity
		(vlax-ename->vla-object (cadr notifier-object))
	 )
       )
       (progn
	 (setq jlq_area nil)
	 (setq jlq_entity nil)
       )
     )
    )

  ) ;_cond

  (setq  *error* olderror)
)
[/quote]
[file=uploads/200706/03_220832_编辑记录器.rar]编辑记录器Autolisp源码点击下载[/file]