以下文件可以使得双击.DWG文件的时候,默认采用的CAD版本不一样.

设置当前CAD版本为2002.reg
[quote]
Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\.dwg]
@="AutoCAD.Drawing.15"

[HKEY_CLASSES_ROOT\.dwg\AutoCAD.Drawing.15]

[/quote]
设置当前CAD版本为2004.reg
[quote]
Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\.dwg]
@="AutoCAD.Drawing.16"

[HKEY_CLASSES_ROOT\.dwg\AutoCAD.Drawing.16]

[/quote]