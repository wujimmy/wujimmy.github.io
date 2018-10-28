用ObjectDBX搜索指定目录是含特定文字的图形

不用打开文件,就可以对文件进行操作.
包括打开文件 获取实体,修改实休,保存文件
以下是关键代码:

;;;创建ObjectDBX实例
(setq dbxdoc
      (vla-GetInterfaceObject 
         (vlax-get-acad-object)
         "ObjectDBX.AxDbDocument"
      )
   )

;;;打开文件
(vla-open dbxdoc filename)
;;获得图纸空间,好像是这么叫的
(setq mSpace(vla-get-modelspace dbxdoc))
;;对图形中每个实休进行操作
(vlax-for eachsub
   mSpace
  (progn
    (vlax-dump-object eachsub) ;; 通过vlisp进行访问实体
    (setq ent (vlax-vla-object->ename eachsub));;;转换成lisp后进行操作
    (setq ent (entget ent))
    (princ ent)
)
)

;;; 添加一个圆,如果要加别的东西就找找相关资料吧
(setq mycircle (vla-addCircle mSpace (vlax-3d-point 3.0 3.0 0.0) 200.0 ))

;;;保存文件: filename是文件名,不知道为什么用 vla-save不可以保存
(vla-saveas dbxdoc filename)
;;;释放实例:
(vlax-release-object dbxdoc)

附件是一个文件夹中所有dwg文件进行查找文字的的程序

[file=uploads/200604/23_115157_s搜索图形.rar]点击下载[/file]