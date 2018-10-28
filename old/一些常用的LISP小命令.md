[quote]

(defun c:5()
  (command "_.scale" (ssget) "" (getpoint "\n选择基点进行0.5倍缩放:") 0.5 "")
  )
(defun c:55 ()
  (vla-startundomark (vla-get-activedocument (vlax-get-acad-object)))

  (setq ss (ssget))
  (setq sslist (mysort ss 3200 1800 nil "xy"))
  (foreach mid-lst sslist
    (setq pt1 (dxf 10 (car mid-lst)))
    (command "_.scale")
    (foreach en	mid-lst
      (command  en )
    )
    (command "" pt1 0.5)
  )
  (vla-EndUndoMark (vla-get-ActiveDocument (vlax-get-acad-object)))
)
(defun c:300 ()
  (vla-startundomark (vla-get-activedocument (vlax-get-acad-object)))
  (princ "\n选择字全改字高为300")
  (setq ss (ssget (list (cons 0 "TEXT"))))
  (setq sslist (wjm_ss2lst ss))
  (foreach en sslist
    (entmod (ch-en (cons 40 300) en))
  )
  (vla-EndUndoMark (vla-get-ActiveDocument (vlax-get-acad-object)))
)
(defun c:500 ()
  (vla-startundomark (vla-get-activedocument (vlax-get-acad-object)))
  (princ "\n选择字全改字高为500")
  (setq ss (ssget (list (cons 0 "TEXT"))))
  (setq sslist (wjm_ss2lst ss))
  (foreach en sslist
    (entmod (ch-en (cons 40 500) en))
  )
  (vla-EndUndoMark (vla-get-ActiveDocument (vlax-get-acad-object)))
)
(defun c:tssd ()
  (if (null (tblsearch "style" "tssd"))
(command "style"  "tssd" "tssdeng.shx,tssdchn.shx" 300 0.7 0 "N" "N" "N")
)
  (vla-startundomark (vla-get-activedocument (vlax-get-acad-object)))
  (princ "\n选择字全改字样式为tssd")
  (setq ss (ssget (list (cons 0 "TEXT"))))
  (setq sslist (wjm_ss2lst ss))
  (foreach en sslist
    (entmod (ch-en (cons 7 "tssd") en))
  )
  (vla-EndUndoMark (vla-get-ActiveDocument (vlax-get-acad-object)))
)
(defun c:tssd2 ()
  (if (null (tblsearch "style" "tssd"))
(command "style"  "tssd2" "tssdeng2.shx,tssdchn.shx" "0" "0.7" "0" "N" "N" "N")
)
  (vla-startundomark (vla-get-activedocument (vlax-get-acad-object)))
  (princ "\n选择字全改字样式为tssd")
  (setq ss (ssget (list (cons 0 "TEXT"))))
  (setq sslist (wjm_ss2lst ss))
  (foreach en sslist
    (entmod (ch-en (cons 7 "tssd2") en))
  )
  (vla-EndUndoMark (vla-get-ActiveDocument (vlax-get-acad-object)))
)

(defun c:zz()(sendkeys "^{TAB}"))

(defun c:tchx(/ mid) (setq mid (ssget (list (cons 0 "TCH*"))))  );_炸开天正的图.

(defun c:vb() (princ "\n移动上一个选择集")(command "_.move" "p" ""))
(defun c:cb() (princ "\n复制上一个选择集")(command "_.copy" "p" ""))
(defun c:eb() (princ "\n删除上一个选择集")(command "_.erase" "p" ""))
(defun c:br ()
  (command)  
  (princ "\n选择要切断的物体:")
  (while (setq mid (entsel))    
    (setq old-osmode (getvar "osmode"))
    (command "_.break"
	     mid
	     "F"
	     (setq pt1 (getpoint "\n输入切断点:"))
	     (progn (setvar "osmode" 0) pt1)
    )
    (setvar "osmode" old-osmode)
  )
)

(defun c:mg()
  (princ "\n选择物体创建无名组:")
  (command "-group" "" "*" "" (ssget) "")
  )
(defun c:mb()
  (init_bonus_error 
    (list(list "REGENMODE" 0 "PICKSTYLE" 1)T)
  )  
  (print "请选择加入块的对象:")
  (setq ss1 (ssget))
  (setq  ptlast (dxf 10(ssname ss1 0)))
  (setq blockname (strcat "wjm" (rtos (abs(car ptlast)) 2 0)(rtos (abs(cadr ptlast)) 2 0)))
  (if (tblsearch "BLOCK" blockname)
    (command "block" blockname "Y" ptlast ss1 "")
    (command "block" blockname ptlast ss1 "")
    )
  (command "insert" blockname ptlast "" "" "")
  (princ (strcat "\n新建块名为:" blockname))
  (restore_old_error)
  )
(defun c:vg()
  (init_bonus_error 
    (list(list "pickbox" 12 "PICKSTYLE" 1)T)
  )
  (princ "\n选择物体组移动:")
  (command "_.move" pause pause pause pause)
  (restore_old_error)
  )
(defun c:cg()
  (init_bonus_error 
    (list(list "pickbox" 12 "PICKSTYLE" 1)T)
  )
  (princ "\n选择物体组复制:")
  (command "_.copy" pause pause pause pause)
  (restore_old_error)
  )
[/quote]