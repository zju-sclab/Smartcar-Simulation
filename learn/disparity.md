# Disparity
![stereo_cam](/assets/stereo_cam.jpeg)
## 1.什么是视差(Disparity)和视差图(Disparity)?
先做个实验，把手指放在眼前，然后闭上右眼，然后迅速睁开右眼同时闭上左眼，你会发现手指在左眼和右眼中的位置是不同的，但手指明明在同一个位置没动啊。恩，体会一下视差。对，离的越近的物体，视差越大。这样说视差还是不够精确，得用数学描述一下。

假设我们有个双目相机，两个相机绝对并排放着，抽象一下，就是下面这个样子：
![stereo](/assets/stereo.png)
其中$P$就是刚才的手指头，$O_{R}$和$O_{T}$就是视网膜，$B$是左右眼的距离，学术名称叫基线(Baseline)，$Z$是手指头离视网膜的距离，$f$是焦距；粉色的线就是左眼的图像和右眼的图像；那么$X_{R}$是手指头在左眼的图像的位置，$X_{T}$就是在右眼图像的位置。比喻完了，改用数学的语言描述了。

看过两个课件，从不同的角度求得公式，先看第一个：
### 1.三角形原理
非常重要的一点：**图中的B长度等于左眼平面(左粉色线)最左边到右眼平面(右粉色线)最左边线长度**。然后，剩下就很好理解了，三角形比一下就好了：

$$
\frac{B}{Z}=\frac{(B+x_{T})-x_{R}}{Z-f}
$$

$$
Z=\frac{B\cdot f}{x_{R}-x_{T}}=\frac{B\cdot f}{d}
$$

其中，视差就是$d=x_{R}-x_{T}$

可以看到，视差和深度$Z$正好是反的。

### 2.投影关系得到
>注意，两个方法的下标有些出入，在上面$R$和$T$分别指Reference和Target；在这里下面$l$和$r$指的就是left和right了。

>**一般，都是以左摄像头的光心作为坐标系的原点，这个还有待验证。**

![cse486](/assets/cse486_stereo_1.png)
![cse486](/assets/cse486_stereo_2.png)
![cse486](/assets/cse486_stereo_3.png)
![cse486](/assets/cse486_stereo_4.png)
![cse486](/assets/cse486_stereo_5.png)
![cse486](/assets/cse486_stereo_6.png)
### 那什么是视差图呢？
知道了视差的公式，我就能求出来（以左摄像头图像为例）每个像素点的视差值，要注意**单位是像素**。
知道了视差图，自然也就知道深度图了。
## 2.计算视差图的那些方法