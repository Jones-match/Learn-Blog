Servlet 程序是跟在工程路径的后面，而不是端口后面

在xml 中配置时，以/ 开头就是要跟在工程路径的后面

在代码中调用时，就是IDEA 中这个工程中的web 目录



而在jsp 或html标签中（或其他前端中），/ 后会直接跟在端口的后面

此时， 用base 标签可以设置成跟在工程路径后





重定向（response.sendRedirect()) 中的 / 表示的是 端口

请求转发(request.getRequestDispatcher()) 中的 / 表示的是 工程路径

