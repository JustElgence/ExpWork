迭代转换



```
{
    "version": "0.2.0",
    "configurations": [
        {
            "python": "/home/zdliu/anaconda3/envs/py37/bin/python3",  # 指定python解释器
            "name": "Python: train",
            "type": "python",
            "request": "launch",
            "program": "/home/axjia/train.py",
            "console": "integratedTerminal",
            "env": {"CUDA_VISIBLE_DEVICES":"0,1"},   # 指定显卡
            "args": ["--train_dir", "./input/train_data",   # 命令行参数
                "--dev_dir", "./input/valid_data",
 
            ],
            "justMyCode": false   # 调试封装包里面的代码，可以在里面打断点
        }
    ]
}
```

点操作符用于结构体变量，而箭头操作符用于结构体指针。尝试在指针上使用点操作符或者在非指针上使用箭头操作符都会导致编译错误。

链表头结点位置很重要
