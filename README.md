StealPic
========

主要作用是用来突破图片的防盗链


部署在Django的站点中也是如此简单。修改如下几点

添加urls.py 
url(r'^picture/(?P<url>.*)$', get_pic, name='get_pic'),
在views中添加调用函数

from antipic.antipic import GetPic
def get_pic(request, url):
  url = url[4:]
  url = urllib.urldecode(url)
  print url
  getpic = GetPic(url)
  req = getpic.get_pic()
  pic = req.read()
  return HttpResponse(pic)

在模板中调用即可，例如原本代码如下 /<img src='http://www.baidu.com/123.jpg'>

在模板中修改为， /<img src='/picture/url=www.baidu.com/123.jpg'>

这样即可以突破“此图片仅能用于百度”等图片防盗链的问题了。

<img src="javascript:alert(1)" onerror=alert(1)>
