# 1.原理
用`Artist`对象在画布`canvas`上绘制`Render`图形。
- `matplotlib.backend_bases.FigureCanvas`绘图区，所有的图像都是在绘图区完成的
- `matplotlib.backend_bases.Renderer`渲染器，可以近似理解为画笔，控制如何在FigureCanvas上画图。
- `matplotlib.artist.Artist`具体的图表组件，调用Renderer的接口在Canvas上作图。


# 2. Artist
Artist有两种类型：`primitives`和`containers`。
- `primitive`是基本要素，它包含一些我们要在绘图区作图用到的标准图形对象，如曲线Line2D，文字text，矩形Rectangle，图像image等。
- `container`是容器，即用来装基本要素的地方，包括图形figure、坐标系Axes和坐标轴Axis。

## 2.1 primitives
### [Line2D](https://matplotlib.org/stable/api/_as_gen/matplotlib.lines.Line2D.html)
- `plot`经常用就不举例了。
  - `xdata`:需要绘制的line中点的在x轴上的取值，若忽略，则默认为range(1,len(ydata)+1)
  - `ydata`:需要绘制的line中点的在y轴上的取值
  - `linewidth`:线条的宽度
  - `linestyle`:线型
  - `color`:线条的颜色
  - `marker`:点的标记，详细可参考[markers API](https://matplotlib.org/stable/api/markers_api.html)
  - `markersize`:标记的size
- `errorbar`示例：
  - `xerr`：x轴方向的误差
  - `yerr`：y轴方向的误差
  - `fmt`：点的标记
  - `ecolor`：误差线的颜色
  - `elinewidth`：误差线的宽度
```python
fig = plt.figure()
yerr = np.linspace(0, 0.5, 100)  # 误差范围
x = np.arange(100)
y = 2.5 * np.sin(x / 30 * np.pi)
plt.errorbar(x, y, yerr=yerr, label='both limits (default)', ecolor='r')
plt.show()
```

### `Patch`

#### `Rectangle矩形`：

hist直方图：
  - `x`: 数据集，最终的直方图将对数据集进行统计
  - `bins`: 统计的区间分布
  - `range`: tuple, 显示的区间，range在没有给出bins时生效
  - `density`: bool，默认为false，显示的是频数统计结果，为True则显示频率统计结果，这里需要注意，频率统计结果=区间数目/(总数*区间宽度)，和normed效果一致，官方推荐使用density
  - `histtype`: 可选{'bar', 'barstacked', 'step', 'stepfilled'}之一，默认为bar，推荐使用默认配置，step使用的是梯状，stepfilled则会对梯状内部进行填充，效果与bar类似
  - `align`: 可选{'left', 'mid', 'right'}之一，默认为'mid'，控制柱状图的水平分布，left或者right，会有部分空白区域，推荐使用默认
  - `log`: bool，默认False,即y坐标轴是否选择指数刻度
  - `stacked`: bool，默认为False，是否为堆积状图

bar条形图：
  - `left`：x轴的位置序列，一般采用range函数产生一个序列，但是有时候可以是字符串
  - `heigh`t：y轴的数值序列，也就是柱形图的高度，一般就是我们需要展示的数据；
  - `alpha`：透明度，值越小越透明
  - `width`：为柱形图的宽度，一般这是为0.8即可；
  - `color`或`facecolor`：柱形图填充的颜色；
  - `edgecolor`：图形边缘颜色
  - `label`：解释每个图像代表的含义，这个参数是为legend()函数做铺垫的，表示该次bar的标签

#### `Polygon多边形`

fill是基于x,y坐标的填充。
```python
x = np.linspace(0, 5 * np.pi, 1000)
y = np.sin(x)
plt.fill(x, y, color="g", alpha=0.3)
plt.show()
```

#### `Wedge契形`

pie饼图：
- `x`：契型的形状，一维数组。
- `explode`：如果不是等于None，则是一个len(x)数组，它指定用于偏移每个楔形块的半径的分数。
- `labels`：用于指定每个契型块的标记，取值是列表或为None。
- `colors`：饼图循环使用的颜色序列。如果取值为None，将使用当前活动循环中的颜色。
- `startangle`：饼状图开始的绘制的角度。

```python
labels = 'Frogs', 'Hogs', 'Dogs', 'Logs'
sizes = [25, 20, 44.5, 10.5]
explode = (0.1, 0.1, 0.2, 0)
fig, ax = plt.subplots()
ax.pie(sizes, explode=explode, labels=labels, autopct='%1.1f%%', shadow=True, startangle=90)
ax.axis('equal')  # Equal aspect ratio ensures that pie is drawn as a circle.
plt.show()
```

### `collections`
用来绘制一组对象的集合。
比如`scatter`。

### `images`
用来绘制图像。
比如`imshow`(传入一个gird，如`grid = np.random.rand(4, 5)`)。

## 2.2 containers
### `Figure`
- `figsize`：指定figure的宽和高，单位为英寸；
- `dpi`：参数指定绘图对象的分辨率，即每英寸多少个像素，缺省值为80；
Figure容器包含了图表中的所有元素，要通过`Figure.add_subplot()`、`Figure.add_axes()`来添加元素，通过`Figure.delaxes()`来删除元素。但是你可以迭代或者访问`Figure.axes`中的Axes，然后修改这个Axes的属性。
```python
fig = plt.figure()
ax1 = fig.add_subplot(211)
for ax in fig.axes:
    ax.grid(True)
plt.show()  # 只有一个子图，所以这个循环只会执行一次
```
绘制非均匀子图：
```python
spec = fig.add_gridspec(nrows=2, ncols=5, width_ratios=[1,2,3,4,5], height_ratios=[1,3])  # 2行5列，宽度比例为1:2:3:4:5，高度比例为1:3
# 下面是两种访问子图的方法：
# 通过索引访问子图
ax = fig.add_subplot(spec[0, 0])
# 通过切片访问子图
ax = fig.add_subplot(spec[0, :3])
```
这样可以在一个图上做出散点图与边际分布图的组合。
```python
from matplotlib import gridspec
data = np.random.randn(2, 150)
x, y = data[0], data[1]
# 创建图表
fig = plt.figure(figsize=(8, 8))
gs = gridspec.GridSpec(4, 4, hspace=0.4, wspace=0.4)
# 主散点图
ax_main = fig.add_subplot(gs[1:4, 0:3])
ax_main.scatter(x, y)
ax_main.set_xlabel('X')
ax_main.set_ylabel('Y')
# 上方的直方图
ax_histx = fig.add_subplot(gs[0, 0:3], sharex=ax_main)
ax_histx.hist(x, bins=20, color='blue', alpha=0.7)
ax_histx.axis('off')  # 隐藏轴
# 右侧的直方图
ax_histy = fig.add_subplot(gs[1:4, 3], sharey=ax_main)
ax_histy.hist(y, bins=20, orientation='horizontal', color='blue', alpha=0.7)
ax_histy.axis('off')  # 隐藏轴
plt.show()
```
不过可以使用sns来做：
```python
g = sns.JointGrid(x=x, y=y)
g.plot(sns.scatterplot, sns.histplot)
plt.show()
```

### `Axes`
Artist container：
`ax.xaxis`：XAxis对象的实例，用于处理x轴tick以及label的绘制
`ax.yaxis`：YAxis对象的实例，用于处理y轴tick以及label的绘制

示例：极坐标
绘制玫瑰图：
```python
plt.rcParams['font.sans-serif'] = ['SimSun']  # 设置中文
# 数据
countries = ['韩国', '意大利', '伊朗', '日本', '法国', '德国', '西班牙', '新加坡', '美国', '科威特',
             '巴林', '泰国', '英国', '瑞士', '澳大利亚', '马来西亚', '挪威', '加拿大', '伊拉克', '阿联酋',
             '奥地利', '希腊', '以色列', '黎巴嫩', '埃及', '比利时', '克罗地亚', '阿曼', '格鲁吉亚', '北马其顿']
cases = [4812, 2036, 1501, 980, 191, 180, 128, 106, 100, 56,
         47, 42, 40, 32, 29, 25, 24, 22, 20, 19, 18, 16, 14, 12, 10, 8, 7, 6, 5, 4]

# 设置极坐标
angles = np.linspace(0, 2 * np.pi, len(countries), endpoint=False).tolist()
cases = np.array(cases)
cases_log = np.log10(cases)  # 对数变换，或者使用cases_log = np.log10(cases + 1)以避免log(0)的问题
cases_log = np.concatenate((cases_log, [cases_log[0]]))
angles = np.concatenate((angles, [angles[0]]))

# 创建图表
fig, ax = plt.subplots(figsize=(10, 10), subplot_kw=dict(polar=True))
# 使用颜色映射
cmap = matplotlib.cm.get_cmap('RdYlBu_r')
colors = cmap(cases_log / max(cases_log))
# 绘制每个扇形
for i in range(len(countries)):
    ax.fill_between(angles[i:i+2], 0, cases_log[i:i+2], color=colors[i], alpha=0.7)
# ax.fill(angles, cases_log, color='red', alpha=0.25)  # 这是不设置渐变色的方法
ax.plot(angles, cases_log, color='red', linewidth=2)

# 设置角度标签
log_ticks = [1, 10, 100, 1000, 10000]
log_labels = ['1', '10', '100', '1000', '10000']
ax.set_yticks(np.log10(np.array(log_ticks)))  # 如果上面使用了log10(cases + 1)，这里也要对应修改为log_ticks + 1
ax.set_yticklabels(log_labels)
ax.set_xticks(angles[:-1])
ax.set_xticklabels(countries)

# 设置标题
plt.title('新冠肺炎全球疫情形势')
plt.show()
```


### `Tick`
`ax.xaxis.major`：XAxis对象的实例，用于处理x轴tick以及label的绘制
`ax.yaxis.major`：YAxis对象的实例，用于处理y轴tick以及label的绘制
```python
formatter = matplotlib.ticker.FormatStrFormatter('$%1.2f')  # 设置y轴的格式为美元，保留两位小数
ax.yaxis.set_major_formatter(formatter)  # 设置y轴的主要刻度的格式
ax.yaxis.set_tick_params(which='major', labelcolor='green', labelleft=False, labelright=True)  # 设置ticker的参数，右侧为主轴，颜色为绿色
```


# 3. Text

使用LaTeX：
https://matplotlib.org/stable/gallery/text_labels_and_annotations/tex_demo.html

设置字体：
全局：
`plt.rcParams['font.sans-serif'] = ['SimSun']`指定默认字体为宋体
`plt.rcParams['axes.unicode_minus'] = False`解决图像负号`-`显示为方块和报错的问题。
局部：
`plt.ylabel('y轴名称', fontproperties='Microsoft YaHei', fontsize=14)`
`plt.title('坐标系的标题',  fontproperties='Microsoft YaHei', fontsize=20)`
`plt.legend(loc='lower right', prop={"family": 'Microsoft YaHei'}, fontsize=10)`
`plt.text(0.5, 0.5, '中文', fontproperties='SimHei')`

## 3.1 `Figure`和`Axes`的文本

`matplotlib.text.Text`对象用于在图表中添加文本。
- `text`：在Axes对象的任意位置添加文本
- `suptitle`：在Figure对象上添加标题
- `annotate`：在Axes对象的任意位置添加注解
```python
fig = plt.figure()
ax = fig.add_subplot()
# 分别为figure和ax设置标题，注意两者的位置是不同的
fig.suptitle('bold figure suptitle', fontsize=14, fontweight='bold')  # 设置figure的标题，在ax设置的标题的上面
ax.set_title('axes title')  # 设置axes的标题，是子图的标题，在figure的标题的下面
ax.axis([0, 10, 0, 10])  # 设置x和y轴显示范围均为0到10
# 在子图上添加文本
ax.text(3, 8, 'boxed italics text in data coords', style='italic', bbox={'facecolor': 'red', 'alpha': 0.5, 'pad': 10})
ax.annotate('annotate', xy=(2, 1), xytext=(3, 4),arrowprops=dict(facecolor='black', shrink=0.05))  # 添加注解
plt.show()
```

## 3.2 `Tick`的文本
```python
# 使用axis的set_ticklabels方法手动设置标签格式的例子
fig, axs = plt.subplots(2, 1, figsize=(5, 3), tight_layout=True)
x1 = np.linspace(0.0, 5.0, 100)
y1 = np.cos(2 * np.pi * x1) * np.exp(-x1)
axs[0].plot(x1, y1)
axs[1].plot(x1, y1)
ticks = np.arange(0., 8.1, 2.)
tickla = [f'{tick:1.2f}' for tick in ticks]
axs[1].xaxis.set_ticks(ticks)  # 设置x轴刻度：0, 2, 4, 6, 8
axs[1].xaxis.set_ticklabels(tickla)  # 设置x轴刻度标签：0.00, 2.00, 4.00, 6.00, 8.00
plt.show()
```
```python
fig, axs = plt.subplots(2, 1, figsize=(6, 4), tight_layout=True)
x1 = np.linspace(0.0, 6.0, 100)
y1 = np.cos(2 * np.pi * x1) * np.exp(-x1)
axs[0].plot(x1, y1)
axs[0].set_xticks([0, 1, 2, 3, 4, 5, 6, 7])
axs[1].plot(x1, y1)
axs[1].set_xticks([0, 1, 2, 3, 4, 5, 7])  # 要将x轴的刻度放在数据范围中的哪些位置(这里越过了x=6的位置，下面的刻度标签也会少一个)
axs[1].set_xticklabels(['zero', 'one', 'two', 'three', 'four', 'five', 'seven'],  # 设置刻度对应的标签
                       rotation=30, fontsize='small')  # rotation选项设定x刻度标签倾斜30度
axs[1].xaxis.set_ticks_position('bottom')  # set_ticks_position()方法是用来设置刻度所在的位置，常用的参数有bottom、top、both、none
plt.show()
```
比如设置三位小数：
`formatter = matplotlib.ticker.FormatStrFormatter('%1.3f')`
`ax.xaxis.set_major_formatter(formatter)`
或者使用函数传递：

```python
# 接收函数的例子
def formatoddticks(x, pos):
    """Format odd tick positions."""
    if x % 2:
        return f'{x:1.2f}'  # 保留两位小数
    else:
        return f'{x:1.1f}'  # 保留一位小数
fig, ax = plt.subplots(figsize=(5, 3), tight_layout=True)
ax.plot(x1, y1)
ax.xaxis.set_major_formatter(formatoddticks)
plt.show()
```
还有官方提供的便捷设置：
```python
matplotlib.ticker.AutoLocator()  # 自动选择刻度
matplotlib.ticker.MaxNLocator(nbins=7)  # 最大刻度数为7
matplotlib.ticker.MultipleLocator(5)  # 刻度是5的倍数
matplotlib.ticker.FixedLocator([0, 2, 4, 6, 8])  # 固定刻度
matplotlib.ticker.IndexLocator(offset=0.5, base=1)  # 从0.5开始，每隔1个单位
```

# 4. `Color`
缩写：
| b | g | r | c | m | y | k | w |
|---|---|---|---|---|---|---|---|
| blue | green | red | cyan | magenta | yellow | black | white |
| 蓝色 | 绿色 | 红色 | 青色 | 品红 | 黄色 | 黑色 | 白色 |

RGBA，比如`plt.plot([4,5,6],[1,2,3],color=(0.1, 0.2, 0.5, 0.5))`
`plt.plot([4,5,6],[1,2,3],color='#0f0f0f80')`

[cmap](https://matplotlib.org/stable/users/explain/colors/colormaps.html)：
```python
x = np.random.randn(50)
y = np.random.randn(50)
plt.scatter(x, y, c=x, cmap='RdPu')
plt.colorbar()
plt.show()
```

`['viridis', 'plasma', 'inferno', 'magma', 'cividis']`
<img src="https://matplotlib.org/stable/_images/sphx_glr_colormaps_001.png" width="80%">
`['Greys', 'Purples', 'Blues', 'Greens', 'Oranges', 'Reds', 'YlOrBr', 'YlOrRd', 'OrRd', 'PuRd', 'RdPu', 'BuPu', 'GnBu', 'PuBu', 'YlGnBu', 'PuBuGn', 'BuGn', 'YlGn']`
<img src="https://matplotlib.org/stable/_images/sphx_glr_colormaps_002.png" width="80%">
`['binary', 'gist_yarg', 'gist_gray', 'gray', 'bone', 'pink', 'spring', 'summer', 'autumn', 'winter', 'cool', 'Wistia', 'hot', 'afmhot', 'gist_heat', 'copper']`
<img src="https://matplotlib.org/stable/_images/sphx_glr_colormaps_003.png" width="80%">
`['PiYG', 'PRGn', 'BrBG', 'PuOr', 'RdGy', 'RdBu', 'RdYlBu', 'RdYlGn', 'Spectral', 'coolwarm', 'bwr', 'seismic']`
<img src="https://matplotlib.org/stable/_images/sphx_glr_colormaps_004.png" width="80%">