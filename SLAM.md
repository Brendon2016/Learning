# SLAM

## 要点记录

* simultaneous localization and mapping
* At a theoretical and conceptual level, SLAM can now be considered a solved problem。在理论层次上，SLAM已经解决的足够好了
* because of the common error in estimated vehicle location,the estimates of landmarks are all necessarily correlated with each other ,thus this would require to employ a huge state vector composed of the vehicle pose and every landmark position.机器人定位误差使得地标的位置估计是相关，也就是说每个地标的状态都是所有已知地标状态的函数，即需要一个很大的状态，其包含机器人位姿和地标位置。
* 考虑到计算的复杂性（状态向量太长了）和没有地图收敛性的知识，一般假定地标的相关性为0，这样状态转移矩阵中大部分数据就为0和1了，地标间就相互解耦了。