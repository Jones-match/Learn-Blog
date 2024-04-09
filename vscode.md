# FileNotFoundError: [Errno 2] No such file or directory: 'data/ind.cora.x'

**把main.py的上级目录打开作为项目**了，导致程序执行的时候是从上级目录开始查找所给路径，自然缺少当前目录的文件夹名，自然会报错。



