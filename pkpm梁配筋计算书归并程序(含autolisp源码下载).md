最新版见:
http://www.jgcad.com/article.asp?id=265

(PRINC "\n配筋工具，Version 1.00, 版权(c) 2005.06.30 Lin.T.Y, Inc. ")
(PRINC "\n计算体积配箍率的工具")
(princ "\n使用命令gg 计算体积配箍率,\n ggn为中间道数[2,3],ggs为箍筋面积φ12=113.1,φ10=78.5")

(setq gga 4
      ggb 350
      ggc 350
      ggd 400
      ggn 2   ;中间道数
      ggs 113.1 ;箍筋面积,当间距为100时就是单肢箍筋的面积,当间距为s时,就是113.1*100/s
      ggss 100  ;箍筋间距.
)

(defun c:gg (  )
  
  (setq p1 (strcat "\n箍筋肢数<" (rtos gga 2 0)  ">:"))
  (setq n (getreal p1))
  (if (= n nil)
    (setq n gga)
    (setq gga n)
  )
  (setq p1 (strcat "\n箍筋间距<" (rtos ggss 2 0)  ">:"))
  (setq s (getreal p1))
  (if (= s nil)
    (setq s ggss)
    (setq ggss s)
  )

  (setq p1 (strcat "\n墙宽度<" (rtos ggb 2 0) ">:"))
  (setq bw (getreal p1))
  (if (= bw nil)
    (setq bw ggb)
    (setq ggb bw)
  )

  (setq p1 (strcat "\n墙肢1长度<" (rtos ggc 2 0) ">:"))

  (setq l1 (getreal p1))
  (if (= l1 nil)
    (setq l1 ggc)
    (setq ggc l1)
  )
  (setq p1 (strcat "\n墙肢2长度<" (rtos ggd 2 0) ">:"))

  (setq l2 (getreal p1))
  (if (= l2 nil)
    (setq l2 ggd)
    (setq ggd l2)
  )

  (SETQ bwl (- bw 30));箍筋算长度 保护层*2
  (setq bws (- bw 40));箍筋算面积 保护层*2
   
  (setq pgl (/ (+ (* bwl n) (* (+ l1 l2) ggn)) (* bws (+ l1 (+ l2 bws)))))
  (princ "\n体积配箍率为:")
  (setq pgl (* pgl ggs (/ 100 ggss)))
  (princ pgl)
  (princ "%")
  (princ)

)