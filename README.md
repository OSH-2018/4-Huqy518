# 4-Huqy518
4-Huqy518 created by GitHub Classroom
# 实验平台
  * 系统：Ubuntu 16.04
  * CPU：Inter(R) Core(TM) i7-6700HQ
  
# 实验说明：
  * 本次实验直接使用了meltdown论文里的github仓库 https://github.com/IAIK/meltdown
  * 依次根据论文和仓库中的demo进行实验
  
# 实验原理：
  * 本次实验针对了采用乱序执行的CPU的漏洞，利用了乱序执行中指令并没有真正执行完成而是加载
  到缓存中没有执行安全检查但是由于乱序和分支预测提前执行的指令会被丢弃，乱序执行的指令对缓存的操作却不会被重置。meltdown利用了安全检查和乱序执行的空窗期。由于缓存cache比内存速度快许多，加载到缓存中的指令会更快地被CPU执行，因此meltdown利用分支预测，检测出被加载到缓存中的代码，然后替换成自己期望的代码来实现攻击。
  * 攻击的源代码:
  ```
  ```
# 实验步骤
###### 第一步：关闭meltdown补丁和KASLR,然后利用```sudo cpupower frequency-set -g performance```设置CPU频率

###### 第二步：分别实现demo:
  * demo 1 : test
  * demo 2 : 关闭kaslr（已通过设置参数关闭)
  * demo 3 : reliablity test
  * demo 4 : Read physical memory
  * demo 5 : dump memory
