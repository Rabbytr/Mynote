# Tensorflow
* #### 保存模型
```
sess = tf.Session()
saver = tf.train.Saver()
saver.save(sess, "./tmp/model.ckpt")
```
* #### 恢复模型
```
sess = tf.Session()
saver = tf.train.Saver()
saver.restore(sess, "./tmp/model.ckpt")
```
