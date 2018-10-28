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
庆祝一下,一注过了.

天天上okok网站查看消息,
等了好几天,终于在年前等到成绩发布的消息.

心里特别激动,打开那熟悉的建设部的网站.

输入自己的身份证,过了一秒钟,那一秒钟真是思绪万千,不懂的是喜是恢忧,还是紧张.

过一秒钟,看到自己以62分过了的成绩,那时的心情真是无法形容.

然后告诉老婆,老婆比我还要高兴.

然后就是一个电话一个电话的打,告诉我的那些好亲朋好友们.分享我那点范进式的喜阅.

最后祝大家新年快乐.