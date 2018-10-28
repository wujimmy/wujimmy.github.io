最新版下载:
http://www.jgcad.com/article.asp?id=309

[quote]
(defun c:get-colu-pgl ()
  (princ "\n选择箍筋配筋值:")
  (setq en (single_select (list (cons 0 "*TEXT")(cons 1 "*%%13#*")) nil))
  (princ "\n选择墙大样外边框:")
  (setq	colu-en	(SINGLE_SELECT
		  (list	(cons 0 "LWPOLYLINE")
			(cons 8 "*colu*,*柱*,*墙*,*wall*")
		  )
		  nil
		)
  )
  (get-ss-pgl colu-en en)
)

[/quote]

[file=uploads/200706/09_233215_colugg.rar]体积配箍率计算程序autolisp源码下载[/file]