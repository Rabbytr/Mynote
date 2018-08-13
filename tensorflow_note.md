### 启动会话
```
sess = tf.Session()
# 初始化变量
init = tf.global_variables_initializer()
sess.run(init)

sess.close()
```

### 定义tensor
```
# 定义常量
a = tf.constant(tensor)
# 定义变量
w = tf.Variable(tensor)
# 输入占位符
x = tf.placeholder(shape=[2,3],dtype=tf.float32)
```

### 张量运算
```
tf.matmul(a,b) # 矩阵乘法
tf.add(a,b)    # 加法
```

### 训练
```
optimizer = tf.train.AdamOptimizer(1)
train_step = opt.minimize(loss)
for step in range(max_steps):
    sess.run(train_step,feed_dict=data)
```

### 执行运算
```
sess.run(var,feed_dict=data)
```

### 模型的保存和恢复
##### 模型保存
```
saver = tf.train.Saver()
saver.save(sess, "./tmp/model.ckpt")
```
> Note: There is not a physical file called /tmp/model.ckpt. It is the prefix of filenames created for the checkpoint. Users only interact with the prefix instead of physical checkpoint files.
##### 模型恢复
```
saver = tf.train.Saver()
saver.restore(sess, "./tmp/model.ckpt")
```
> Note: 可将图定义在一个专门的类Network中,方便模型的恢复
```
class Network():
    ...
    构建图
    ...
from ? import Network
net = Network()
sess = tf.Session()
saver = tf.train.Saver()
saver.restore(sess, "./tmp/model.ckpt")
sess.run(net.Variables)
```
