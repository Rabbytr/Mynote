## Pytorch

#### NET

##### RNN

调用方式有torch.nn.**RNNCell**()，torch.nn.**RNN**()

RNNCell只接受**单步输入**且必须**显式传入**隐藏状态

RNN可以接受**序列输入**且默认一个**全零**的隐藏状态

###### 内部

$$ h_t=tanh(w_{ih} *x_t+b_{ih}+w_{hh}* h_{t-1}+b_{hh}) $$

$x_t$是上一层时刻$t$的隐状态，或者是第一层在时刻$t$的输入。如果`nonlinearity='relu'`,那么将使用`relu`代替`tanh`作为激活函数

###### 参数说明

- input_size – 输入`x`的特征数量。
- hidden_size – 隐层的特征数量。
- num_layers – RNN的层数。
- nonlinearity – 指定非线性函数使用`tanh`还是`relu`。默认是`tanh`。
- bias – 如果是`False`，那么RNN层就不会使用偏置权重 $b_ih$和$b_hh$,默认是`True`
- batch_first – `True`的话，则输入的shape应该是[batch_size, seq_len, feature],输出也是这样。
- dropout – 如果值非零，那么除了最后一层外，其它层的输出都会套上一个`dropout`层。
- bidirectional – 如果`True`，将会变成一个双向`RNN`，默认为`False`。

`RNN`的输入： **(input, h_0)** - input (seq_len, batch, input_size)

`RNN`的输出： **(output, h_n)**

- output (seq_len, batch, hidden_size * num_directions): 保存着`RNN`最后一层的输出特征。如果输入是被填充过的序列，那么输出也是被填充的序列。
- h_n (num_layers * num_directions, batch, hidden_size): 保存着最后一个时刻隐状态。

##### LSTM

`LSTM`输入: input, (h_0, c_0)

- input (seq_len, batch, input_size): 包含输入序列特征的`Tensor`。
- h_0 (num_layers * num_directions, batch, hidden_size):保存着`batch`中每个元素的初始化隐状态的`Tensor`
- c_0 (num_layers * num_directions, batch, hidden_size): 保存着`batch`中每个元素的初始化细胞状态的`Tensor`

`LSTM`输出 output, (h_n, c_n)

- output (seq_len, batch, hidden_size * num_directions): 保存`RNN`最后一层的输出的`Tensor`。
- h_n (num_layers * num_directions, batch, hidden_size): `Tensor`，保存着`RNN`最后一个时间步的隐状态。
- c_n (num_layers * num_directions, batch, hidden_size): `Tensor`，保存着`RNN`最后一个时间步的细胞状态。

##### GRU

输入输出与传统RNN基本类似

##### CNN(Conv2d)

定义：**torch.nn.Conv2d**(in_channels, out_channels, kernel_size, stride=1, padding=0, dilation=1, groups=1, bias=True)

 输入的尺度是(batch, in_channels,H,W)

输出尺度(batch,out_channels,H_out,W_out)

#### Torch

**Torch.cat**(inputs, dimension=0)->Tensor

在给定维度上对输入的张量序列`seq` 进行连接操作

```python
>>> x = torch.randn(2, 3)
>>> x

 0.5983 -0.0341  2.4918
 1.5981 -0.5265 -0.8735
[torch.FloatTensor of size 2x3]

>>> torch.cat((x, x, x), 0)

 0.5983 -0.0341  2.4918
 1.5981 -0.5265 -0.8735
 0.5983 -0.0341  2.4918
 1.5981 -0.5265 -0.8735
 0.5983 -0.0341  2.4918
 1.5981 -0.5265 -0.8735
[torch.FloatTensor of size 6x3]

>>> torch.cat((x, x, x), 1)

 0.5983 -0.0341  2.4918  0.5983 -0.0341  2.4918  0.5983 -0.0341  2.4918
 1.5981 -0.5265 -0.8735  1.5981 -0.5265 -0.8735  1.5981 -0.5265 -0.8735
[torch.FloatTensor of size 2x9]
```

**Tips**: *合并后增加的是dim的维度*

#### Tensor

**Tensor.repeat(*sizes)**

 ***sizes** (*torch.Size ot int...*)-沿着每一维重复的次数

```python
>>> x
tensor([1., 2., 3.])
>>> x.repeat(1,2)
tensor([[1., 2., 3., 1., 2., 3.]])
>>> x.repeat(2,2)
tensor([[1., 2., 3., 1., 2., 3.],
        [1., 2., 3., 1., 2., 3.]])
```



**Tensor.squeeze**(*input, dim=None, out=None*)

将输入张量形状中的`1` 去除并返回。 如果输入是形如(A×1×B×1×C×1×D)，那么输出形状就为： (A×B×C×D)

> 注意： 返回张量与输入张量共享内存，所以改变其中一个的内容会改变另一个

**torch.unsqueeze**(*input, dim, out=None*)

返回一个新的张量，对输入的制定位置插入维度 1

如果`dim`为负，则将会被转化dim+input.dim()+1

```python
>>> x
tensor([1., 2., 3.])
>>> x.unsqueeze(0)
tensor([[1., 2., 3.]])
>>> x.unsqueeze(1)
tensor([[1.],
        [2.],
        [3.]])
```

