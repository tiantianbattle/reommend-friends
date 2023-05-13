# reommend-friends
Best friend recommendation using Mapreduce

该仓库只记录代码和实验理念，虚拟机搭建暂没有提供，该项目主要是使用mapreduce去实现最佳好友推荐，具体过程如下：

![image](https://github.com/tiantianbattle/reommend-friends/assets/71861094/6a2a2a82-0eb0-4ee5-b7b8-b68afed394af)


虚拟机网络通信如下：node节点使用虚拟机CenterOS 7 

![image](https://github.com/tiantianbattle/reommend-friends/assets/71861094/468d1ed7-df40-4705-b76a-70ab3db297c3)


数据集选择为soc-LiveJournal1Adj.txt，下面是一个具体推荐好友例子：
该数据包含用户ID邻接表中的多个数据。数据集中的第一个属性是用户的ID，其中用户的ID是一个唯一值。第二个属性是以逗号分隔的用户列表。在下图中，你可以看到用户0不是用户4、5的朋友，但是用户0和用户4有3位共同好友分别是1，2，3。用户0和用户5有一位共同好友就是用户1。因此可以发现用户0和用户4，5都有共同好友，因此推荐用户4和用户5位用户0为好友。

![image](https://github.com/tiantianbattle/reommend-friends/assets/71861094/1b0d09a2-4f60-4a32-95c4-33575e22c520)


## Map阶段
1）发出<fromUser,r=toUser;m=-1>对于所有toUser。假设有n个toUser；然后我们将发出n条记录来描述fromUser和toUser已经是朋友。请注意，他们已经是发出的key和r之间的朋友，因此我们将m设置为-1。

2）发出<toUser1,r=toUser2;m=fromUser>对于toUser1和toUser2从toUser的所有可能组合，并且他们有共同的朋友fromUser。它将发出n(n-1)条记录。

3）总共有n^2个在map阶段发出的记录，其中n是朋友的数量。


## Reduce阶段
1）只是总结他们在键和值r之间有多少共同好友。如果他们中的任何一个有共同的朋友-1，我们就不会推荐，因为她们已经是朋友了。

2）根据共同好友的数量对结果进行排序。

实验生成的jar包可以直接在虚拟机上进行分布式实验
