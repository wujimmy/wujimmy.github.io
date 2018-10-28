从网上弄下来的,整理了一下,为我所用.
因为不喜欢没有源码的东西.

[quote]
(if filter
    (progn
      (princ "\n通过过滤器")
      (princ filter)
      (princ "选择物体")
      (setq myss (ssget filter))
      (princ (getvar "cmdnames"))
      (if (/= "" (getvar "cmdnames"))
	myss
	(progn
	  (if (and (equal (getvar "pickfirst") 1)
		   myss
		   (equal 'PICKSET (type myss))
	      )				;and 
	    (sssetfirst myss myss)
	  )				;if
	  (princ)
          ;;;shhhhh
	)				;progn else
      )
    )
  )
[/quote]

[file=uploads/200706/08_002131_ss.rar]Click Here To Download[/file]