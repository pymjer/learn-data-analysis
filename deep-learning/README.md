# 深度学习
深度学习算法练习，所有练习的教程都是基于fastai官方课程[Practical Deep Learning](https://course.fast.ai/)

课程资源
- fastbook: [Github](https://github.com/fastai/fastbook)
- 第一部分: [Github](https://github.com/fastai/course22)
- 第二部分: [Github](https://github.com/fastai/course22p2)

## 工具库
fastai
```sh
conda install -c fastchan fastai
```

## 调试技巧
[python pdb tutorial](https://realpython.com/python-debugging-pdb/)
在vscode中可以直接调试，不需要用pdb这些命令

导入调试包，设置端点
```
import pdb; pdb.set_trace()
```
常用命令
- h 查看帮助
- p 打印变量，如果变量名称和命令不同，也可以直接输入变量名称查看, 可以用逗号分隔直接查看多个变量
- c 下一个断点
- n 下一行
- w where, 查看短点的堆栈

## 说明
代码中的大文件使用[git-lfs](https://git-lfs.com/)进行提交