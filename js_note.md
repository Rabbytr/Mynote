## 一些JS小坑
* #### 获取到后台字符串数据比较时，记得Trim()

## 获得Cookie
```
function getCookie(cookie_name)
{
    var cookies = document.cookie;
    var cookie_pos = cookies.indexOf(cookie_name);
    if (cookie_pos != -1)
    {
        cookie_pos += cookie_name.length + 1;
        var cookie_end = cookies.indexOf(";", cookie_pos);
        if (cookie_end == -1)
        {
            cookie_end = cookies.length;
        }
        var value = unescape(cookies.substring(cookie_pos, cookie_end)).trim();
        return value;
    }
    return null;
}
```

### 验证输入
```
$("#idinput").blur(function(){
  var value = $(this).val();
  if(!value)return;
  else if(!value.match(/\d{11}/)){
  }
});
```
