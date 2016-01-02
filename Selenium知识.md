##Selenium相关概念及知识
* **Selenium**是Web自动化测试工具集，包括IDE,Grid，RC（selenium 1.0），WebDriver（selenium 2.0）等。

* **Selenium IDE**是firefox浏览器的一个插件。提供简单的脚本录制，编辑与回放功能。

* **Selenium Grid**是用来对测试脚本做分布式处理。现在已经集成到selenium server中了。

* **RC**和**WebDriver**更多应该把它看成一套规范，在这套规范里定义客户端与浏览器交互的协议

###WebDriver是什么？
**WebDriver**其实就是一层基础的协议规范。WebDriver的API（接口规范参考链接[click here](http://www.w3.org/TR/2013/WD-webdriver-20130117/)。

例如：我们需要提供一个元素id的定位方法。

python的WebDriver模块具体实现为：

```python
from selenium import webdriver   #导入python版的selenium（webdriver）
find_element_by_id("XX")         #id定位方法

```

###WebDriver如何组织和执行用例？
**WebDriver**不会组织和执行用例，而是由编译语言的单元测试框架去完成的，这些框架负责把写好这些操作页面元素的方法（用例）组织起来并执行并输入测试结果。如**java**的**junit**和**testing**单元测试框架，**python**的**unittest**单元测试框架。

###Selenium RC和WebDriver什么关系？

**RC**和**Webdriver**类似，都可以看做是一套操作Web页面的规范，只是它们的工作原理不一样。

**selenium RC**在浏览器中运行**JavaScript翻译器来翻译和执行selenese命令（selenese是selenium的命令集合）。

**WebDriver**通过原生浏览器支持或者浏览器扩展直接控制浏览器。**WebDriver**针对各个浏览器而开发，取代了嵌入到被测Web应用中的JavaScript。与浏览器的紧密集成支持创建更高级的测试，避免了JavaScript安全模型导致的限制。除了来自浏览器厂商的支持，**WebDriver**还利用操作系统级得调用模拟用户输入。

###selenium如何做移动端测试呢？
以**python**为例：

```python
from selenium import webdriver
driver = webdriver.Chrome() #获取浏览器驱动，拿到浏览器驱动
driver才能操作浏览器所找的页面上的元素
```
把驱动展开式这样的：

```python
from selenium import webdriver
driver = webdriver.Remote(
                       command_execute='http://127.0.0.1:444/wd/hub',
                       desired_capabilities={'platform':'ANY','browserName':chrome,
                       'version':'','javascriptEnabled':True})
                       
```

驱动里面包含了一些参数，代理服务器（URL），平台，浏览器，浏览器版本等。


###移动端的自动化测试工具Appium
从本质上来讲，**Appium**同样继承了**WebDriver API**的接口规范，**Appium**也支持多种编程语言。以**Python**为例，在真机上安装app简单的实例：

```python

from appium import webdriver #导入python版的appium（webdriver）模块

#定义驱动参数
desired_caps = {}
desired_caps['platformName'] = 'Android'
desired_caps['platformVersion'] = '5.0.1'     #真机的android版本
desired_caps['deviceName'] = '750ABL6ELAKF'   #真机的udid

PATH = lambda p: os.path.abspath(
    os.path.join(os.path.dirname(__file__), p)
)

desired_caps['app'] = PATH('/Users/jzhe/jyxb-release-jyxb_latest.apk')  #apk所在目录

self.driver = webdriver.Remote('http://127.0.0.1:4444/wd/hub', desired_caps)  # 连接appium

```

由于以上操作均为移动端的安卓，驱动的参数里就要指定平台是android，版本信息，设备的udid等信息，获取到取得驱动就可以操作安卓上的APP了。
