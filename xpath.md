

双斜杠 (`//`) 表示从当前节点开始的任意深度的后代

点符号 (`.`) 表示当前节点

bool(imgs) 将结果转换为布尔值，如果 imgs 列表非空，则返回 True，表示至少有一个 <img> 标签被找到；如果 imgs 列表为空，则返回 False





在 `lxml` 中，`Element` 对象的 `.text` 属性返回的是紧跟在元素起始标签后的文本。如果一个元素没有任何直接跟在起始标签后的文本，那么 `.text` 将返回 `None`。





str.replace(old, new)