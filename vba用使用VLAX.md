[quote]' VLAX.CLS v2.0 (Last updated 8/1/2003)
' Copyright 1999-2001 by Frank Oquendo
'
' 该程序由明经通道修改支持2004版本
' http://www.mjtd.com
'
' Permission to use, copy, modify, and distribute this software
' for any purpose and without fee is hereby granted, provided
' that the above copyright notice appears in all copies and
' that both that copyright notice and the limited warranty and
' restricted rights notice below appear in all supporting
' documentation.
'
' FRANK OQUENDO (THE AUTHOR) PROVIDES THIS PROGRAM "AS IS" AND WITH
' ALL FAULTS. THE AUTHOR SPECIFICALLY DISCLAIMS ANY IMPLIED WARRANTY
' OF MERCHANTABILITY OR FITNESS FOR A PARTICULAR USE.  THE AUTHOR
' DOES NOT WARRANT THAT THE OPERATION OF THE PROGRAM WILL BE
' UNINTERRUPTED OR ERROR FREE.
'
' Use, duplication, or disclosure by the U.S. Government is subject to
' restrictions set forth in FAR 52.227-19 (Commercial Computer
' Software - Restricted Rights) and DFAR 252.227-7013(c)(1)(ii)
' (Rights in Technical Data and Computer Software), as applicable.
'
' VLAX.cls allows developers to evaluate AutoLISP expressions from
' Visual Basic or VBA
'
' Notes:
' All code for this class module is publicly available througout various posts
' at news://discussion.autodesk.com/autod ... stomization.vba.Idonot 
' claim copyright or authorship on code presented in these posts, only on this
' compilation of that code. In addition, a great big "Thank you!" to Cyrille Fauvel
' demonstrating the use of the VisualLISP ActiveX Module.
'
' Dependencies:
' Use of this class module requires the following application:
' 1. VisualLISP

Private VL As Object
Private VLF As Object

Private Sub Class_Initialize()
    '根据AutoCAD的版本判断使用的库类型
    If Left(ThisDrawing.Application.Version, 2) = "15" Then
        Set VL = ThisDrawing.Application.GetInterfaceObject("VL.Application.1")
    ElseIf Left(ThisDrawing.Application.Version, 2) = "16" Then
        Set VL = ThisDrawing.Application.GetInterfaceObject("VL.Application.16")
    End If
    
    Set VLF = VL.ActiveDocument.Functions
End Sub

Private Sub Class_Terminate()
    '类析构时，释放内存
    Set VLF = Nothing
    Set VL = Nothing
End Sub

Public Function EvalLispExpression(lispStatement As String)
    '根据LISP表达式调用函数
    Dim sym As Object, ret As Object, retVal
    Set sym = VLF.item("read").funcall(lispStatement)
    
    On Error Resume Next
    
    retVal = VLF.item("eval").funcall(sym)
    
    If Err Then
        EvalLispExpression = ""
    Else
        EvalLispExpression = retVal
    End If
End Function

Public Sub SetLispSymbol(symbolName As String, value)

    Dim sym As Object, ret, symValue
    symValue = value
    
    Set sym = VLF.item("read").funcall(symbolName)
    
    ret = VLF.item("set").funcall(sym, symValue)
    EvalLispExpression "(defun translate-variant (data) (cond ((= (type data) 'list) (mapcar 'translate-variant data)) ((= (type data) 'variant) (translate-variant (vlax-variant-value data))) ((= (type data) 'safearray) (mapcar 'translate-variant (vlax-safearray->list data))) (t data)))"
    EvalLispExpression "(setq " & symbolName & "(translate-variant " & symbolName & "))"
    EvalLispExpression "(setq translate-variant nil)"
End Sub

Public Function GetLispSymbol(symbolName As String)

    Dim sym As Object, ret, symValue
    symValue = value
    
    Set sym = VLF.item("read").funcall(symbolName)
    
    GetLispSymbol = VLF.item("eval").funcall(sym)
End Function

Public Function GetLispList(symbolName As String) As Variant
    Dim sym As Object, list As Object
    Dim Count, elements(), i As Long
    
    Set sym = VLF.item("read").funcall(symbolName)
    Set list = VLF.item("eval").funcall(sym)
    
    Count = VLF.item("length").funcall(list)
    
    ReDim elements(0 To Count - 1) As Variant
    
    For i = 0 To Count - 1
        elements(i) = VLF.item("nth").funcall(i, list)
    Next
    
    GetLispList = elements
End Function

Public Sub NullifySymbol(ParamArray symbolName())

    Dim i As Integer
    
    For i = LBound(symbolName) To UBound(symbolName)
        EvalLispExpression "(setq " & CStr(symbolName(i)) & " nil)"
    Next
End Sub

欢迎转载，本文转自[田草博客www.tiancao.net] 原文链接：http://tiancao.net/blogview.asp?logID=290
[/quote]

[separator]
[quote]
Public Sub BlockInsert(Name As String)
Dim pLisp As String
Dim obj As VLAX
Dim pnt(2) As Double
Set obj = New VLAX
Dim pObj  As AcadBlockReference
Set pObj = ThisDrawing.ModelSpace.InsertBlock(pnt, Name, 1, 1, 1, 0)
obj.EvalLispExpression "(setq ed (entget (handent " & ToStr(pObj.Handle) & ")))"
pLisp = "(while (not (= (caddr " & _
"(setq pTime (grread t) " & _
"pSt (car pTime) " & _
"pnt (cond ((= pSt 3) (List 0 0 -1)) ((= pSt 5) (cadr pTime)) (t (List 0 0 1))))) -1)) " & _
"(setq ed (subst (cons 10 pnt) (assoc 10 ed) ed)) " & _
"(entmod ed) " & _
") "
obj.EvalLispExpression pLisp
Set obj = Nothing
End Sub

Public Function ToStr(ByVal str) As String
ToStr = Chr(34) & str & Chr(34)
End Function

Sub Test()
BlockInsert "123"
End Sub

欢迎转载，本文转自[田草博客www.tiancao.net] 原文链接：http://tiancao.net/blogview.asp?logID=290
[/quote]