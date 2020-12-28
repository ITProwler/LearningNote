# HTML中文乱码

前端页面出现中文乱码是因为文件的编码和浏览器的编码不同，大部分浏览器的编码都是UTF-8（因为既可以显示中文也可以显示其它国家的语言，不会乱码），所以一般在head头部添加以下代码来解决乱码问题：

    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
*<meta>元素提供与页面有关的元信息（meta-information）*
