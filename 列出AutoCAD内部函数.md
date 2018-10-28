一个方便,实用,能列出AutoCAD内部函数的小程序 
http://www.xdcad.net/forum/showthread.php?s=&threadid=146898%A1%A3
[quote]

(defun c:test ()
  (setq funn (getstring "\nFunction Name <*>: "))
  (if (= funn "")(setq funn "*")) 
  (setq fl (vl-remove-if-not
             (function (lambda (i)(wcmatch i (strcase funn))))
         (atoms-family 1)
           )
  )
  (if fl
    (foreach i (acad_strlsort fl)(write-line i))
    (alert "no function definition!")
  )
  (princ)
)

[/quote]