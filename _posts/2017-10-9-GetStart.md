## Geting Started ##
scikit-image是一个工作在numpy数组上的python图像处理模块，这个模块通过import skimage导入：

	import skimage

skimage大部分的功能都在子模块中：

    {% highlight python %}
	from skimage import data
    camera = data.camera()
    # data.camera()是一张内置的图片，以二维数组的方式读取出来
    {%endhighlight %}
    
子模块和功能清单可以在网页上的API reference中找到。

在scikit-image中，图片被表示为numpy数组，例如，灰度图表示为2D数组。
    
	>>> type(camera)
    <type 'numpy.ndarray'>
    >>> camera.shape
    (512, 512)
    
