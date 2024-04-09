

# 省略号

| 代码 | 效果 | 意义 |
| :--- | :--- | ---- |
|\cdots| ⋯ |	横向|
|\vdots| ⋮ |	竖向|
|\ddots| ⋱ |	对角线方向|
|x,y,\ldots,z|	x , y , … , z	|跟文本底线对齐|



反向省略号：

https://blog.csdn.net/m0_37203420/article/details/112250713

采用对象旋转的命令来操作对角线方向的省略号旋转从而实现反斜对角方向的省略号。

先要使用usepackage{rotating}导入旋转包，旋转命令格式\begin{command}{x}，这里的{command}有三个命令选项： sideways, turn, rotate。{x}是用户自己定义的旋转角度。



```latex
\documentclass{article}


\usepackage{rotating}         %用于旋转对象（旋转包）

\begin{document}

$\ddots$\qquad
\begin{sideways}$\ddots$\end{sideways}\qquad
\begin{turn}{90}$\ddots$\end{turn}\qquad\qquad
\begin{rotate}{90}$\ddots$\end{rotate}



\end{document}

```



# 数学符号

| 表示 | 代码               |
| ---- | ------------------ |
| 矩阵 | X                  |
| 向量 | \boldsymbol{y}     |
| 范式 | \left \| \right \| |
| 下标 | _{}                |
| 上标 | ^{}                |
| 偏导 | \partial {y}       |
|      |                    |

# 求和

|        |                           |
| ------ | ------------------------- |
| 在上下 | \sum_{x}^{y}              |
| 在左右 | {\textstyle \sum_{x}^{y}} |
| 没有   | \sum x                    |



# 字符上的加线

| 加^号    | \hat{x}          |
| -------- | ---------------- |
| 加横线   | \overline{x}     |
| 加宽^    | \widehat{x}      |
| 加波浪线 | \widetilde{x}    |
| 加一个点 | \dot{x}          |
| 加两个点 | \ddot{x}         |
|          | 最多可以加4 个点 |



