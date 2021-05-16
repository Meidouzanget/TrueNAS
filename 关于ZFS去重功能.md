# TrueNAS

写入两个相同的文件根本就没去重

去重ZFS文件系统的一个特性，不过实际用起来并不美好

我一共写入3份，开了这个功能写入非常慢，十几mb那种

这个问题我就当我配置不够好了，毕竟ZFS很吃内存

但问题是我在控制页查看储存池用量，这根本就没去重啊，已用空间就是文件x3的大小

如一下reddit的大佬所解释

https://www.reddit.com/r/freenas/comments/evlgjw/using_deduplication_safely/ffwxwnf/

![15645](https://user-images.githubusercontent.com/59044398/118381284-05f1bc00-b61c-11eb-9922-16414cfe4026.PNG)

![捕获](https://user-images.githubusercontent.com/59044398/118381298-2e79b600-b61c-11eb-91ac-03e7ead69722.PNG)

ZFS去重有三种方式：文件级，块状级，字节级

Truenas用的是块状级，就是把文件分成块状，再计算块状哈希再去重

然而文件那几个部分被分成同一块，是随机的，所以每个块状都不同自然哈希也不同，可谓是随缘去重

以昂贵的内存，和cpu计算廉价硬盘的随缘去重，不现实

然而，TrueNas关闭了去重和lz4文件压缩后，传输速度依然糟糕

![4156456](https://user-images.githubusercontent.com/59044398/118381400-21a99200-b61d-11eb-8696-8469c1cff017.PNG)

![4156486](https://user-images.githubusercontent.com/59044398/118381402-240bec00-b61d-11eb-8acb-53978f8c7bd8.PNG)

对比群晖下图。我对ZFS的性能有多怀疑。

因为内存只有4g，写入慢也可能是内存太小的原因，无法断定

![48784564](https://user-images.githubusercontent.com/59044398/118381440-6b927800-b61d-11eb-80f9-869fbd0ecd9c.PNG)


