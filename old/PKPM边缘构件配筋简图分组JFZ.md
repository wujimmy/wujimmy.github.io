(defun c:jfz (/ 2d1 2d10 2d11 7d 8d d1 d10 d11 d40 d50 dd dis1 dis2 dxf dxf2
		en en2 i ii line1 line2 p1 p2 ss ss2 str textdxf)
  (setvar "cmdecho" 0)
  (setq @os (getvar "osmode"))(setvar "osmode" 0)  	     
  (command ".undo" "be")
  (setq ss (ssget '((0 . "text") (1 . "(*号)"))))
  (setq i -1)
  (while (setq en (ssname ss (setq i (1+ i))))
    (setq dxf (entget en)
	  7d (assoc 7 dxf)
	  8d (assoc 8 dxf)
	  d1 (cdr (assoc 1 dxf))
	  d10 (cdr (assoc 10 dxf))
	  d11 (cdr (assoc 11 dxf))
	  d40 (cdr (assoc 40 dxf))
	  d50 (cdr (assoc 50 dxf)))
    (setq p1 (polar d10 (+ d50 1.5708) (* 8 d40))
	  p2 (polar d11 (- d50 1.5708) (* 8 d40)))
    (command ".line" d10 p1 "")
    (setq line1 (entlast))
    (command ".line" d11 p2 "")
    (setq line2 (entlast))
    (setq ss2 (ssget "cp" (list d10 p1 d11 p2 d10) '((0 . "text"))))
    (setq ss2 (ssdel en ss2)
	  str d1)
    (if (and ss2 (setq ii -1))
      (repeat (sslength ss2)
	(setq en2 (ssname ss2 (setq ii (1+ ii)))
	      dxf2 (entget en2)
	      2d1 (cdr (assoc 1 dxf2))
	      2d10 (cdr (assoc 10 dxf2))
	      2d11 (cdr (assoc 11 dxf2))
	      2d50 (cdr (assoc 50 dxf2)))
	(setq dis1 (car (@dis-per@ 2d10 line1))
	      dis2 (car (@dis-per@ 2d11 line2)))
	(if (and (equal d50 2d50 0.001)
	         (or (equal dis1 0.0 0.01) (equal dis2 0.0 0.01)))
	  (progn
	    (setq str (strcat str "\\P" 2d1))
	    (if (equal dis1 0.0 0.01)
	      (setq d d10 dd 7))
	    (if (equal dis2 0.0 0.01)
	      (setq d d11 dd 9))
	    (entdel en2)
	  )
	)
      )
    )
    (entdel line1)
    (entdel line2)
    (setq ss2 (ssdel en2 ss2))
    (entdel en)
    (setq TextDxf (list '(0 . "MTEXT") '(100 . "AcDbEntity") '(100 . "AcDbMText")
			8d 7d (cons 10 d) (cons 40 d40) '(41 . 800.0)
			(cons 71 dd) (cons 1 str) (cons 50 d50) '(44 . 0.7)))
    (entmake TextDxf)
  )
  (setvar "osmode" @os)
  (command "undo" "end")
  (princ)
)