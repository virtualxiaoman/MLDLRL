Hello！这是我的学习笔记，主要是ML、DL、RL、CV、NLP、RS等AI相关的内容。笔记的仓库**可以直接下载下来看，无需经由我同意**。但是**请不要用于学习之外的用途**（比如不标注出处的转载、商业用途、大篇幅抄袭等），少量引用可以不注明出处，引用多了还是希望能注明出处是`virtual小满  https://github.com/virtualxiaoman/MLDLRL`。

- PDF与Word的内容一般是一样的，但PDF可能落后一些版本，因为我懒得每次写完转PDF，可以下载word后自行转为PDF。
- html是markdown直接导出的，方便阅读，未来可能上线**在线阅读版**，目前已经能在本地阅读了，我还没买服务器，所以暂时没法在线阅读。
~~现已将仓库里的部分html文件删除了，如果需要可以查看`Sep 13, 2024`的`95515f535d8721fd4e997397628f643faf426116`这个commit以及之前的版本。因为md转PDF的时候用html作为中转站的话CSS不容易丢失，所以留存了部分html，html转PDF的代码在[easier_tools/html2pdf.py](https://github.com/virtualxiaoman/Easier_DataScience/blob/master/easier_tools/html2pdf.py)中。~~ 建议使用Typora。

md内统一使用的语法有：
```
小标题：
<p style="color:#EC407A; font-weight:bold">1. 小标题</p>

图片：
<div style="display: flex; justify-content: center; align-items: center;">
    <div style="text-align: center;">
        <img src="assets/···/···/···.png" style="width: 60%;"/>
        <p style="font-size: small; color: gray;">注释</p>
    </div>
</div>

代码：
<div style="display: flex; justify-content: center; align-items: center;">
<div style=" max-height: 200px; max-width: 90%; overflow-y: auto; border: 1px solid #39c5bb; border-radius: 10px;">
```python
很长的一段代码
```
</div>
</div>

```

以PDF、md为例，本笔记的整个结构与描述是：
```
.
├── 数学基础.pdf        [√]主要是线代与概率论，参考的鸢尾花书、雷明
├── 数据分析-Code.pdf   [√]之前的练手的，能run，但是正在整理与重构中，请参考我的Easier_DataScience仓库
├── 机器学习.pdf        [正在更新]机器学习(含DL)的原理推导(一般不推导纯数学公式)
├── 深度学习.md         [正在更新]对深度学习的一些总结，正在机器学习.pdf中迁移出来
├── 推荐系统.md         [暂缓更新]
├── 扩散模型.md         [暂缓更新]
├── 自然语言处理.md     [暂缓更新]
├── LaTex.md           [偶尔更新]
├── git.md             [偶尔更新]
├── 代码基础.pdf        [×]刚学的时候记录的，还没翻新，逻辑可能混乱
├── 数据处理-Code.pdf   [×]虽然数据处理很重要，但是我比较懒，还没翻新，而且也可以在Easier_DataScience中找到
```
建议将**数学基础**当做查阅；

**机器学习**的还是可以的(自认为)，算是比较基础的，因为当初学的时候也是从这个开始的；

**数据分析**的代码请参考[Easier_DataScience](https://github.com/virtualxiaoman/Easier_DataScience)(基本所有的机器学习、深度学习等的代码都会整合到里面去，形成统一而便捷的api调用或是demo)；

**深度学习**是我自己的一些总结，正在持续更新中，不过可能不适合初学者，初学可以看下文的推荐资料；

**推荐系统**、**扩散模型**、**自然语言处理**只是浅浅学了一点。


## 1.最主要、最好的的参考资料与个人的一点推荐
1. [《鸢尾花书》](https://github.com/Visualize-ML) - 从加减乘除到机器学习
    - **推荐理由**：配图极其优秀，整体逻辑比较连贯，原理讲解很棒。我所见过的最想让你看懂的书籍，能看出作者的用心。
    - **缺陷**：有些啰嗦，没办法速通，代码写的也是一坨，甚至不肯格式化一下。
2. [《动手学深度学习》](https://zh.d2l.ai/) - 面向中文读者的能运行、可讨论的深度学习教科书，简称d2l
    - **推荐理由**：深度学习实操，除了部分大一点的模型我的电脑太辣鸡直接爆显存之外，基本都能直接运行，而且原理的讲解确实牛逼，社区也不错。
    - **缺陷**：虽然是中文，但是很有机翻的感觉。什么都放在d2l.py里了，代码逻辑比较混乱，需要自己重构一部分代码，但是起码也算是我目前见过的代码写得比较好的了。
3. [李宏毅深度学习教程 LeeDL Tutorial](https://github.com/datawhalechina/leedl-tutorial) - 李宏毅的深度学习课程
    - **推荐理由**：不是入门书，可以先看[d2l]((https://zh.d2l.ai/))再看这个。这个书提及了很多细节与问题，更多的是启发性思考，主要是讲解一些深度学习的原理。
    - **缺陷**：没有代码实现，然后感觉就是他的课的文字版，有些地方都没校验就直接放上去了，需要自己去看源视频。（因为我自己不喜欢看视频来学习，所以我看的是这个书，视频还是很不错的）
4. [Easier_DataScience](https://github.com/virtualxiaoman/Easier_DataScience) - [自荐]我写的一些便于MLDL等AI相关的module或是一些demo，希望调用或复用的时候更方便
    - **推荐理由**：方便调用，不用每次都写一遍
    - **缺陷**：还在更新中，有些模块还没写完或者还没测试，部分代码逻辑可能不够清晰，就当是自己的练手了。
5. [雷明-机器学习的数学](https://www.epubit.com/bookDetails?id=UB7812edb26d3f9) - 机器学习的数学基础
    - **推荐理由**：数学推导比较详细，适合想要深入了解的人。
    - **缺陷**：没图，全是公式。另外目前还没在网上找到电子书，我是买的纸质的。

(好像我格外喜欢电子书，逃~~)(我是Datawhale和d2l的狗~)


## 2.其余推荐资料
**没**打○的就是我**没看过**，阿巴阿巴~（没看的未来应该会看的，看完了再更新评价）。

中文社区的资料就这鬼样子，真的烂大街的我肯定不会放上来了。

以下排名分先后（我没看的不算）：
1. ○[AI数学笔记 Liang's Blog](https://wangliangster.github.io/#/) 
   ○[AI算法工程师手册 huaxiaozhuan](https://www.huaxiaozhuan.com/)
    - **比较难的公式推导都有**，按需查阅。
    - 感觉挺全面的。
2. ○[动手学ML](https://github.com/boyu-ai/Hands-on-ML) 
    - 电子书，免费。
    - 不是入门书，**适合有一定基础**的看。
    - 部分公式存在严重错误，但是讲解还可以，需要有自己的判断能力。
    - 习题答案可以参考：[motewei](https://github.com/motewei/Hands-on-ML-solutions)
3. ○[文亮-推荐系统技术原理与实践](https://www.epubit.com/bookDetails?id=UB831721e9d193a)
   - 有电子书(需要异步会员，但是异步会员可以通过已经购买了的纸质书兑换)，相当于半白嫖。
   - 整体**讲解还可以**，最好搭配[FunRec](https://datawhalechina.github.io/fun-rec/#/)一起看。
   - 举例大部分是阿里巴巴的模型，难道阿里巴巴给他打钱了？
4. ○[动手学NLP](https://github.com/boyu-ai/Hands-on-NLP)
    - 无电子版(异步都没电子版)，买了纸质书，书挺好的，但我现在被劝退了，我不适合学NLP，感觉NLP的理论不美。
5. ○[王晓华-从零开始大模型开发与微调：基于PyTorch与ChatGLM](http://www.tup.tsinghua.edu.cn/Wap/tsxqy.aspx?id=10334701)
    - 有电子版，付费，跟纸质版价格差不多。有[神秘链接](https://pan.baidu.com/s/1cY8htDmzXMIoJIan9aIWRw?pwd=fgyb)，但是要快手关注才能拿密码，我又没下。。。
    - 这本书不适合0基础，而是适合学了一点之后再看。其号称“通俗易懂”的原因是**难的都不讲**，都让读者“自行在网上查阅”。
    - 没有原理讲解，代码写的屎到不行而且有些感觉直接copy的连注释都是英文(我见过的最烂的)，唯一的优势是新且比较实用。
6. [动手学CV](https://github.com/boyu-ai/Hands-on-CV)
   - 无电子版，而且github仓库都没建好，纸质书好像也没了，所以我没看
7. [动手学RL](https://github.com/boyu-ai/Hands-on-RL)
    - 有电子版，据说好
8. [带注释的pytorch论文实现](https://nn.labml.ai/zh/)
    - 个人感觉翻译得非常差，但是类似的其他资源还没找到更好的
9. [强化学习导论](https://rl.qiwihui.com/zh-cn/latest/index.html)
10. [人大LLM-Book](https://github.com/LLMBook-zh/LLMBook-zh.github.io)
    - 可下载阅读

以下请避雷：
1. 扩散原理从入门到实战-异步图书：**没有原理讲解**，我看完了还是一知半解的状态，代码是英文原版的机翻。另外其实这是个[开源的书](https://huggingface.co/datasets/HuggingFace-CN-community/Diffusion-book-cn)，感觉不如看[这个开源资料](https://github.com/yangqy1110/Diffusion-Models/tree/main)。
2. 自动机器学习入门与实践-华中科技大学出版社：**没有原理讲解**，大部分是ML而非autoML，代码就是英文原版的一个字都没改。


## 3.部分大型的开源学习资源
1. [Datawhale-github](https://github.com/datawhalechina)或者[Datawhale-官网](https://datawhale.cn/learn)
好像都是免费，质量还挺不错的(但是因为显然每一章节的作者不相同，导致逻辑连贯性不够强、符号使用不太统一)，但是感觉最近更新的不多，好的教程似乎都已经是一两年前的了。整体来说，我觉得Datawhale的质量还是比较高的，并且有些教程确实是**独一无二**的，比如`plt`的我就没在其他地方看到研究得这么细致的。
2. [boyuai-github](https://github.com/boyu-ai)或者[boyuai-官网](https://www.boyuai.com)
有付费内容，但是动手学系列都是免费的，但是动手学NLP,CV的不知道为什么没有电子书了，所以只有ML,RL有电子书了，唉。


## 4.视频
1. [B站-这是我已经看完了的视频教程的一个收藏夹](https://space.bilibili.com/506925078/favlist?fid=2648566378)
主要包括：
- [BV1T84y167U9](https://www.bilibili.com/video/BV1T84y167U9/)  机器学习(传统的机器学习算法基本都有)。虽然我不推荐看唐宇迪的视频来学机器学习，但是他的视频确实简单，拿个二倍速过一遍当**入门**就行，不要去纠结其中的代码是怎么写的或者去纠结他公式推导的细节。
- [BV1RT411G7jJ](https://www.bilibili.com/video/BV1RT411G7jJ)  机器学习(侧重统计学习)。内容不是很多，但是讲的都很好
- [BV15V411W7VB](https://www.bilibili.com/video/BV15V411W7VB/)  机器学习(侧重神经网络)。跟上面一个一样，内容讲的很不错，能启发思考。

2. 李沐、李宏毅、吴恩达等大佬的视频，这里不给出链接了，B站一搜就有的，去Youtube看也行。真的比唐宇迪的强很多。


## 5.对于我阅读较久的书籍&视频的一些打分

| 书籍 | 整体印象[^1] | 阅读舒适度[^2] | 实用性[^3] | 逻辑性[^4] | 启发性[^5] | 语言[^6] |
|------|---------|-----------|-------|--------|-------|-------------------------------|
| [《动手学深度学习》](https://zh.d2l.ai/)|9| ★★★★★  | ★★★★☆ | ★★★★☆ | ★★★★☆ |★★★☆☆|
|  [李宏毅深度学习教程 LeeDL Tutorial](https://github.com/datawhalechina/leedl-tutorial) |9| ★★★★★ | ★★★☆☆ | ★★★★☆ | ★★★★★ |★★★☆☆ |
| [《鸢尾花书》](https://github.com/Visualize-ML)|8.5| ★★★★☆  | ★★★☆☆ | ★★★★☆ | ★★★★★ |★★★★★ |
| [《机器学习的数学》](https://www.epubit.com/bookDetails?id=UB7812edb26d3f9) |8| ★★★☆☆  | ★★★★☆ | ★★★★☆ | ★★★☆☆ |★★★★☆ |
| [动手学ML](https://github.com/boyu-ai/Hands-on-ML) |7| ★★★☆☆  | ★★★☆☆ | ★★★★☆ | ★★★☆☆ |★★★☆☆ |
| [BV1T84y167U9](https://www.bilibili.com/video/BV1T84y167U9/) | 5| ★★★★☆  | ★★★★☆ | ★★☆☆☆ | ★☆☆☆☆ |★★★☆☆ |

以上是我觉得还不错的资料的评分。评分十分主观，仅供参考，应当根据自己的学习**目的与风格**选择适合自己的学习资料。

[^1]: 整体印象是我的主观感受。
[^2]: 阅读舒适度是能不能让人有继续阅读的冲动。
[^3]: 实用性主要是看代码写的好不好。
[^4]: 逻辑性主要看作者的思维。
[^5]: 启发性主要看作者能否给我带来启发。
[^6]: 语言是指作者的语言表达能力，不是指代码的语言。包括：是否是母语或者翻译得是否是个正常人、描述是否清晰、用词是否准确。


