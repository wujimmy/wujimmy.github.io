Sub 以段为单位建目录_wjm090414()
On Error Resume Next

maxlen = 15 '设定段落最大字数
minlen = 2 '设定段落最小字数
Dim myParagraph As Paragraph
'对每一段落进行操作
For Each myParagraph In ActiveDocument.Paragraphs

'
If myParagraph.Range.Font.Size > 1000 Then Exit For
'
 len1 = Len(myParagraph.Range.Text)
If len1 <= maxlen And len1 >= minlen Then
myParagraph.Range.Font.Size = 13.5
'myParagraph.Range.Font.Size = myParagraph.Range.Font.Size + 2
myParagraph.Range.Bold = True

myParagraph.OutlineLevel = wdOutlineLevel1
Else
myParagraph.Range.Bold = False
'myParagraph.Range.Font.Size = myParagraph.Range.Font.Size + 2
myParagraph.OutlineLevel = wdOutlineLevelBodyText
myParagraph.Range.Font.Size = 10.5

End If

Next myParagraph
End Sub

'版本二,用是过滤含"第" "章"字
Sub 创建文档结图_wjm090414()
On Error Resume Next

maxlen = 55 '设定段落最大字数
minlen = 2 '设定段落最小字数
Dim myParagraph As Paragraph
'对每一段落进行操作
For Each myParagraph In ActiveDocument.Paragraphs

'
If myParagraph.Range.Font.Size > 1000 Then Exit For
'
str1 = myParagraph.Range.Text
len1 = Len(str1)

'b1 = InStr(str1, "：") = 0
'b2 = InStr(str1, ":") = 0
'b3 = InStr(str1, "，") = 0
'b4 = InStr(str1, ",") = 0
'If len1 <= maxlen And len1 >= minlen And b1 And b2 And b3 And b4 Then

b1 = (InStr(str1, "：") <> 0) Or (InStr(str1, ":") <> 0) Or ((InStr(str1, "第") <> 0) And (InStr(str1, "章") <> 0))

If len1 <= maxlen And len1 >= minlen And b1 Then
myParagraph.Range.Font.Size = 13.5
'myParagraph.Range.Font.Size = myParagraph.Range.Font.Size + 2
myParagraph.Range.Bold = True

myParagraph.OutlineLevel = wdOutlineLevel1
Else
myParagraph.Range.Bold = False
'myParagraph.Range.Font.Size = myParagraph.Range.Font.Size + 2
myParagraph.OutlineLevel = wdOutlineLevelBodyText
myParagraph.Range.Font.Size = 10.5

End If

Next myParagraph
End Sub