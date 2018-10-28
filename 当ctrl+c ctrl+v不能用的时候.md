[quote]
说明:以下为旧的解决办法,新的解决办法如下:
http://www.jgcad.com/article.asp?id=315
[/quote]

我自定义的拷贝,粘贴命令.
暂不支持块.
其他的可能都支持.

用于,建筑图,不能复制的时候.
[quote]
(defun c:mc() 
  (progn
      (setq sslist (wjm_ss2lst (setq ss(ssget))))
    (setq ss nil)
      (princ "\n复制中...")
      (if sslist
	(progn
	  (setq fn-w-mid (open "c:\\temp.lsp" "w"))
