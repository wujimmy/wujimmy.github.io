对于图纸比较大的时候,要采用创建视口的办法在布局里面把图分隔成一个一个小图.
然而CAD创建视口的操作比较麻烦.

使用本程序使得该操作变的很简单.
首先在图中采用矩形PL线把视口一个一个的画好.
然后加载本程序(命令:appload,选择该文件)
运行命令vp.
选择上面所画的PL线.
结束.
[quote]
;;文件名:创建视口.lsp
;;作者:吴所不及
;;网址:http://www.jgcad.com/article.asp?act=edit&id=297
(defun c:vp ()
  (princ "\n选择PL线创建视口:")
  (setq ss(ssget (list (cons 0 "*POLYLINE"))))
  (setq sslist (wjm_ss2lst ss))
  (setq pospt (list 0 0 0))
  (foreach en sslist
    (setq obj (vlax-ename->vla-object en))
    (vla-getboundingbox obj 'll 'ur)
    (setq pt1 (vlax-safearray->list ll))
    (setq pt2 (vlax-safearray->list ur))
    (setq cenpt(MIDpt pt1 pt2))
    (setq width (- (car pt2)(car pt1)))
    (setq height (- (cadr pt2)(cadr pt1)))
    (ax:CreateVP
    (vla-get-activedocument (vlax-get-acad-object))
    cenpt
    width
    height
    pospt
  )
    (setq pospt(polar pospt 0 width))
  )  
)

(defun ax:CreateVP (ad center width height pospt / ps ent)
  (setq ps (vla-get-paperspace ad))
  (vla-put-activespace ad acpaperspace)
  (vla-put-mspace ad :vlax-false)
  (setq ent
         (vla-addpviewport
           ps
           (vlax-safearray-fill
             (vlax-make-safearray
               vlax-vbdouble
               (cons 0 2)
             )
             (if pospt pospt center)
           )
           width
           height
         )
  )
  (vla-put-viewporton ent :vlax-true)(vla-display ent :vlax-true)(vla-update ent)
;;;(setq ViewPort (vla-AddPViewport Space (vlax-3d-point 1000 1000) 500 500))
;;;(vla-put-target ent (vlax-3d-point center))
  (vla-put-mspace ad :vlax-true)
  (vla-put-activepviewport ad ent)
  (vla-zoomcenter (vlax-get-acad-object) (vlax-3d-point (car center) (cadr center) 0) 1)
  (vla-put-mspace ad :vlax-false)
; Set the scale.
(vla-put-StandardScale ent 1)
(vla-put-customscale ent 1)
 ent
)
;;;转换选择集为表

(defun wjm_ss2lst (ss / n lst1)
  (if ss
    (repeat (setq n (sslength ss))
      (setq lst1 (cons (ssname ss (setq n (1- n))) lst1))
    )
  )
)
[/quote]