用来做一个造价比较软件时发现两个问题
  1.一个是函数CAL运算速度比较慢,虽然这个函数用来求表达式比较直观,但是速度有比较大的降低,所以后来还是全改过来了.

下面是一个例子,分号后面的是原来的CAL函数计算的.
[quote]
;;;由梁截面求钢筋面积.
;;;(wjmfun_beam_area 300 600 300 14.3 360)
(defun wjmfun_beam_area	(wjm_b wjm_h wjm_m wjm_fc wjm_fy)
  (setq as (+ 30 12.5))
  (setq wjm_m (* wjm_m 1000000))
  
;;;  (setq as_mid (cal "wjm_m/wjm_fc/wjm_b/(wjm_h-as)/(wjm_h-as)"))
;;;  (if (< as_mid 0.5)
;;;    (progn
;;;      (setq Ys (cal "(1+SQRT(1-2*as_mid))/2"))
;;;      (setq epc (cal "1-SQRT(1-2*as_mid)"))
;;;      (setq As (cal "wjm_m/wjm_fy/Ys/(wjm_h-as) "))
;;;    )
;;;    (setq As 999999)
;;;  )

  (setq as_mid (/ wjm_m wjm_fc wjm_b (- wjm_h as) (- wjm_h as)))
  (if (< as_mid 0.5)
    (progn
      (setq Ys (* 0.5 (+ 1 (sqrt (- 1 (* 2 as_mid)) ))))
      (setq epc (- 1 (sqrt (- 1 (* 2 as_mid)) )))
      (setq As (/ wjm_m wjm_fy Ys (- wjm_h as) ))
    )
    (setq As 999999)
  )
  
  (if (> epc epcb)
    (setq As 888888)
    )
  As
)
[/quote]

  2.用表,比较长的表进行操作的话,会用比较多的时间.

[quote]
(setq beam_lst (append beam_lst (list(list  total_money kuadu beam_n beam_b beam_h pan_h ))))
[/quote]