flags = tf.app.flags  用变量flags 来处理和解析命令行参数

FLAGS = flags.FLAGS 定义一个全局对象FLAGS, 使用flags 来定义参数后，可以在程序的其他部分使用FLAGS 来访问参数

flags.DEFINE_string("name", "默认值", "备注") 定义一个字符串类型的参数，其默认值写在第2 个位置

