VBA 改变文字高度.bas

[quote]
Attribute VB_Name = "NewMacros"
Sub Macro1()
Attribute Macro1.VB_Description = "宏在 2008-4-20 由 FiSh 录制"
Attribute Macro1.VB_ProcData.VB_Invoke_Func = "Normal.NewMacros.Macro1"
'
' Macro1 Macro
' 宏在 2008-4-20 由 FiSh 录制
'
    Selection.Font.Size = 14
End Sub

'   1. 以Paragraphs(段)为操作对象,将文档中的每一段的字号都减小一号
 '   如果Word文档中的各段落的字号不相同 , 但段落内部的字号都相同, 则可以通过改变段落对象的字号属性来达到我们的目的?代码如下?
    Sub 以段为单改字高()
    On Error Resume Next
    Dim myParagraph As paragraph
    '对每一段落进行操作
     For Each myParagraph In ActiveDocument.Paragraphs
     
    '如果该段落中的字号不尽一致或有其他格式,Word段落字号属性的返回值将为9999 9,此时使用段落对象模型不能改变该段落的字号,故退到下一段
    If myParagraph.Range.Font.Size > 1000 Then Exit For
    '将该段的字号减小一号
    myParagraph.Range.Font.Size = myParagraph.Range.Font.Size + 1
    Next myParagraph
    End Sub
   ' 2. 以Sentences(句子)为对象,将文档中每一句的字号都减小一号
    Sub 以句为单位改字高()
    On Error Resume Next
    Dim myParagraph As paragraph
    '对每一段落进行操作
     For Each myParagraph In ActiveDocument.Paragraphs
    Dim I, J As Integer
    '统计每一段中句子的总数
    J = myParagraph.Range.Sentences.Count
    For I = 1 To J
    '防止同一句中出现不同的字号
    If myParagraph.Range.Sentences(I).Font.Size > 1000 Then Exit For
    '将每一句的字号减小一号
    myParagraph.Range.Sentences(I).Font.Size = myParagraph.Range.Sentences(I).Font.Size + 1
    Next I
     Next myParagraph
    End Sub
    
    '3. 以Words(单词)为操作对象,将文档中的每一单词的字号都减小一号
        Sub 以单词为单位改字高()
    On Error Resume Next
    Dim myParagraph As paragraph
    '对每一段落进行操作

    For Each myParagraph In ActiveDocument.Paragraphs
    '统计每一段中总单词数
    J = myParagraph.Range.Words.Count
    '将每一个单词的字号减小一号
    For I = 1 To J
    myParagraph.Range.Words(I).Font.Size = myParagraph.Range.Words(I).Font.Size + 1
    Next I
     Next myParagraph
    End Sub
   ' 4. 以Characters(单字)为操作对象,将文档中的每一个字的字号减小一号
    Sub 以单字为单位改字高()
    On Error Resume Next
    Dim myParagraph As paragraph
    For Each myParagraph In ActiveDocument.Paragraphs
    '统计每一段中总字数
    J = myParagraph.Range.Characters.Count
    '将每一个字的字号减小一号
    For I = 1 To J
    myParagraph.Range.Characters(I).Font.Size = myParagraph.Range.Characters(I).Font.Size + 1
    Next I
     Next myParagraph
    End Sub
  '  带格式单词的替换
   ' Word自身有替换命令 (ctrl + h), 但该命令的不足之处是, 不能对带格式的单词进行替换, 例如, 要将整篇文档中的H2CO3替换成H2CO3, 该命令就无能为力了?下面介绍如何借助Word中的对象模型来实现替换?
    Sub ReplaceWord()
    On Error Resume Next
    '对文档中的H2CO3进行格式替换
    Dim myParagraph As paragraph
    Dim I, J As Integer
    Dim tmpStr As String
    '对每一段进行操作
    For Each myParagraph In ActiveDocument.Paragraphs
    '统计该段的单词数
    J = myParagraph.Range.Words.Count
    For I = 1 To J
    '比较字符串,查找所有替换的单词
    If (LCase(myParagraph.Range.words(I)) = "h2co3")
    Then
    '选择所替换的单词
    myParagraph.Range.Words(I).Select
    '替换单词,写入字母H
    Selection.TypeText Text:="H"
    '将其格式变为下标
    Selection.Font.Subscript = True
    '写入下标2
    Selection.TypeText Text:="2"
    '字体变为正常体
    Selection.Font.Subscript = False
    '写入字母CO
    Selection.TypeText Text:="CO"
    '将其格式变为下标
    Selection.Font.Subscript = True
    '写入下标3
    Selection.TypeText Text:="3"
    '字体变为正常体
    Selection.Font.Subscript = False
    End If
    Next I
    Next myParagraph
    End Sub

[/quote]