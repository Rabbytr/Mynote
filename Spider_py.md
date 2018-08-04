## requests库
* #### response基本属性
```
import requests
r = requests.get(url)
r.url #查看r所对应的url
r.status_code #查看对应http返回状态码
r.encoding #查看返回内容字符集
r.text #查看返回的内容，会根据响应的头的字符集编码做动态调整
r.content #以字节的方式响应内容，如img类型的字节流
r.json() #内置的JSON解码器
r.headers #查看以一个Python字典形式展示的服务器响应头，根据 RFC 2616,TTP头部是大小写不敏感的
r.request.headers #查看请求头
r.headers.get('content-type') #获取content-type对应的值
r.cookies['example_cookie_name']查看cookies信息，注意写法，是key value形式
r.history #查看请求历史
```
* #### 请求超时设置
```
#仅对连接过程有效，与响应体的下载无关
requests.get(url, timeout=0.001)
```
* #### 传递数据
```
r = requests.post(url, data = {'key':'value'})
payload = {'key1': 'value1', 'key2': 'value2'}
r = requests.get(url, params=payload)
```
* #### 设置头请求
```
headers = {'user-agent': 'my-app/0.0.1'}
r = requests.get(url, headers=headers)
```
* #### Cookie
```
r = requests.get(url)
r.cookies['example_cookie_name'] # 获得cookie
cookies = dict(cookies_are='working')
r = requests.get(url, cookies=cookies) # 带cookie请求
```

## BeautifulSoup
* #### 生成对象
```
soup = BeautifulSoup(html_sample, 'html.parser')#html.parser是python的内置标准库用来解析html代码
```
* #### 获得标签
```
soup.select('a')
```
