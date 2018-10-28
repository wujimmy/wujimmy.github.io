[quote]
(defun c:brr()

  (princ "\n输入要切断的板钢筋:")

  (setq ss (ssget (list (cons 0 "LWPOLYLINE")(cons 90 4))))
  (setq pt (getpoint "\n输入切断点:"))
  (foreach en (wjm_ss2lst ss)
    (setq ptl (EP_LIST en nil))
    (setq pt1 (car ptl)
	  pt2 (cadr ptl)
	  pt3 (caddr ptl)
	  pt4 (last ptl))
    (setq pt-new (WJMF_SHADOW pt pt2 pt3))
    (setq pt5 (polar pt-new (angle pt3 pt2) -100))
    (setq pt6 (polar pt5 (angle pt2 pt1) (distance pt1 pt2)))
    
    (setq pt7 (polar pt-new (angle pt2 pt3) -100))
    (setq pt8 (polar pt7 (angle pt2 pt1) (distance pt1 pt2)))

    ;; draw-pline (pl_list lay_pl width color d70  /)
  
    (draw-pline (list pt1 pt2 pt5 pt6) (dxf 8 en) (dxf 40 en) -1 0)
    (draw-pline (list pt8 pt7 pt3 pt4) (dxf 8 en) (dxf 40 en) -1 0)
    (entdel en)
    )

  )
[/quote]