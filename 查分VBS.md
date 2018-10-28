Function getHTTPPage(url)
  On Error Resume Next
  Dim http
  Set http = CreateObject("Microsoft.XMLHTTP")
  http.Open "GET", url, False
  http.send
  If http.readystate <> 4 Then
   Exit Function
  End If
  getHTTPPage = bytes2BSTR(http.responseBody)
  Set http = Nothing

 End Function

 Function bytes2BSTR(vIn)
  Dim strReturn
  Dim i1, ThisCharCode, NextCharCode
  strReturn = ""
  For i1 = 1 To LenB(vIn)
   ThisCharCode = AscB(MidB(vIn, i1, 1))
   If ThisCharCode < &H80 Then
    strReturn = strReturn & Chr(ThisCharCode)
   Else
    NextCharCode = AscB(MidB(vIn, i1 + 1, 1))
    strReturn = strReturn & Chr(CLng(ThisCharCode) * &H100 + CInt(NextCharCode))
    i1 = i1 + 1
   End If
  Next
  bytes2BSTR = strReturn
 End Function
 

 
 Function GetMid(txt, StrOne, StrTwo)
 NumOne = InStr(txt, StrOne)
 NumTwo = InStr(txt, StrTwo)
 If NumOne = 0 Or NumTwo = 0 Then GetMid = "": Exit Function
 GetMid = Mid(txt, NumOne + Len(StrOne), NumTwo - NumOne - Len(StrOne))
 End Function
 
 Function mymsgbox(str, time)
Set ws = CreateObject("WScript.shell")
mymsgbox = ws.popup(str, time, str, 1)
End Function
 

'VBScript.RegExp

Function RegExpTest(patrn, strng)
  Dim regEx, Match, Matches     ' 建立变量。
  Set regEx = New RegExp            ' 建立正则表达式。
  regEx.Pattern = patrn         ' 设置模式。
  regEx.IgnoreCase = True           ' 设置是否区分大小写。
  regEx.Global = True           ' 设置全局替换。
  Set Matches = regEx.Execute(strng)    ' 执行搜索。
  For Each Match In Matches     ' 遍历 Matches 集合。
'    retstr = retstr & "Match " & I & " found at position "
'    retstr = retstr & Match.FirstIndex & ". Match Value is " '
    retstr = retstr & Match.Value & "'." & "\t"
  Next
  RegExpTest = retstr
End Function

Function test()

 retstr = getHTTPPage("http://www.8315.cn/sms/fjpta_score_print2.asp?title=全国一、二级注册结构工程师资格考试&year=2008&cmd=ZCJG&zkzh=123&sfzh=321")

 'MsgBox retstr
retstr2 = RegExpTest("..............记录..................................", retstr)
retstrno = RegExpTest("....暂无..............................", retstr)

If (retstr2 <> "") Then
test = mymsgbox(retstr2, 9000)
 Else
test = mymsgbox(retstrno, 10)

End If

End Function

Do While test<>1
'msgbox test
    Wscript.Sleep 200000
Loop