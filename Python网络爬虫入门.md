# 网络爬虫入门

## 网页基础

### 网页组成

+ 网页是由 HTML 、 CSS 、JavaScript 组成的。HTML 是用来搭建整个网页的骨架；CSS 是为了让整个页面更好看，包括我们看到的颜色，每个模块的大小、位置等都是由 CSS 来控制的；JavaScript 是用来让整个网页“动起来”，这个动起来有两层意思，一层是网页的数据动态交互，还有一层是真正的动，比如我们都见过一些网页上的动画，一般都是由 JavaScript 配合 CSS 来完成的。

### 直观展示

+ 我们可以打开浏览器，随便访问一个网站，点击F12 开发者工具。即可看到网页代码。

### 代码分析

+ 在选项 Elements 中可以看到网页的源代码，这里展示的是 HTML 代码。

+ 不同类型的文字通过不同类型的标签来表示，如图片用 <img> 标签表示，视频用 <video> 标签表示，段落用 <p> 标签表示，它们之间的布局又常通过布局标签 <div> 嵌套组合而成，各种标签通过不同的排列和嵌套才形成了网页的框架。

+ 在Style 标签页中，显示的就是当前选中的 HTML 代码标签的 CSS 层叠样式。

## 网页结构

+ 整个 HTML 文档一般分为 head 和 body 两个部分，在 head 头中，我们一般会指定当前的编码格式为 UTF-8 ，并且使用 title 来定义网页的标题，这个会显示在浏览器的标签上面。
+ body 中的内容一般为整个 html 文档的正文，html的标签由<h1>到<h6>六个标签构成，字体由大到小递减，换行标签为<br>，链接使用<a>来创建，herf属性包含链接的URL地址，比如<a href="http://www.baidu.com" >就是一个指向百度的链接。

## 检查网页

| 开发者模式  |                                                              |
| ----------- | ------------------------------------------------------------ |
| Elements    | 允许用户从浏览器的角度来观察网页，用户可以借此看到浏览器渲染页面所需要的HTML、CSS和DOM（Document Object Model）对象。 |
| Network     | 可以看到网页向服务气请求了哪些资源、资源的大小以及加载资源的相关信息。此外，还可以查看HTTP的请求头、返回内容等。 |
| Source      | 即源代码面板，主要用来调试JavaScript。                       |
| Console     | 即控制台面板，可以显示各种警告与错误信息。在开发期间，可以使用控制台面板记录诊断信息，或者使用它作为shell在页面上与JavaScript交互。 |
| Performance | 使用这个模块可以记录和查看网站生命周期内发生的各种事情来提高页面运行时的性能。 |
| Memory      | 这个面板可以提供比Performance更多的信息，比如跟踪内存泄漏。  |
| Application | 检查加载的所有资源。                                         |
| Security    | 即安全面板，可以用来处理证书问题等。                         |

## 爬取翻译

```python
import hashlib
import json
import requests

class fy_spider(object):

    def __init__(self,query_str):
        self.query_str = query_str#翻译内容
        #t = c()("6key_cibaifanyicjbysdlove1").toString().substring(0, 16);
        #        return g("/index.php?c=trans&m=copyevent&client=6&auth_user=key_ciba&sign=".concat(t)
        #初始翻译路径
        sign = (hashlib.md5(("6key_cibaifanyicjbysdlove1" + self.query_str).encode('utf-8')).hexdigest())[0:16]#找到生成sign的方法
        url = 'https://ifanyi.iciba.com/index.php?c=trans&m=fy&client=6&auth_user=key_ciba'
        self.url = url + '&sign=' + sign
        self.headers = {
            "User Agent": "Mozilla / 5.0(Windows NT 10.0;WOW64) AppleWebKit / 537.36(KHTML, likeGecko) Chrome / 78.0.3904.108Safari / 537.36"
        }#请求头 模拟浏览器
        self.data = self.get_data()

    def get_data(self):#获取请求体数据
        data = {
            'from': 'auto',
            'to': 'auto',
            'q': self.query_str
        }
        return data

    def get_data_fromurl(self):#发起请求获取响应数据
        response = requests.post(self.url, headers = self.headers,data = self.data)
        return response.content.decode()

    #{"status":1,"content":{"from":"en","to":"zh","out":"hello","vendor":"ciba","err_no":0,"ttsLan":8}}
    def parse_data(self, json_str):#提取json中的数据
        dict_data = json.loads(json_str)
        result = dict_data['content']['out']
        print('{}翻译后的结果是：{}'.format(self.query_str, result))



    def run(self):
        json_str = self.get_data_fromurl()
        self.parse_data(json_str)
if __name__ == '__main__':
    query_str = input("请输入要翻译的内容：")
    spider = fy_spider(query_str)
    spider.run()
```

