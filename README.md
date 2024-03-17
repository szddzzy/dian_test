# dian_test
dian团队算法方向招生题

本来顺手就写在代码最后面，但是怕不方便看，就又写了一遍
# content
-[第一部分（全连接层）](#学习记录：(第一部分题目：全连接层))

-[第二部分（RNN网络）](#学习记录：(第二部分题目：RNN网络))
# 学习记录：(第一部分题目：全连接层)

   **对于测评指标的基本理解：(多分类问题)**
    
        accuracy反映的是总体预测值和标签值匹配的概率，但是反映的信息不够全面，我们如果想
        
        了解某个分类是不是更容易被预测出来，或者更容易被误预测等等，就需要其他指标来测评
        
        precision反映的是某一个分类在所有的预测值中，预测对了的概率
        
        recall反映的是标签中的某一分类，被正确预测出的概率，体现这个分类是否容易被预测
        
        F1-score是上面两个的调和平均数，算是一个综合考量。

  *这边贴一张我的测试截图，可以看到每个分类单独计算指标*

  ![image](https://github.com/szddzzy/dian_test/blob/main/test_pic1.png)

        
  **对于全连接神经网络的理解:**
    
        根据我个人的理解，神经网络的作用就是找出输入数据和输出数据之间的映射关系，方法是通过
        
        反向计算梯度，也就是损失(预测值与标签值的差距，这个差距也有多种计算方式)对权重的求导
        
        w=w-grad*lr,通过反向传播来逐渐减小损失的大小，是预测值向标签值逼近。

  *下面是一张简单的 loss-weight 函数*

  ![image](https://github.com/szddzzy/dian_test/blob/main/test_pic2.png)

        由这张图可以很直观地了解loss和weight之间的关系，每一次梯度更新实际上就是使weight向能够让

        loss减小的方向移动，最后找出让loss最小的weight，也即找出极小值点。

        但在实际中，往往极小值点并不是最小值点。而各种优化器就是为我们解决之一难题的。
        
  **对模型层数的理解：**
    
        增大隐藏层的层数可以提高学习能力。因为增加层数就是增加了权重数量，模型更加复杂，
        
        对输入数据的变化也会更加敏感，但同时也可能由于过于敏感，对噪声的反映也很强烈，
        
        这就不是我们想要的结果。我们想要的是模型对输入数据敏感，但对噪声忽视，
        
        所以模型层数不能太多，也不能太少。

  *下面两张图片是我分别采用较多隐藏层和没有隐藏层的可视化矩阵*

  ![image](https://github.com/szddzzy/dian_test/blob/main/test_pic3.png)

  ![image](https://github.com/szddzzy/dian_test/blob/main/test_pic4.png)

        可以看出，两者还是有显著差别
        
  **对全连接层处理图片问题的理解：**
    
        mnist分类问题里，为了使线性层可以对图片数据进行处理，把一个二维矩阵(28,28),
        
        转化成了一个行向量(784)，这种方法虽然利于模型处理数据，但却破坏了图片的空间结构，
        
        比如人的头和脖子连接在一起，这种空间上的关系在二维矩阵上可以看出，但在一维向量上
        
        就没办法表示这种空间上的关系。而这种空间关系往往还是图片数据处理的关键，所以
        
        全连接层处理mnist问题的accuracy有个极限值，很难再提高了。

# 学习记录：(第二部分题目：RNN网络)

  **对RNN网络的理解：**
    
        RNN网络与基础的全连接层的巨鳖就在于RNN网络引入了上一个样本与这一个样本之间的关系，
        
        这样就可以体现出数据之间的顺序关系。具体的操作就是把上一次隐藏层中的数据留存下来，
        
        并且作为这一次输入数据的一部分，和输入数据融合，一起计算这一次的隐藏层数据，实现
        
        两次运算的关联，从而推理出数据之间的相关性。
        
  **RNN的缺陷：**
    
        RNN网络可以对数据之间的先后顺序进行学习，但是也有局限性，比如随着样本不断计算，
        
        第一个样本和最后一个样本之间的关联会逐渐不被注意。Self-attention机制实际上就解决了
        
        这个问题，它可以无视这种距离的远近对关联度计算的影响。下一个题目里有我对attention
        
        的理解。
        
  **对本题的理解：**
    
        因为fashion-mnist对图片顺序并没有什么要求，所以用RNN网络进行训练优势不大，
        
        我用基础的全连接层也试了一下，两者的正确率区别不大，而且RNN更耗时间






