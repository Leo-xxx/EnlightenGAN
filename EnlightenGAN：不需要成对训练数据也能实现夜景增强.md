## EnlightenGAN：不需要成对训练数据也能实现夜景增强

埃里克不吃香菜 [CVer](javascript:void(0);) *今天*

点击上方“**CVer**”，选择加"星标"或“置顶”

重磅干货，第一时间送达![img](https://mmbiz.qpic.cn/mmbiz_jpg/ow6przZuPIENb0m5iawutIf90N2Ub3dcPuP2KXHJvaR1Fv2FnicTuOy3KcHuIEJbd9lUyOibeXqW8tEhoJGL98qOw/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

> 作者：埃里克不吃香菜
>
> https://zhuanlan.zhihu.com/p/70230047
>
> 本文已授权，未经允许，不得二次转载

EnlightenGAN: Deep Light Enhancement without Paired Supervision

![img](https://mmbiz.qpic.cn/mmbiz_png/yNnalkXE7oXIEeQ0emUqz3icicgVaIG0F08SZOpzGO8nofib4AvtkS6icY2BlMqtfowbnaiajiccaeS1Ah94fugd0XcA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

arXiv：https://arxiv.org/abs/1906.06972

code：https://github.com/yueruchen/EnlightenGAN

最近一年来，夜景模式逐渐成为各大手机厂商的标配，从google pixel3到oppo，xiaomi，huawei，夜景拍摄逐渐成为人们的刚需。

![img](https://mmbiz.qpic.cn/mmbiz_jpg/yNnalkXE7oXIEeQ0emUqz3icicgVaIG0F0PLO1tUOWP9TBclJ1GLblUJt4lWibXdoZ9bYdMTK8d7sTakbzLs2doNw/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)易烊千玺代言huawei夜景模式广告

尽管传统方法在亮度增强上已经有了不错的效果（例如直方图均衡化，Retinex），此类算法缺乏对context信息的处理，限制了最终效果的提升。基于data-driven同时又学习prior knowledge的深度学习方法更加吸引我们。然而，训练data-driven方法同时要求我们拥有更多的成对数据。如何解决收集和制作大批量成对数据的难题极大的阻碍了深度学习方法应用于实际场景当中。

本文中提出了应用于无监督学习的低光图像增强算法。具体而言，作者在实验中发现由pre-trained VGG model构成的perceptual loss对光照信息并不敏感，于是构建了perceptual loss和adversarial loss对抗的损失函数。perceptual loss成功地约束了图片除光照以外的特征信息，而GAN loss帮助模型学习了生成更加逼进真实光照的图像。区别于CycleGAN，EnlightenGAN并未使用cycle consistency的结构来约束模型稳定性，只需要one-path architecture就能训练，节省了训练复杂性。

![img](https://mmbiz.qpic.cn/mmbiz_jpg/yNnalkXE7oXIEeQ0emUqz3icicgVaIG0F06x3A5icRiaMFAK2vHfQCIULPNiagBFnVIZL5DDZAX9dljCvbU4sQLJWOA/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)Two-path GAN vs. One-path GAN

除此之外。无监督学习相比于监督性学习引入了更多的不稳定性，作者加入了self-regularized attention和global-local discriminator模块来提高模型对于细节特征的处理，具体结构如下。

![img](https://mmbiz.qpic.cn/mmbiz_jpg/yNnalkXE7oXIEeQ0emUqz3icicgVaIG0F0L849ibcsx0qIy2oiaot7diaUeiau5ztpqezxPh2arUb02TQ09C5Xrf1rgQ/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

同时，本文采用了第三方用户评测和non-referenced metric来对模型进行比较

![img](https://mmbiz.qpic.cn/mmbiz_jpg/yNnalkXE7oXIEeQ0emUqz3icicgVaIG0F0zia6tHic17Zz0VqltUxImVQKoHjdnYhADbwSomwYclfJO18eLt0pcjjQ/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

![img](https://mmbiz.qpic.cn/mmbiz_jpg/yNnalkXE7oXIEeQ0emUqz3icicgVaIG0F0vEVWmENEteia9PDQkP8j8pUO33v1Lofy8Cse6pmV17BEullCIC5Wiaeg/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

最后，由于无监督训练带来的便利性，EnlightenGAN可以随意地更换数据集来实现领域适配。例如，当我们想将模型应用到条件恶劣的自动驾驶数据集中时，我们可以仅改变低光训练数据为自动驾驶场景（Berkeley Deep Drive）的低光数据，正常光数据依旧使用先前数据，由于模型在训练时已经适配自动驾驶数据集的环境，训练的模型相比于未适配模型有了显著的提升（最右列是适配的模型），对比倒数第二列和传统算法，适配后的模型既能做到亮度的提升，也减小了artifacts。

![img](https://mmbiz.qpic.cn/mmbiz_jpg/yNnalkXE7oXIEeQ0emUqz3icicgVaIG0F0YbAicVSBCsmWRvCiaPib6wOSk78kNd56ITDnXqHxSfVo5FcSKpwnRAf2g/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

**CVer学术交流群**



扫码添加CVer助手，可申请加入**CVer-目标检测交流群、图像分割、目标跟踪、人脸检测&识别、OCR、超分辨率、SLAM、医疗影像、Re-ID、GAN、NAS、深度估计、自动驾驶和剪枝&压缩等群。****一定要备注：****研究方向+地点+学校/公司+昵称**（如目标检测+上海+上交+卡卡）

![img](https://mmbiz.qpic.cn/mmbiz_jpg/yNnalkXE7oX7pdpBKibicSnmb8wRGicbT0Rhr61k0f922lbXcowibk5DTRibROvFB1yMCAZQvj1iaEe6Qsia9bU0UMJCA/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

▲长按加群



![img](https://mmbiz.qpic.cn/mmbiz_png/e1jmIzRpwWg3jTWCAZ4BrnvIuN20lLkhIjtg4GRSDhTk9NpeF0GGTJwUpKPatscIQU7Ndj9hgl8BPpGj2BJoFw/640?tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

▲长按关注我们

**麻烦给我一个在看****！**

[阅读原文](https://mp.weixin.qq.com/s?__biz=MzUxNjcxMjQxNg==&mid=2247490051&idx=3&sn=0ed8d5e924de831a490b5ee722d6eb2d&chksm=f9a2688cced5e19aab7764dc2a66701e30c789bfa79df1cc0e522752d03f7ecb7a4576a87821&mpshare=1&scene=1&srcid=&key=0aa21025b9197e7f544b2ea9d4af33e07875e341ce34e2e1cdac8d0d9e1458c961ee38d2a7d9f012b2c5fc68a19ad65abfce7eb8de2ef199907a2fd6c624092eadf85827ed134b414af1179bea43f141&ascene=1&uin=MjMzNDA2ODYyNQ%3D%3D&devicetype=Windows+10&version=62060833&lang=zh_CN&pass_ticket=uE%2FzNT3xkKpTnhtL1gR7a%2BevYo04HqaegFNjM616cr2UKiV9sbfqtnWsOhV7gv5o##)



![img](https://mp.weixin.qq.com/mp/qrcode?scene=10000004&size=102&__biz=MzUxNjcxMjQxNg==&mid=2247490051&idx=3&sn=0ed8d5e924de831a490b5ee722d6eb2d&send_time=)

微信扫一扫
关注该公众号