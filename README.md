# 4-Huqy518
4-Huqy518 created by GitHub Classroom
# 实验平台
  * 系统：Ubuntu 16.04
  * CPU：Inter(R) Core(TM) i7-6700HQ
  
# 实验说明：
  * 本次实验直接使用了meltdown论文里的github仓库 https://github.com/IAIK/meltdown
  * 依次根据论文和仓库中的demo进行实验
  
# 实验原理：
  * 本次实验针对了采用乱序执行的CPU的漏洞，利用了乱序执行中指令并没有真正执行完成而是加载到缓存中没有执行安全检查，但是由于乱序和分支预测提前执行的指令会被丢弃，乱序执行的指令对缓存的操作却不会被重置。meltdown利用了安全检查和乱序执行的空窗期。由于缓存cache比内存速度快许多，加载到缓存中的指令会更快地被CPU执行，因此meltdown利用分支预测，检测出被加载到缓存中的代码，然后替换成自己期望的代码来实现攻击。
  
  * 攻击的源代码:
  
  ![avatar](https://github.com/OSH-2018/4-Huqy518/blob/master/code.png)
  
  * 仓库部分代码分析：
    * sched_yield() : 释放CPU 
    * libkdump_read_tsx() : 以TSX的机制处理中断
    * size_t libkdump_phys_to_virt(size_t addr) : 实现物理地址到虚拟地址的转换
    * size_t libkdump_virt_to_phys(size_t virtual_address) : 实现虚拟地址到物理地址的转换
    * static void flush(void *p) : 清空缓存
    
# 实验步骤
###### 第一步：关闭meltdown补丁和KASLR,然后利用```sudo cpupower frequency-set -g performance```设置CPU频率
 ![avatar](https://github.com/OSH-2018/4-Huqy518/blob/master/IMG_20180702_214310.jpg)
###### 第二步：分别实现demo:
  * demo 1 : test
  ![avatar](https://github.com/OSH-2018/4-Huqy518/blob/master/IMG_20180702_220656.jpg)
  * demo 2 : 关闭KASLR（已通过设置参数关闭)
  * demo 3 : reliablity test
  ![avatar](https://github.com/OSH-2018/4-Huqy518/blob/master/IMG_20180702_213937.jpg)
  * demo 4 : Read physical memory
  ![avatar](https://github.com/OSH-2018/4-Huqy518/blob/master/IMG_20180702_214018.jpg)
  * demo 5 : dump memory
  ![avatar](https://github.com/OSH-2018/4-Huqy518/blob/master/IMG_20180702_220613.jpg)



### reference:
  * Meltdown   Moritz Lipp, Michael Schwarz, Daniel Gruss等
  * https://github.com/IAIK/meltdown
  * https://blog.csdn.net/gjq_1988/article/details/79138505
  * https://blog.hackerchai.com/meltdown-exploit-on-linux-opensource/
  
