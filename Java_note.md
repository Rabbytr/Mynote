### 对数组逆排序
```
int[] rev_a = Arrays.stream(a).boxed().sorted((o1,o2)->o2-o1).mapToInt(i->i).toArray();
```
### 对字符串逆排序
```
String r = s.chars().boxed().sorted((o1,o2)->o2-o1).mapToInt(i->i).collect(
    StringBuilder::new,
    (sb, i) -> sb.append((char)i),
    StringBuilder::append
    ).toString();
```
### 实现toggle
```
boolean toggle = false;
for(int i:arr){
  // java赋值语句返回所赋的值
  if(toggle = !toggle){
    // do something
  }else{
    // do toggle thing
  }
}
```
