### 安装依赖

```shell
pip install wheel twine
```

### 打包

```shell
python setup.py sdist bdist_wheel
```

### 其它格式打包

```shell
python setup.py bdist_wininst  # 生成windows .exe 可执行文件
python setup.py bdist_rpm  # 实现linux rpm 包的构建
```

### 打包检查

```shell
python setup.py check
```

### 上传至测试PyPi

```shell
twine upload --repository testpypi dist/*
```

### 上传至PyPi

```shell
twine upload dist/*
```

