使用socket建立TCP连接

	import socket
	s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)	# 参数代表IPV4,TCP
    s.connect(('127.0.0.1', 5000))	# 服务器IP、端口号