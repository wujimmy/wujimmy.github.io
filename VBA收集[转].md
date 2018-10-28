本示例为设置密码窗口 (1) 
If Application.InputBox("请输入密码：") = 1234 Then 
[A1] = 1 '密码正确时执行 
Else: MsgBox "密码错误，即将退出！" '此行与第2行共同设置密码 
End If 

本示例为设置密码窗口 (1) 
X = MsgBox("是否真的要结帐？", vbYesNo) 
If X = vbYes Then 
Close 

本示例为设置工作表密码 
ActiveSheet.Protect Password:=641112 ' 保护工作表并设置密码 
ActiveSheet.Unprotect Password:=641112 '撤消工作表保护并取消密码 

'本示例关闭除正在运行本示例的工作簿以外的其他所有工作簿，并保存其更改内容 

。 
For Each w In Workbooks 
If w.Name ThisWorkbook.Name Then 
w.Close SaveChanges:=True 
End If 
Next w 

'每次打开工作簿时，本示例都最大化 Microsoft Excel 窗口。 
Application.WindowState = xlMaximized 

'本示例显示活动工作表的名称。 
MsgBox "The name of the active sheet is " & ActiveSheet.Name 

'本示例保存当前活动工作簿的副本。 
ActiveWorkbook.SaveCopyAs "C:\TEMP\XXXX.XLS" 

'下述过程激活工作簿中的第四张工作表。 
Sheets(4).Activate 

'下述过程激活工作簿中的第1张工作表。 
Worksheets(1).Activate 

'本示例通过将 Saved 属性设为 True 来关闭包含本段代码的工作簿，并放弃对该 

工作簿的任何更改。 
ThisWorkbook.Saved = True 
ThisWorkbook.Close 

'本示例对自动重新计算功能进行设置，使 Microsoft Excel 不对第一张工作表自 

动进行重新计算。 
Worksheets(1).EnableCalculation = False 

'下述过程打开 C 盘上名为 MyFolder 的文件夹中的 MyBook.xls 工作簿。 
Workbooks.Open ("C:\MyFolder\MyBook.xls") 

'本示例显示活动工作簿中工作表 sheet1 上单元格 A1 中的值。 
MsgBox Worksheets("Sheet1").Range("A1").Value 

本示例显示活动工作簿中每个工作表的名称 
For Each ws In Worksheets 
MsgBox ws.Name 
Next ws 

本示例向活动工作簿添加新工作表 , 并设置该工作表的名称? 
Set NewSheet = Worksheets.Add 
NewSheet.Name = "current Budget" 

本示例将新建的工作表移到工作簿的末尾 
'Private Sub Workbook_NewSheet(ByVal Sh As Object) 
Sh.Move After:=Sheets(Sheets.Count) 
End Sub 

本示例将新建工作表移到工作簿的末尾 
'Private Sub App_WorkbookNewSheet(ByVal Wb As Workbook, _ 
ByVal Sh As Object) 
Sh.Move After:=Wb.Sheets(Wb.Sheets.Count) 
End Sub 

本示例新建一张工作表，然后在第一列中列出活动工作簿中的所有工作表的名称。 
Set NewSheet = Sheets.Add(Type:=xlWorksheet) 
For i = 1 To Sheets.Count 
NewSheet.Cells(i, 1).Value = Sheets(i).Name 
Next i 

本示例将第十行移到窗口的最上面? 
Worksheets("Sheet1").Activate 
ActiveWindow.ScrollRow = 10 

当计算工作簿中的任何工作表时，本示例对第一张工作表的 A1:A100 区域进行排序 

。 
'Private Sub Workbook_SheetCalculate(ByVal Sh As Object) 
With Worksheets(1) 
.Range("a1:a100").Sort Key1:=.Range("a1") 
End With 
End Sub 
本示例显示工作表 Sheet1 的打印预览。 
Worksheets("Sheet1").PrintPreview 

本示例保存当前活动工作簿? 
ActiveWorkbook.Save 

本示例保存所有打开的工作簿，然后关闭 Microsoft Excel。 
For Each w In Application.Workbooks 
w.Save 
Next w 
Application.Quit 

下例在活动工作簿的第一张工作表前面添加两张新的工作表? 
Worksheets.Add Count:=2, Before:=Sheets(1) 

本示例设置 15 秒后运行 my_Procedure 过程，从现在开始计时。 
Application.OnTime Now + TimeValue("00:00:15"), "my_Procedure" 

本示例设置 my_Procedure 在下午 5 点开始运行。 
Application.OnTime TimeValue("17:00:00"), "my_Procedure" 

本示例撤消前一个示例对 OnTime 的设置。 
Application.OnTime EarliestTime:=TimeValue("17:00:00"), _ 
Procedure:="my_Procedure", Schedule:=False 

每当工作表重新计算时，本示例就调整 A 列到 F 列的宽度。 
'Private Sub Worksheet_Calculate() 
Columns("A:F").AutoFit 
End Sub 

本示例使活动工作簿中的计算仅使用显示的数字精度。 
ActiveWorkbook.PrecisionAsDisplayed = True 

本示例将工作表 Sheet1 上的 A1:G37 区域剪下，并放入剪贴板。 
Worksheets("Sheet1").Range("A1:G37").Cut 

Calculate 方法 
计算所有打开的工作簿、工作簿中的一张特定的工作表或者工作表中指定区域的单元 

格，如下表所示： 
'要计算 '依照本示例 
所有打开的工作簿 ' Application.Calculate （或只是 Calculate 

） 
指定工作表 '计算指定工作表Sheet1 Worksheets 

("Sheet1").Calculate 
指定区域 'Worksheets(1).Rows(2).Calculate 

本示例对自动重新计算功能进行设置，使 Microsoft Excel 不对第一张工作表自动 

进行重新计算。 
Worksheets(1).EnableCalculation = False 

本示例计算 Sheet1 已用区域中 A 列、B 列和 C 列的公式。 
Worksheets("Sheet1").UsedRange.Columns("A:C").Calculate 

本示例更新当前活动工作簿中的所有链接? 
ActiveWorkbook.UpdateLink Name:=ActiveWorkbook.LinkSources 

本示例设置第一张工作表的滚动区域? 
Worksheets(1).ScrollArea = "a1:f10" 

本示例新建一个工作簿，提示用户输入文件名，然后保存该工作簿。 
Set NewBook = Workbooks.Add 
Do 
fName = Application.GetSaveAsFilename 
Loop Until fName False 
NewBook.SaveAs Filename:=fName 

本示例打开 Analysis.xls 工作簿，然后运行 Auto_Open 宏。 
Workbooks.Open "ANALYSIS.XLS" 
ActiveWorkbook.RunAutoMacros xlAutoOpen 

本示例对活动工作簿运行 Auto_Close 宏，然后关闭该工作簿。 
With ActiveWorkbook 
.RunAutoMacros xlAutoClose 
.Close 
End With 

在本示例中，Microsoft Excel 向用户显示活动工作簿的路径和文件名称。 
'Sub UseCanonical() 
Display the full path to user. 
MsgBox ActiveWorkbook.FullNameURLEncoded 
End Sub 

本示例显示当前工作簿的路径及文件名（假定尚未保存此工作簿）。 
MsgBox ActiveWorkbook.FullName 

本示例关闭 Book1.xls，并放弃所有对此工作簿的更改。 
Workbooks("BOOK1.XLS").Close SaveChanges:=False 

本示例关闭所有打开的工作簿。如果某个打开的工作簿有改变，Microsoft Excel 

将显示询问是否保存更改的对话框和相应提示。 
Workbooks.Close 

本示例在打印之前对当前活动工作簿的所有工作表重新计算? 
'Private Sub Workbook_BeforePrint(Cancel As Boolean) 
For Each wk In Worksheets 
wk.Calculate 
Next 
End Sub 

本示例对查询表一中的第一列数据进行汇总，并在数据区域下方显示第一列数据的总 

和。 
Set c1 = Sheets("sheet1").QueryTables(1).ResultRange.Columns(1) 
c1.Name = "Column1" 
c1.End(xlDown).Offset(2, 0).Formula = "=sum(Column1)" 

本示例取消活动工作簿中的所有更改? 
ActiveWorkbook.RejectAllChanges 

本示例在商业问题中使用规划求解函数，以使总利润达到最大值。SolverSave 函数 

将当前问题保存到活动工作表上的某一区域。 
Worksheets("Sheet1").Activate 
SolverReset 
SolverOptions Precision:=0.001 
SolverOK SetCell:=Range("TotalProfit"), _ 
MaxMinVal:=1, _ 
ByChange:=Range("C4:E6") 
SolverAdd CellRef:=Range("F4:F6"), _ 
Relation:=1, _ 
FormulaText:=100 
SolverAdd CellRef:=Range("C4:E6"), _ 
Relation:=3, _ 
FormulaText:=0 
SolverAdd CellRef:=Range("C4:E6"), _ 
Relation:=4 
SolverSolve UserFinish:=False 
SolverSave SaveArea:=Range("A33") 

本示例隐藏 Chart1、Chart3 和 Chart5。 
Charts(Array("Chart1", "Chart3", "Chart5")).Visible = False 

当激活工作表时，本示例对 A1:A10 区域进行排序。 
'Private Sub Worksheet_Activate() 
Range("a1:a10").Sort Key1:=Range("a1"), Order:=xlAscending 
End Sub 

本示例更改 Microsoft Excel 链接。 
ActiveWorkbook.ChangeLink "c:\excel\book1.xls", _ 
"c:\excel\book2.xls", xlExcelLinks 

本示例启用受保护的工作表上的自动筛选箭头? 
ActiveSheet.EnableAutoFilter = True 
ActiveSheet.Protect contents:=True, userInterfaceOnly:=True 

本示例将活动工作簿设为只读? 
ActiveWorkbook.ChangeFileAccess Mode:=xlReadOnly 

本示例使共享工作簿每三分钟自动更新一次? 
ActiveWorkbook.AutoUpdateFrequency = 3 

下述 Sub 过程清除活动工作簿中 Sheet1 上的所有单元格的内容。 
'Sub ClearSheet() 
Worksheets("Sheet1").Cells.ClearContents 
End Sub 

本示例对所有工作簿都关闭滚动条? 
Application.DisplayScrollBars = False 

如果具有密码保护的工作簿的文件属性没有加密，则本示例设置指定工作簿的密码加 

密选项。 
'Sub SetPasswordOptions() 
With ActiveWorkbook 
If .PasswordEncryptionProvider "Microsoft RSA SChannel 

Cryptographic Provider" Then 
.SetPasswordEncryptionOptions _ 
PasswordEncryptionProvider:="Microsoft RSA SChannel 

Cryptographic Provider", _ 
PasswordEncryptionAlgorithm:="RC4", _ 
PasswordEncryptionKeyLength:=56, _ 
PasswordEncryptionFileProperties:=True 
End If 
End With 
End Sub 

在本示例中，如果活动工作簿不能进行写保护，那么 Microsoft Excel 设置字符串 

密码以作为活动工作簿的写密码。 
'Sub UseWritePassword() 
Dim strPassword As String 
strPassword = "secret" 
' Set password to a string if allowed. 
If ActiveWorkbook.WriteReserved = False Then 
ActiveWorkbook.WritePassword = strPassword 
End If 
End Sub 

在本示例中，Microsoft Excel 打开名为 Password.xls 的工作簿，设置它的密码 

，然后关闭该工作簿。本示例假定名为 Password.xls 的文件位于 C:\ 驱动器上。 
'Sub UsePassword() 

Dim wkbOne As Workbook 

Set wkbOne = Application.Workbooks.Open("C:\Password.xls") 

wkbOne.Password = "secret" 
wkbOne.Close 
'注意 Password 属性可读并返回 “********”。 
End Sub 

本示例将 Book1.xls 的当前窗口更改为显示公式。 
Workbooks("BOOK1.XLS").Worksheets("Sheet1").Activate 
ActiveWindow.DisplayFormulas = True 

'本示例接受活动工作簿中的所有更改? 
ActiveWorkbook.AcceptAllChanges 

本示例显示活动工作簿的路径和名称 
Sub UseCanonical() 
MsgBox '消息框 
[b7] = ActiveWorkbook.FullName '当前工作簿 
[b8] = ActiveWorkbook.FullNameURLEncoded '活动工作簿 
End Sub 

本示例显示 Microsoft Excel 启动文件夹的完整路径。 
MsgBox Application.StartupPath 

本示例显示活动工作簿中每个工作表的名称。 
For Each ws In Worksheets 
MsgBox ws.Name 
Next ws 

本示例关闭除正在运行本示例的工作簿以外的其他所有工作簿，并保存其更改内容。 
For Each w In Workbooks 
If w.Name ThisWorkbook.Name Then 
w.Close savechanges:=True 
End If 
Next w 

Activate 事件 
激活一个工作簿、工作表、图表或嵌入图表时产生此事件。 
当激活工作表时，本示例对 A1:A10 区域进行排序。 
Private Sub Worksheet_Activate() 
Range("a1:a10").Sort Key1:=Range("a1"), Order:=xlAscending 
End Sub 

Calculate 事件 
对于 Worksheet 对象，在对工作表进行重新计算之后产生此事件 
每当工作表重新计算时，本示例就调整 A 列到 F 列的宽度。 
Private Sub Worksheet_Calculate() 
Columns("A:F").AutoFit 
End Sub 

BeforeDoubleClick 事件 
应用于 Worksheet 对象的 Activate 方法。 
当双击某工作表时产生此事件，此事件先于默认的双击操作。 
Private Sub expression_BeforeDoubleClick(ByVal Target As Range, Cancel 

As Boolean) 
expression 引用在类模块中带有事件声明的 Worksheet 类型对象的变量。 
Target 必需。双击发生时最靠近鼠标指针的单元格。 
Cancel 可选。当事件发生时为 False。如果事件过程将该参数设为 True，则该 

过程执行完之后将不进行默认的双击操作。 

BeforeRightClick 事件 
应用于 Worksheet 对象的 Activate 方法。 
当用鼠标右键单击某工作表时产生此事件，此事件先于默认的右键单击操作。 
Private Sub expression_BeforeRightClick(ByVal Target As Range, Cancel 

As Boolean) 
expression 引用在类模块中带有事件声明的 Worksheet 类型对象的变量。 
Target 必需。右键单击发生时最靠近鼠标指针的单元格。 
Cancel 可选。当事件发生时为 False。如果该事件过程将本参数设为 True，则 

该过程执行结束之后不进行默认的右键单击操作。 

Change 事件 
当用户更改工作表中的单元格，或外部链接引起单元格的更改时产生此事件。 
Private Sub Worksheet_Change(ByVal Target As Range) 
Target 更改的区域。可以是多个单元格。 
说明 
重新计算引起的单元格更改不触发本事件。可使用 Calculate 事件俘获工作表重新 

计算操作。 
本示例将更改的单元格的颜色设为蓝色。 
Private Sub Worksheet_Change(ByVal Target as Range) 
Target.Font.ColorIndex = 5 
End Sub 

Deactivate 事件 
图表、工作表或工作簿从活动状态转为非活动状态时产生此事件。 
Private Sub object_Deactivate() 
object Chart、Workbook 或者 Worksheet。有关对 Chart 对象使用事件的详细 

信息，请参阅 Chart 对象事件的用法。 
本示例当工作簿转为非活动状态时，对所有打开的窗口进行排列。 
Private Sub Workbook_Deactivate() 
Application.Windows.Arrange xlArrange 
End Sub 

FollowHyperlink 事件 
当单击工作表上的任意超链接时，发生此事件。对于应用程序级或工作簿级的事件， 

请参阅 SheetFollowHyperlink 事件。 
Private Sub Worksheet_FollowHyperlink(ByVal Target As Hyperlink) 
Target Hyperlink 类型，必需。一个代表超链接目标位置的 Hyperlink 对象。 
本示例对在当前活动工作簿中访问过的所有链接保留一个列表或历史记录。 
Private Sub Worksheet_FollowHyperlink(ByVal Target As Hyperlink) 
With UserForm1 
.ListBox1.AddItem Target.Address 
.Show 
End With 
End Sub 

PivotTableUpdate 事件 
发生在工作簿中的数据透视表更新之后。 
Private Sub expression_PivotTableUpdate(ByVal Target As PivotTable) 
expression 引用在类模块中带有事件声明的 Worksheet 类型对象的变量。 
Target 必需。选定的数据透视表。 
本示例显示一则消息，说明数据透视表已经更新。本示例假定您已在类模块中声明了 

带有事件的 Worksheet 类型的对象。 
Private Sub Worksheet_PivotTableUpdate(ByVal Target As PivotTable) 
MsgBox "The PivotTable connection has been updated." 
End Sub 

SelectionChange 事件 
当工作表上的选定区域发生改变时，将产生本事件。 
Private Sub Worksheet_SelectionChange(ByVal Target As Excel.Range) 
Target 新选定的区域。 
本示例滚动工作簿窗口，直至选定区域位于窗口的左上角。 
Private Sub Worksheet_SelectionChange(ByVal Target As Range) 
With ActiveWindow 
.ScrollRow = Target.Row 
.ScrollColumn = Target.Column 
End With 
End Sub 

本示例显示活动工作簿中工作表 sheet1 上单元格 A1 中的值。 
MsgBox Worksheets("Sheet1").Range("A1").Value 

本示例显示活动工作簿中每个工作表的名称。 
For Each ws In Worksheets 
MsgBox ws.Name 
Next ws 

本示例向活动工作簿添加新工作表，并设置该工作表的名称。 
Set newSheet = Worksheets.Add 
newSheet.Name = "current Budget" 

本示例关闭工作簿 Book1.xls，但不提示用户保存所作更改。Book1.xls 中的所有 

更改都不会保存。 
Application.DisplayAlerts = False 
Workbooks("BOOK1.XLS").Close 
Application.DisplayAlerts = True 

本示例设置保存文件时显示提示，要求用户输入汇总信息。 
Application.PromptForSummaryInfo = True 

本示例显示 Microsoft Excel 的完整路径。 
Private Sub aa() 
MsgBox "The path is " & Application.Path 
End Sub 

示例显示每一个可用加载宏的路径及文件名。 
For Each a In AddIns 
MsgBox a.FullName 
Next a 

ChDir 语句 
改变当前的目录或文件夹。 
ChDir path 
在 Power Macintosh 中，默认驱动器总是改为在 path 语句中指定的驱动器。完整 

路径指定由卷标名开始，相对路径由冒号 (:) 开始. ChDir 可以辨认路径中指定的 

别名: 
ChDir "MacDrive:Tmp" ' 在 Macintosh 中 

本示例显示当前路径分隔符。 
MsgBox "The path separator character is " & _ 
Application.PathSeparator 

Move 方法 
将一个指定的文件或文件夹从一个地方移动到另一个地方。 
语法 
object.Move destination 
Move 方法语法有如下几部分： 
部分 描述 
object 必需的。始终是一个 File 或 Folder 对象的名字。 
destination 必需的。文件或文件夹要移动到的目标。不允许有通配符。 

CreateFolder 方法 
创建一个文件夹。 
语法 
object.CreateFolder(foldername) 
reateFolder 方法有如下几部分： 
部分 描述 
object 必需的。始终是一个 FileSystemObject 的名字。 
foldername 必需的。字符串表达式，它标识创建的文件夹。 

本示例使用 MkDir 语句来创建目录或文件夹。如果没有指定驱动器，新目录或文件 

夹将会建在当前驱动器中。 
MkDir "MYDIR" ' 建立新的目录或文件夹。 

Name 语句示例 
本示例使用 Name 语句来更改文件的名称。示例中假设所有使用到的目录或文件夹都 

已存在。 在 Macintosh 中，默认驱动器名称是 “HD” 并且路径部分由冒号取代 

反斜线隔开。 
Dim OldName, NewName 
OldName = "OLDFILE": NewName = "NEWFILE" ' 定义文件名。 
Name OldName As NewName ' 更改文件名。 
OldName = "C:\MYDIR\OLDFILE": NewName = "C:\YOURDIR\NEWFILE" 
Name OldName As NewName ' 更改文件名，并移动文件。 

本示例显示当前默认文件路径。 
MsgBox "The current default file path is " & _ 
Application.DefaultFilePath 

本示例设置替换启动文件夹。 
Application.AltStartupPath = "C:\EXCEL\MACROS" 

FolderExists 方法 
如果指定的文件夹存在返回 True，不存在返回 False。 
语法 
object.FolderExists(folderspec) 

本示例在单元格中启用编辑。 
Application.EditDirectlyInCell = True 

程序说明： 
几种用VBA在单元格输入数据的方法： 
Public Sub Writes() 
1-- 2 方法，最简单在 "[ ]" 中输入单元格名称。 
1 [A1] = 100 '在 A1 单元格输入100。 
2 [A2:A4] = 10 '在 A2:A4 单元格输入10。 
3-- 4 方法，采用 Range(" ")， " " 中输入单元格名称。 
3 Range("B1") = 200 '在 B1 单元格输入200。 
4 Range("C1:C3") = 300 '在 C1:C3 单元格输入300。 
5-- 6 方法，采用 Cells(Row,Column)，Row是单元格行数，Column是单元格栏数。 
5 Cells(1, 4) = 400 '在 D1 单元格输入400。 
6 Range(Cells(1, 5), Cells(5, 5)) = 50 '在 E1:E 5单元格输入50。 
End Sub 

你点选任何单元格，按 Selection 按钮，則则所点选的单元格均会被输入文字 

"Test"。 
Public Sub Selection1() 
Selection.Value = "Test" '在任何你点选的单元格输入文字 "Test"。 
End Sub 

VBALesson2 程序说明： 
几种如何把别的工作表 Sheet4 数据，读到这个工作表的方法：在被读取的单元格 

前加上工作表名称 Sheet4。 
Public Sub Writes() 
1-- 2 方法，最简单在被读取的 "[ ]" 前加上被读取的工作表名称 Sheet4。 
1 [A1] = Sheet4.[A1] '把Sheet4 A1 单元格的数据，读到 A1单元格。 
2 [A2:A4] = Sheet4.[B1] ''把 Shee4 工作表单元格 B1 数据，读到 A2:A4 

单元格。 
3-- 4 方法，在被读取的工作表 Range(" ")的 Range 前加上被读取的工作表名称 

Sheet4。 
3 Range("B1") = Sheet4.Range("B1") ''把 Shee4工作表单元格 B1 数据，读 

到 B1 单元格。 
4 Range("C1:C3") = Sheet4.Range("C1") '把 Shee4 工作表单元格 C1 数据 

，读到 C1:C3 单元格。 
5-- 6 方法，在被读取的工作表 Cells(Row,Column)，Cells 前加上被读取工作表 

名称 Sheet4。 
5 Cells(1, 4) = Sheet4.Cells(1, 4) '把 Shee4 工作表单元格 D1 数据，读 

到 D1 单元格。 
6 Range(Cells(1, 5), Cells(5, 5)) = Sheet4.Cells(1, 5) '把 Shee4 工 

作表单元格 E1 数据，读到 E1:E 5单元格。 
End Sub 

你点选任何单元格，按 Selection 按钮，则所点选的单元格均会被输入 Shee4 工 

作表单元格 F1 数据。 
Public Sub Selection1() 
Selection.Value = Sheet4.[F1] '把 Shee4 工作表单元格 F1 数据，读到任 

何你点选的单元格。 
End Sub 

VBALesson3 程序说明： 
如何利用 Worksheet_SelectionChange 输入数据的方法。 
Private Sub Worksheet_SelectionChange(ByVal Target As Range) 
Target = 100 
End Sub 

Target 指的是你鼠标所选的单元格，Worksheet_SelectionChange() 事件的参数 

。 
可以是一个也可以是好几个单元格。 
Range 是 Excel 特有的变量形态，叫范围。 
Target As Rang 是把 Target 这个参数设定为 Range 变量形态。 
Target = 100 是把你点选的单元格输入数字100。 

VBALesson4 程序说明： 
如何利用 Worksheet_SelectionChange 在限定的单元格输入数据的方法。 
Private Sub Worksheet_SelectionChange(ByVal Target As Range) 
If Target.Row >= 2 And Target.Column = 2 Then 
Target = 100 
End If 
End Sub 

If ... Then ... End If 这是我们学的这一个逻辑判断语句。 
Target.Row >= 2，指的是鼠标选定的单元格的行大于或等于 2。 
Target.Column = 2 ，指的是鼠标选定的单元格的栏等于 2。 
If Target.Row >= 2 And Target.Column = 2 Then 指的是只有在Target.Row >= 

2及Target.Column = 2二个条件成立时。 
就是 (Target.Row >= 2) 为True及(Target.Column = 2)为True时，才执行下面的 

程序 Target=100， 
也就是 B 栏第二行及以下行用鼠标被点选时，才会被输入100，其它单元格则不被输 

入数据。 

VBALesson5 程序说明： 
比较 Worksheet_SelectionChange() 与用按钮 CommandButton1_Click() 来执行 

程序二者的方法与写法有何不同。 
Worksheet_SelectionChange()事件 
Private Sub Worksheet_SelectionChange(ByVal Target As Range) 
If Target.Row >= 2 And Target.Column = 2 Then 
Target = 100 
End If 
End Sub 

按鈕 CommandButton1_Click() 
Private Sub CommandButton1_Click() 
If ActiveCell.Row >= 2 And ActiveCell.Column >= 3 Then 
ActiveCell = 100 
End If 
End Sub 

二者执行方法最大的地方，在于 Worksheet_SelectionChange() 是自动的，你不用 

了解他是怎么完成工作的。 
按钮 CommandButton1_Click() 是人工的，比 SelectionChange()多一道手续， 

就是要去按那接钮，程序才会执行。 
SelectionChange() 有一个参数 Target 可用；CommandButton1_Click ()没有。 
所以我们要用 ActiveCell 内定函数来取代Target，ActiveCell 与 Target最大的 

不同点他只能指定一个单元格。 
就是你选取多个单元格也只有最上面的单元格会加上数据；用 Selection 取代 

ActiveCell， 用法就跟 Target 一样了。 

VBALesson 6 程序说明： 
完整的 If...Then ┅ End 逻辑判断式。 
Private Sub Worksheet_SelectionChange(ByVal Target As Range) 
If Target.Row >= 2 And Target.Column = 2 Then 
Target = 200 
ElseIf Target.Row >= 2 And Target.Column = 3 Then 
Target = 300 
ElseIf Target.Row >= 2 And Target.Column = 2 Then 
Target = 400 
Else 
Target = 500 
End If 
End Sub 

这是个完整的 If 逻辑判断式，意思是说，假如 If 後的判断式条件成立的话，就 

执行第二条程序，否则假如 ElseIf 後的判断式条件成立的话，就执行第四条程序 

，否则假如另一个 ElseIf 後的判断式条件成立的话，就执行第六条程序。 
Else 的意思是说，假如以上条件都不成立的话，就执行第八条程序。 
他的执行方式是假如 IF 的条件成立的话，就不执行其它ElseIf 及Else 的逻辑判 

断式，假如 If 後的条件不成立的话才会执行 ElseIf 或 Else 逻辑判断式。第二 

个 ElseIf後的条件因为与 IF 後的条件一样，所以这个判断式後面的 Target=400 

将是永远无法执行到的程序。 

VBALesson 7 程序说明∶我们为什麽要用变数。 

Private Sub Worksheet_SelectionChange(ByVal Target As Range) 
Dim i , j As Integer 
Dim k As Range 
i = Target.Row 
j = Target.Column 
Set k = Target 
If i >= 2 And j = 2 Then 
k = 200 
ElseIf i >= 2 And j = 3 Then 
k = 300 
ElseIf i >= 2 And j = 4 Then 
k = 400 
Else 
k = 500 
End If 
End Sub 

跟VBALesson 6比较，程序是不是明朗多了，在前课重复的用 Target.Row， 

Target.Column及Target来写程序是不是有一点烦。用变量的第一个好处大家马上感 

觉得出来，就是可以简化程序。 
使用变量前，你得先宣告变量。宣告变量的方法是在 "Dim " 后面写上变量 " i 

" As 后面接上变量的形态 "Integer"。 
Dim i , j As Integer 就是宣告 i 与 j 为整数变量，这是同时宣告二个变量 

i 与 j 所以要在二个变量间加个 " , "号。 
Dim k As Range 是宣告 k 为范围资料形态，Range这是 Excel 特有的资料形态 

。 
i = Target.Row是把当前单元格的行数，指定给变量 i。 
j = Target.Column 是把当前单元格的栏数，指定给变量 j。 
Set k = Target 是把当前的单元格，指定给变量 k。 
用像 i 与 j 这样简单的变量，在程序的前面你可能还记得 i 或 j 代表着 

什厶。程序写长了，你可能忘记 i 或 j 代表着什厶。所以最好的方法是用比较有 

意义的代号，来为变量命名如 iRow 或 iCol 来取代 i 及 j 。 

VBALesson 8 程序说明∶体会一下Worksheet_Change()事件。 

Private Sub Worksheet_Change(ByVal Target As Range) 
Dim iRow, iCol As Integer 
iRow = Target.Row 
iCol = Target.Column 
If iRow >= 2 And iCol = 2 And Target "" Then 
Application.EnableEvents = False 
Cells(iRow, iCol + 1) = Cells(iRow, iCol) * 2 
Application.EnableEvents = True 
ElseIf iRow >= 2 And iCol = 2 And Target = "" Then 
Cells(iRow, iCol + 1) = "" 
Else 
Cells(iRow, iCol + 1) = "" 
End If 
End Sub 

前几个教程都是用Worksheet_SelectionChange 事件来举例子，大家应该能体会他 

是怎厶一回事了吧。 
这个教程就是要让你来体会什厶是Worksheet_Chang()事件。因为这二个事件在VBA 

都是非常有用的，所以一定要了解。 
简单的说，前者是你鼠标移动到那个单元格，就触发那个事件的执行。後者是要等到 

你点选的单元格，数有了改变才会触发事件的执行。二者执行的时机一前一後。 
Target "" 是代表限定当前的单元格要是有数的，才会执行以下三行的程序。 
Cells(iRow, iCol + 1) = Cells(iRow, iCol) * 2，是你在 B 栏输入数时，C 

栏将可得到 B 栏二倍的数。 
Target = "" 是限定当前的单元格要是没有数的，才会执行以下一行的程序。 
Cells(iRow, iCol + 1) = ""，是把 C 栏的数清成空格。 
Application.EnableEvents = False与Application.EnableEvents = True，这是 

个成双的程序，当你用了前者记得在执行其他程序後要写上後面的程序。它的目的在 

抑制事件连锁执行。简单的说就是，在 B 字段所触发的事件，不愿在其它单元格再 

触发另一个Worksheet_Change()事件。 

VBALesson 9 程序说明∶体会一下Worksheet_Change()事件连锁反应。 

Private Sub Worksheet_Change(ByVal Target As Range) 
Dim iRow As Integer 
iRow = Target.Row 
Application.EnableEvents = False 
Cells(iRow, 3) = Cells(iRow, 3) + Cells(iRow, 2) 
Application.EnableEvents = True 
End Sub 

Private Sub Worksheet_Change(ByVal Target As Range) 
Dim iRow As Integer 
iRow = Target.Row 
'Application.EnableEvents = False 
Cells(iRow, 3) = Cells(iRow, 3) + Cells(iRow, 2) 
'Application.EnableEvents = True 
End Sub 

这个程序的目的是要在 B2 输入新的数时，C2 会将 B2 输入的新数加上 C2 原 

有的数呈现在 C2 上。 
照上面有加上 Application.EnableEvents = False 程序执行当然没问题。 
现在你在 Application.EnableEvents = False 与 Application.EnableEvents = 

True 前加上「 '」看看。 
程序前加上「 '」的目的是要使「 '」之后的文字变成说明文字，程序执行时是会跳 

过说明文字，不执行说明文字的内容。 
程序前加上「 '」符号后，文字会变成绿色。 
执行第二个程序时，你将发现 C2 不会按你所要求的，呈现结果。 
这就是所谓的事件连锁反应。 

请问这个宏该如何写! 
我想运行一个宏,就能在当前工作表B3上填上一条公式;这条公式的结果是所有工作 
表上的B4单元格的和.请问这个宏该如何写.谢谢! 
Sub gg() 
Dim sh As Worksheet, shname$ 
For Each sh In Worksheets 
shname = sh.Name 
ActiveSheet.Range("b3").value = ActiveSheet.Range("b3").value + 

Worksheets(shname).Range("b4") 
Next 
End Sub 

VBA中怎样创建一个名为“table”的新工作表 
通过VBA编程，很容易添加新的工作表，但是新表的名字不知怎样控制，对于新创建 

的工作表，由于其名字并非特定，所以就不好使用所创建的新表了。不知各位有何高 

见。。。。 
Sheets.Add 
ActiveSheet.Name = "table" 

请教：如何用VBA检索表1中A列与表2，3，4，5.....中A列相同的行并把后者整行拷 

贝到表1检索到的行中,谢谢!!!! 
To yxptwq∶用这程序试看看。 
Sub Copy1() 
Dim Row_dn1, Row_dnN, i, j, n As Integer 
Row_dn1 = Sheet1.Range("A65536").End(xlUp).Row 
k = 1: n = 1 
For Each wSheet In ActiveWorkbook.Worksheets 
With wSheet 
If .Name "Sheet1" Then 
Row_dnN = .Range("A65536").End(xlUp).Row 
For i = 2 To Row_dn1 
For j = 2 To Row_dnN 
If .Cells(j, 1) = Sheet1.Cells(i, 1) Then 
.Rows(j & ":" & j).Copy Destination:=Sheet1.Rows(Row_dn1 + 

n & ":" & Row_dn1 + n) 
n = n + 1 
End If 
Next j 
Next i 
End If 
End With 
Next wSheet 
End Sub 

如果要用VBA程式输入密码使用下列程式码 

Sub EnterNewPW() 
'程式说明:利用SendKey输入VBAProject密码 
'注意事项:执行本程式需要在Excel视窗,不能在VBE视窗 
Application.SendKeys "%{F11}", True 'Alt + F11 切换到VBA视窗 
Application.SendKeys "%T", True 'ALT + T 工具(繁体中文是(T)) 
Application.SendKeys "e", True '工具(T)-VBproject属性(E) 
Application.SendKeys "^{TAB}", True 'TAB 键(切换到PAge2 保护页面) 
Application.SendKeys "{+}", True '选取Checkbox方块(锁定专案以供检 

视) 
'({+} 选取, {-} 取消选取) 
Application.SendKeys "{TAB}", True 'TAB 键(跳到第一次输入密码 

Textbox 
myPW = "chijanzen" '假设密码 chijanzen 
Application.SendKeys myPW, True '输入密码 
Application.SendKeys "{TAB}", True 'TAB 键(跳到第二次输入密码 

Textbox 
Application.SendKeys myPW, True '输入密码 
Application.SendKeys "{ENTER}", True '按确定钮(预设值) 
Application.SendKeys "%{F11}", True '返回Excel视窗 
End Sub 

冒泡排序法： 
冒泡排序法之所以成为“冒泡排序”是因为值较小的或是较轻的元素浮到作为继续排 

序的一组数的顶部。 
Sub Macro1() 
Dim i As Integer 
Dim j As Integer 
Dim t as integer 
Static number(1 To 10) As Integer 
For i = 1 To 10 
number(i) = inputbox“输入要排序的数：” 
Next i 

For i = 10To 2 Step -1 
For j = 1 To i – 1 
‘下面进行位置交换 
If number(j) > number(j + 1) Then 
t = number(j + 1) 
number(j + 1) = number(j) 
number(j) = t 
End If 

Next j 
Next i 

For i = 1 To 20 
Print number(i) 
Next i 
End sub 

首先定义一个数组：通过循环录入10个整数，然后用一个二重循环测试前一个数是否 

大于后一个数。如果大于则交换两个数的下标，即交换两个数在数组中的位置，交换 

通过一个变量来进行。 

我先用传统的方法解决这个问题，经过比较，选用了较为简单的和高效的排序方法 
——“快速排序”，具体算法可参考数据结构等有关书籍。对所有数据排序后再合 
并相同数据，合并程序较为简便，我开始时采用了这种方法，但后来发现对于这些 
的数据，先合并后排序速度更快，因为有大量相同的数据。合并是采用“标记”算 
法，具体如下：（设数据已存放在sData()数组中 ，结果存到Queryp()数组， 
Amount是数据个数） 
'把相同元素置 0 
For i = 1 To Amount 
If sData(i) 0 Then 
For j = i ＋ 1 To Amount 

If sData(i) = sData(j) Then sData(j) = 0 
Next j 
End If 
Next i 
'删除相同元素 
Queryp(1) = sData(1) 
k = 1 
For i = 2 To Amount 
If Not (sData(i) = 0) Then 
k = k ＋ 1 
Queryp(k) = sData(i) 
End If 
Next i 
kMax = k 
ReDim Preserve Queryp(kMax) 
虽然这样使得运算速度有所高，但是仍然要进行大量的循环运算，占据了程序大部 
分的运算时间。于是我一直在寻觅一种更为高效的算法。 
功夫不负有心人，在仔细分析数据的特征，比较了多种方案之后，我终于找到了一 
种相当成功的算法，原来要3到4秒的运算缩短到仅需0.1到0.2秒。 
我遇到的数据具有以下特征：①相同数据很多，②最大、最小数之间相差不到3， 
③都是带两位小数的正数。 
针对数据的特征，我采用了以下算法： 
针对数据的特征，我采用了以下算法： 
步骤： 
1． 用一个循环找出整数和小数部分的最大、最小值。小数部分的最大、最小值乘 
以100转为整数。 
2． 定义一个二维数组，下标范围分别是整数和小数部分的最小值到最大值。 
3． 再用一个循环把所有源数据填入刚才定义的二维数组，填写规则是，源数据的 
整数和小数部分分别对应二维数组的两个下标。例如，“13.51"填到“A(13,51)" 
中。 
4． 最后顺向或逆向读取二维数组中的非零数据即可得到从小到大或从大到小排列 
的数据，而且不会含有重复数据。 
用VB 编写的程序如下： 
'＊＊＊＊密集型数据处理＊＊＊＊ 
Dim i As Long, j As Long, k As Long, kMax As Long 
Dim Queryp() As Single 
ReDim Queryp(Amount) 
Dim IntegerPart As Integer, DecimalPart As Integer 
Dim IPmax As Integer, IPmin As Integer 
Dim DPmax As Integer, DPmin As Integer 
Dim DiffDataArray() 
'读取数据 
ReadData 
IPmax = 0: IPmin = 1000 
DPmax = 0: DPmin = 99 

For i = 1 To Amount 
' 找整数和小数部分的最大、最小值 
IntegerPart = Int(sData(i)) 
DecimalPart = (sData(i) － IntegerPart) ＊ 100 
If IntegerPart > IPmax Then 
IPmax = IntegerPart 
ElseIf IntegerPart DPmax Then 
DPmax = DecimalPart 
ElseIf DecimalPart 0 Then 
k = k ＋ 1 
Queryp(k) = DiffDataArray(i, j) 
End If 
Next j 
Next i 
kMax = k 
ReDim Preserve Queryp(kMax) 
该方法对于本人遇到的这种“密集型”数据最为有效，但是如果遇上“稀疏型”数 
据，例如最大、最小值相差几千，甚至上万的数据，就没什么优势了，而且会占用 
较大的内存。 
经过改进，我得到了处理稀疏型数据的高效算法。高效的前提条件同样是源数据具 
有大量相同数据。思路是在前一种方法的基础上增加一个单维数组，用来保存整数 
部分数据，保存过程中用插入法对其进行排序。因为有大量重复数据，要排序的数 
据量相对较少。当从二维数组中读取数据时，用单维数组代入二维数组的第一个下 
标，具体代码下： 
'＊＊＊＊稀疏型数据处理＊＊＊＊ 
Dim i As Long, j As Long, k As Long, kMax As Long 

Dim Queryp() As Single 
ReDim Queryp(Amount) 
Dim IntegerPart As Integer, DecimalPart As Integer 
Dim IPmax As Integer, IPmin As Integer 
Dim DPmax As Integer, DPmin As Integer 
Dim IPArray() As Integer, IPAamount As Integer 
ReDim IPArray(Amount) 
Dim DiffDataArray() 
'读取数据 

ReadData 
IPmax = 0: IPmin = 1000 
DPmax = 0: DPmin = 99 
IPAamount = 0 
For i = 1 To Amount 
'获取整数和小数部分的最大最小值 
IntegerPart = Int(sData(i)) 
DecimalPart = (sData(i) － IntegerPart) ＊ 100 
If IntegerPart > IPmax Then 
IPmax = IntegerPart 
ElseIf IntegerPart DPmax Then 
DPmax = DecimalPart 
ElseIf DecimalPart IPArray(j) Then 
IPAamount = IPAamount ＋ 1 
For k = IPAamount To j ＋ 1 Step －1 
IPArray(k) = IPArray(k － 1) 
Next k 
IPArray(j) = IntegerPart 
Exit For 
ElseIf IntegerPart = IPArray(j) Then 
Exit For 
End If 
Next j 
If j > IPAamount Then 
IPAamount = IPAamount ＋ 1 
IPArray(IPAamount) = IntegerPart 

End If 
Next i 
ReDim DiffDataArray(IPmin To IPmax, DPmin To DPmax) 
'填入数据 
For i = 1 To Amount 
IntegerPart = Int(sData(i)) 
DecimalPart = (sData(i) － IntegerPart) ＊ 100 
DiffDataArray(IntegerPart, DecimalPart) = sData(i) 
Next i 
'提取数据 
k = 0 
For i = 1 To IPAamount 
For j = DPmax To DPmin Step －1 
If DiffDataArray(IPArray(i), j) 0 Then 
k = k ＋ 1 
Queryp(k) = DiffDataArray(IPArray 
（i), j) 
End If 
Next j 
Next i 
kMax = k 
ReDim Preserve Queryp(kMax) 
k 
ReDim Preserve Queryp(kMax) 
具体采用哪种算法，要看数据的性质而定，以下是本人的一些实测数据，仅供参考 
。如果你有更好的方法，可不要忘记和朋友们分享哦。 

自动隐藏表格中无数据的行 
表1 是数据源，经常改变； 
表2 引用表1 中某列有数据的单元格（利用动态位址已实现。） 
由于表1 的改变，表2 的大小随之而变。 
问题：如何实现表2 中没有数据的行（有公式）自动隐藏？谢谢赐教！ 
Sub abc() 
For i = 1 To 300 
If Cells(i, 1).value = "" Then Rows(i).Hidden = True 
Next i 
End Sub 
你写的语句可以解决隐藏的问题，可是如果我执行了它之后，再在表1中增加数据， 

表2不会自动显示有了数据的行。如何修改？ 
将此宏设为自动运行（打开文件时） 
Sub abc() 
For i = 1 To 300 
If Cells(i, 1).value "" Then Rows(i).Hidden = false 
Next i 
End Sub 

用VBA如何自动合并列的内容？ 
用VBA如何自动合并列的内容？ 
To hongjian ： 
Sub MergeTest() 
For i = 3 To 30 
Cells(i, 3) = Cells(i, 1) & Chr(10) & Cells(i, 2) 
Next 
End Sub 

基于VB和EXCEL的报表设计及打印 
　　在现代管理信息系统的开发中，经常涉及到数据信息的分析、加工， 
最终还需把统计结果形成各种形式的报表提供给领导决策参考，或进行外 
部交流。在Visual Basic中制作报表，通常是用数据环境设计器(Data 
Environment Designer)与数据报表设计器(Data Report Designer),或者 
使用第三方产品来完成。但对于大多数习惯于Excel报表的用户而言,用以 
上方法生成的报表在格式和功能等方面往往不能满足他们的要求。 

　　由于Excel具有自己的对象库，在Visual Basic工程中可以加以引用， 
通过对Excel使用OLE自动化，可以创建一些外观整洁的报表，然后打印输 
出。这样实现了Visual Basi应用程序对Excel的控制。本文将针对一个具 
体实例，阐述基于VB和EXCEL的报表设计及打印过程。 

　1）创建Excel对象 
　　Excel对象模型包括了128个不同的对象，从矩形、文本框等简单的对 
象到透视表，图表等复杂的对象。下面简单介绍一下其中最重要，也是用 
得最多的五个对象。 

（1）Application对象 
　　Application对象处于Excel对象层次结构的顶层，表示 Excel自身的 
运行环境。 

（2）Workbook对象 
　　Workbook对象直接地处于Application对象的下层，表示一个Excel工 
作薄文件。 

（3）Worksheet对象 
　　Worksheet对象包含于Workbook对象，表示一个Excel工作表。 

（4）Range对象 
　　Range对象包含于Worksheet对象，表示 Excel工作表中的一个或多个 
单元格。 

（5）Cells对象 
　　Cells对象包含于Worksheet对象，表示Excel工作表中的一个单元格。 
　　如果要启动一个Excel，使用Workbook和Worksheet对象，下面的代码 
启动了Excel并创建了一个新的包含一个工作表的工作薄： 
Dim zsbexcel As Excel.Application 
Set zsbexcel = New Excel.Application 
　　　　zsbexcel.Visible = True 
如要Excel不可见，可使zsbexcel.Visible = False 
　　zsbexcel.SheetsInNewWorkbook = 1 
　　Set zsbworkbook = zsbexcel.Workbooks.Add 

　2）设置单元格和区域值 
　　要设置一张工作表中每个单元格的值，可以使用Worksheet对象的 
Range属性或Cells属性。 
With zsbexcel.ActiveSheet 
　　　　.Cells(1, 2).value = "100" 
　　　　.Cells(2, 2).value = "200" 
　　　　.Cells(3, 2).value = "=SUM(B1:B2)" 
　　　　.Range("A3:A9") = "中国人民解放军" 
　　End With 
　　要设置单元格或区域的字体、边框，可以利用Range对象或Cells对象 
的Borders属性和Font属性： 
　　With objexcel.ActiveSheet.Range("A2:K9").Borders　 '边框设置 
　　　　.Line = xlBorderLine 
　　　　.Weight = xlThin 
　　　　.ColorIndex = 1 
　　End With 
　　With objexcel.ActiveSheet.Range("A3:K9").Font　　'字体设置 
　　　　.Size = 14 
　　　　.Bold = True 
　　　　.Italic = True 
　　　　.ColorIndex = 3 
　　End With 

　　通过对Excel单元格和区域值的各种设置的深入了解,可以创建各种复 
杂、美观、满足需要的、具有自己特点的报表。 

　3）预览及打印 

　　生成所需要的工作表后，就可以对EXCEL发出预览、打印指令了。 

　　zsbexcel.ActiveSheet.PageSetup.Orientation = xlPortrait　　 ' 
　　设置打印方向 
　　zsbexcel.ActiveSheet.PageSetup.PaperSize = xlPaperA4　　　' 
　　设置打印纸的打下 
　　zsbexcel.Caption = "打印预览"　　　　　　　 '设置预览窗口的 
　　标题 
　　zsbexcel.ActiveSheet.PrintPreview　　　　　　'打印预览 
　　zsbexcel.ActiveSheet.PrintOut　　　　　　　　'打印输出 

　　通过打印方向、打印纸张大小的设置，不断进行预览，直到满意为止， 
最终进行打印输出。 

　　为了在退出应用程序后EXCEL不提示用户是否保存已修改的文件,需使 
用如下语句： 

　　zsbexcel.DisplayAlerts = False 
　　zsbexcel.Quit　　　 '退出EXCEL 
　　zsbexcel.DisplayAlerts = True 

　　如此设计的报表打印是通过 EXCEL程序来后台实现的。对于使用者来 
说，根本看不到具体过程，只看到一张张漂亮的报表轻易地被打印出来了。 

　4）具体实例 

　　下面给出一个具体实例，它在window98、Visual Basic 6.0、 
Microsoft Office97的环境下调试通过。 

　　在VB中启动一个新的Standard EXE工程，在“工程”菜单的“引用” 
选项下引用Excel Object Library；然后在Form中添加一个命令按钮 
cmdExcel；最后在窗体中输入如下代码： 

　　Dim zsbexcel As Excel.Application 
　　　　　　Private Sub cmdExcel_Click() 
　　　　　　　　　　Set zsbexcel = New Excel.Application 
　　　zsbexcel.Visible = True 
　　　zsbexcel.SheetsInNewWorkbook = 1 
　　　Set zsbworkbook = zsbexcel.Workbooks.Add 
　　　With zsbexcel.ActiveSheet.Range("A2:C9").Borders　　　'边框设置 
　　　　　　.Line = xlBorderLine 
　　　　　　.Weight = xlThin 
　　　　　　.ColorIndex = 1 
　　　　　　End With 
　　　With zsbexcel.ActiveSheet.Range("A3:C9").Font　　'字体设置 
　　　　　　 .Size = 14 
　　　　　　.Bold = True 
　　　　　　.Italic = True 
　　　　　　.ColorIndex = 3 
　　　End With 
　　zsbexcel.ActiveSheet.Rows.HorizontalAlignment = 
xlVAlignCenter　　　'水平居中 

　　zsbexcel.ActiveSheet.Rows.VerticalAlignment = 
xlVAlignCenter　　　　'垂直居中 

　　With zsbexcel.ActiveSheet 
　　　　.Cells(1, 2).value = "100" 
　　　　.Cells(2, 2).value = "200" 
　　　　.Cells(3, 2).value = "=SUM(B1:B2)" 
　　　　.Cells(1, 3).value = "中国人民解放军" 
　　　　.Range("A3:A9") = "50" 
　　End With 
　zsbexcel.ActiveSheet.PageSetup.Orientation = xlPortrait　　　 ' 
xlLandscape 
　zsbexcel.ActiveSheet.PageSetup.PaperSize = xlPaperA4 
　zsbexcel.ActiveSheet.PrintOut 
　zsbexcel.DisplayAlerts = False 
　zsbexcel.Quit 
　zsbexcel.DisplayAlerts = True 
　Set zsbexcel = Nothing 

提高EXCEL中VBA的效率 

　　方法1：尽量使用VBA原有的属性、方法和Worksheet函数 
　　由于Excel对象多达百多个，对象的属性、方法、事件多不胜数，对于初学者来 

说可能对它们不全部了解，这就产生了编程者经常编写与Excel对象的属性、方法相 

同功能的VBA代码段，而这些代码段的运行效率显然与Excel对象的属性、方法完成 

任务的速度相差甚大。例如用Range的属性CurrentRegion来返回 Range 对象，该对 

象代表当前区。（当前区指以任意空白行及空白列的组合为边界的区域）。同样功能 

的VBA代码需数十行。因此编程前应尽可能多地了解Excel对象的属性、方法。 
　　充分利用Worksheet函数是提高程序运行速度的极度有效的方法。如求平均工资 

的例子：For Each c In Worksheet(1).Range(″A1:A1000″) 
　　 Totalvalue = Totalvalue ＋ c.value 
　　Next 
　　Averagevalue = Totalvalue / Worksheet(1).Range(″ 

A1:A1000″).Rows.Count 
　　而下面代码程序比上面例子快得多： 
　　Averagevalue="/blog/Application.WorksheetFunction.Average(Worksheets 
(1).Range(″A1:A1000″)) 
　　其它函数如Count,Counta,Countif,Match,Lookup等等，都能代替相同功能的 

VBA程序代码，提高程序的运行速度。 

　　方法2：尽量减少使用对象引用，尤其在循环中 
　　每一个Excel对象的属性、方法的调用都需要通过OLE接口的一个或多个调用， 

这些OLE调用都是需要时间的，减少使用对象引用能加快VBA代码的运行。例如 
　　1．使用With语句。 
　　 Workbooks(1).Sheets(1).Range(″A1:A1000″).Font.Name=″Pay″ 
　　 Workbooks(1).Sheets(1).Range(″A1:A1000″).Font.Font 

... 
　　则以下语句比上面的快 
　　With Workbooks(1).Sheets(1).Range(″A1:A1000″).Font 
　　 .Name = ″Pay″ 
　　 .Font = ″Bold″ 
　　 ... 
　　End With 
　　2．使用对象变量。 
　　 如果你发现一个对象引用被多次使用，则你可以将此对象用Set 设置为对象变 

量，以减少对对象的访问。如： 
　　Workbooks(1).Sheets(1).Range(″A1″).value = 100 
　　 Workbooks(1).Sheets(1).Range(″A2″).value = 200 
　　则以下代码比上面的要快： 
　　Set MySheet = Workbooks(1).Sheets(1) 
　　MySheet.Range(″A1″).value = 100 
　　MySheet.Range(″A2″).value = 200 
　　3．在循环中要尽量减少对象的访问。 
　　For k = 1 To 1000 
　　 Sheets(″Sheet1″).Select 
　　 Cells(k,1).value = Cells(1,1).value 
　　Next k 
　　则以下代码比上面的要快： 
　　Set Thevalue = Cells(1,1).value 
　　Sheets(″Sheet1″).Select 
　　For k = 1 To 1000 
　　 Cells(k,1).value = Thevalue 
　Next k 

　　方法3：减少对象的激活和选择 
　　如果你的通过录制宏来学习VBA的，则你的VBA程序里一定充满了对象的激活和选 

择，例如Workbooks(XXX).Activate、Sheets(XXX).Select、Range(XXX).Select等 

,但事实上大多数情况下这些操作不是必需的。例如 
　　Sheets(″Sheet3″).Select 
　　Range(″A1″).value = 100 
　　Range(″A2″).value = 200 
　可改为： 
　　With Sheets(″Sheet3″) 
　　 .Range(″A1″).value = 100 
　　 .Range(″A2″).value = 200 
　　End With 

　　方法4：关闭屏幕更新 
　　如果你的VBA程序前面三条做得比较差，则关闭屏幕更新是提高VBA程序运行速度 

的最有效的方法，缩短运行时间2/3左右。关闭屏幕更新的方法： 
　　Application.ScreenUpdate = False 
　　请不要忘记VBA程序运行结束时再将该值设回来： 
　　Application.ScreenUpdate = True 
　　以上是提高VBA运行效率的比较有效的几种方法 

本示例重复最近用户界面命令。本示例必须放在宏的第一行。 
Application.Repeat 

下例中，变量 counter 代替了行号。此过程将在单元格区域 C1:C20 中循环，将所 

有绝对值小于 0.01 的数字都设置为 0（零）。 
Sub RoundToZero1() 
For Counter = 1 To 20 
Set curCell = Worksheets("Sheet1").Cells(Counter, 3) 
If Abs(curCell.Value) 0 Then 
' Application.ActivePrinter = "\\zdserver2\HP LaserJet 5000 PCL 6 

在 Ne00:" '指定打印机 
ActiveWindow.SelectedSheets.PrintOut Copies:=myPrintNum, 

Collate:=True '设置打印信息,其中Copies:=myPrint为打印份数 
Else 
MsgBox "请输入要打印的份数" 
End If 
ActiveSheet.ShowAllData '全部显示 
ActiveSheet.Protect Password:=641112 ' 保护工作表并设置密码 
Sheets("封面").Select 
Application.ScreenUpdating = True 
End Sub 

Sub 打印余额() 
Application.ScreenUpdating = False 
Sheets("余额表").Select 
Call 重算所有表 
ActiveSheet.Unprotect Password:=641112 '撤消工作表保护并取消密码 
ActiveWindow.ScrollColumn = 10 
Selection.AutoFilter Field:=1, Criteria1:="" 
'以下10行弹出窗口输入打印信息 
Dim myPrintNum As Integer 
Dim myPrompt, myTitle As String 
myPrompt = "请输入要打印的份数" 
myTitle = "打印选取范围" 
myPrintNum = Application.InputBox(myPrompt, myTitle, 4, , , , , 1) 
If myPrintNum 0 Then 
' Application.ActivePrinter = "\\zdserver2\HP LaserJet 5000 PCL 6 在 

Ne00:" ' '指定打印机 
ActiveWindow.SelectedSheets.PrintOut Copies:=myPrintNum, 

Collate:=True '设置打印信息,其中Copies:=myPrint为打印份数 
Else 
MsgBox "请输入要打印的份数" 
End If 
ActiveSheet.ShowAllData '全部显示 
ActiveSheet.Protect Password:=641112 ' 保护工作表并设置密码 
Sheets("封面").Select 
Application.ScreenUpdating = True 
End Sub 

Sub 备份() 
Dim y '变量声明-需保存工作表的路径和名称 
[M1] = ActiveWorkbook.FullName '单元格M1=当前工作簿的路径和名称 
y = cells(1, 14) 'Y=单元格N1的值,即计算后的需保存工作簿的 

路径和名称 
Worksheets("封面").UsedRange.Columns("M:N").Calculate '计算指定 

区域 
ActiveWorkbook.SaveCopyAs y '备份到指定路么Y 
End Sub 

Sub 重算活动表() 
With Application 
.Calculation = xlManual 
.MaxChange = 0.001 
End With 
ActiveWorkbook.PrecisionAsDisplayed = True 
ActiveWindow.DisplayZeros = True 
ActiveSheet.Calculate 
End Sub 

Sub 重算指定表() 
Attribute 重算指定表.VB_ProcData.VB_Invoke_Func = "z\n14" 
Worksheets("银行帐").Calculate 
Worksheets("日报表").Calculate 
End Sub 

单元格数据改变引起计算激活过程 
Private Sub Worksheet_Change(ByVal Target As Range) 
Dim irow, icol As Integer 
irow = Target.Row '变量行irow 
icol = Target.Column '变量列icol 
If irow > 6 And icol = 3 And cells(irow, 3) >= cells(irow - 1, 3) 

Then '>大于6行,并且第3列,当本行 3列>2行3列