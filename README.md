# SZStiching

## 项目介绍
一、 识别图片重合部分的智能长拼图工具
二、只有纵向重合的图片才能识别拼成（识别成功率在80%-90%之间）

### 项目运用到的算法


####   一. 提取指纹算法：
   
      1）循环冗余校验码（crc32）
      
      2）灰度公式提取灰度值：0.3B + 0.59G + 0.11R，提取每行主色调
      
####   二. 获取重合部分算法：
   
       1.最长公共子串+动态规划
         (1)将两个字符串分别以行和列组成矩阵。
         (2) 计算每个节点行列字符是否相同，如相同则为 1。
         (3) 通过找出值为 1 的最长对角线即可得到最长公共子串。
####    ![image](https://github.com/shaozhe-chen/SZStiching/blob/master/SZStiching/normal.png)

         进一步的优化:
            我们可以将字符相同节点(1)的值加上左上角(d[i-1, j-1])的值，
            这样即可获得最大公用子串的长度。如此一来只需以行号和最大值为条件即可截取最大子串。
####    ![image](https://github.com/shaozhe-chen/SZStiching/blob/master/SZStiching/youhua.png)
####   三. 耗时优化：
   
      1） crc32+灰度公式：使用多线程并发处理，最后在线程同步的时候处理结果
      
      2） 灰度公式：跳点取像素点
