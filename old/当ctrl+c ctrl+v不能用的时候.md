为什么叫准加密.
因为加密完了还是可以破解的.

加密的时候,在代码中随机加入一些无用的代码.使得程序运行的速度不会变慢.
但是代码解读起来很费事.

然后,把函数,变量,替换成随机的代码.

有的程序自己读起来都费事,加上这么一搞.
给你源码你也不会明白的了

 [别这样]  [别这样][quote]
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
