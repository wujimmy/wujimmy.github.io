[quote]
(defun c:mypt ()
  (setq ss (ssget '((0 . "LWPOLYLINE")(62 . 5))))
  (setq ss-list (WJM_SS2LST ss))

    (setq    AcadObject   (vlax-get-acad-object)
       AcadDocument (vla-get-ActiveDocument AcadObject)
       mSpace        (vla-get-ModelSpace AcadDocument)

  )
  (setq preferenceSel (vla-get-Preferences AcadObject))
  (setq fileSel (vla-get-Files preferenceSel))

  (setq filedir(vla-get-PrinterConfigPath fileSel));_打印机.
  (setq plots (vl-directory-files filedir "*.pc3"))
  (setq style (myp:get_properties plots))
  (setq style (substr style 1 (- (strlen style) 4)))
  
  (setq filedir(vla-get-PrinterStyleSheetPath fileSel));_打印样式.
  (setq plot-styles (vl-directory-files filedir "*.ctb"))
  (setq plot (myp:get_properties plot-styles))
  (setq plot (substr plot 1 (- (strlen plot) 4)))
 
  (foreach en ss-list
    (progn
      (setq obj (vlax-ename->vla-object en))
      (vla-getboundingbox obj 'll 'ur)
      (setq pt1 (vlax-safearray->list ll))
      (setq pt2 (vlax-safearray->list ur))
      (command "_.PLOT"
	       "Y";_是否需要详细打印配置？[是(Y)/否(N)] <否>: y
	       "";_输入布局名或 [?] <模型>:
	       plot;_输入输出设备的名称或 [?] <在 网管 上自动 HP LaserJet 5100 PCL 6>:
	       "A3";_输入图纸尺寸或 [?] <A3>:
	       
	       "m";_输入图纸单位 [英寸(I)/毫米(M] <毫米>:
	       "L";_输入图形方向 [纵向(P)/横向(L)] <横向>:
	       "N";_是否反向打印？[是(Y)/否(N)] <否>:
	       "W";_输入打印区域 [显示(D)/范围(E)/图形界限(L)/视图(V)/窗口(W)] <范围>: w
	       pt1;_输入窗口的左下角 <0.000000,0.000000>: 输入窗口的右上角 <0.000000,0.000000>: 
	       pt2;_输入窗口的右上角 <0.000000,0.000000>: 
	       "f";_输入打印比例 (打印的 毫米=图形单位) 或 [布满(F)] <Fit>: fit
	       "c";_输入打印偏移 (x,y) 或 [居中打印(C)] <0.00,0.00>: c
	       "Y";_是否按样式打印？[是(Y)/否(N)] <是>:
	       style;_输入打印样式表名称或 [?] (输入 . 表示无) <hp5100.ctb>:
	       "Y";_是否打印线宽？[是(Y)/否(N)] <是>:
	       "N";_是否删除隐藏线？[是(Y)/否(N)] <否>:
	       "N" ;_是否打印到文件 [是(Y)/否(N)] <N>: y
	       "Y";_是否保存模型选项卡的修改 .
	       "Y";_是否继续打印 .
	      )
      (princ "\n*********************\n")
    )
  )
)
[/quote]
[file=uploads/200706/28_233229_mypt.rar]Click Here To Download[/file]