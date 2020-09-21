# 记录硬件开源项目  
  
## 唐杉StarryHeavensAbove  
https://birenresearch.github.io/AIChip_Paper_List/  
https://github.com/BirenResearch/AIChip_Paper_List  
  
https://github.com/basicmi  
https://github.com/basicmi/AI-Chip  
https://github.com/basicmi/AI-Articles  
https://mp.weixin.qq.com/s/6sUhseHU5deXgAV4T0W_2A  
https://zhuanlan.zhihu.com/DNN-on-Chip  

## Eyeriss in MIT  
http://eyeriss.mit.edu/tutorial.html  
http://www-mtl.mit.edu/wpmu/tutorial/  

## 芯片验证平台
硬件仿真加速器，例如Mentor的Veloce，Synopsy的ZeBu，Candance的Palladium
基于FPGA原型验证平台：
典型的产品有Synopsys的HAPS系列，HAPS-80
Cadence公司的ProTIum，
S2C公司的Prodigy系列，Single VU440 
亚科鸿宇 VeriTiger-H4000T 
国内的公司如亚科宏宇的VeriTiger系列等。
目前市面上在售的原型平台使用的最大容量FPGA是Xilinx的VU440（Virtex UltraScal 440，20nm工艺），
单颗FPGA芯片可以容纳的芯片门数是26~30Million，一般为了容纳更大的SoC芯片设计，会采用多颗芯片级联。
https://developer.aliyun.com/article/740415

## 新的HLS平台和paper
by Shan Tang linkedin
Do you know with reinforcement learning, the design team at #synopsys can speed physical design by 86%? Isn't the idea of using #AI to build a better AI chip fascinating? Are you ready to challenge Isaac Asimov's Three Laws of Robotics?

Read the latest industry report on the adoption of AI in chip design. Available in Chinese & English: https://bit.ly/30O7HjG

XLS, https://lnkd.in/g22JFeS, a very interesting open-source high-level synthesis project. In parallel, CIRCT (Circuit IR Compilers and Tools) project, https://lnkd.in/g7j-P2Z, is from the software/compiler community trying to re-do EDA tasks with ideas of multi-level IR. Will these new players change something of EDA industry?
Do you know with reinforcement learning, the design team at #synopsys can speed physical design by 86%? Isn't the idea of using #AI to build a better AI chip fascinating? Are you ready to challenge Isaac Asimov's Three Laws of Robotics?
Read the latest industry report on the adoption of AI in chip design. Available in Chinese & English: https://bit.ly/30O7HjG

https://google.github.io/xls/
https://github.com/llvm/circt

by Shan Tang
最近开源EDA和IP领域确实有些新鲜有趣的东西，感觉背后有两大推动力量，RISCV和Google。前者的生态(包括DSL Chisel/FIRRTL，开源工具和IP)。随着ARM的不确定性增大会有更多玩家参与。后者具有超强的软件技术和开源执行力，而且越来越关注硬件。
EDA的核心就是DSL，compiler和verification(包括formal)，加上flow，是软件工程+硬件的domain knowledge，似乎现在的google连后者都不缺了。

Chisel/FIRRTL Hardware Compiler Framework
https://www.chisel-lang.org/

https://stackoverflow.com/questions/53007782/what-benefits-does-chisel-offer-over-classic-hardware-description-languages
What benefits does Chisel offer over classic Hardware Description Languages? [closed]

https://symbiflow.github.io/
SymbiFlow is a fully open source toolchain for the development of FPGAs of multiple vendors. Currently, it targets the Xilinx 7-Series, Lattice iCE40, Lattice ECP5 FPGAs, QuickLogic EOS S3 and is gradually being expanded to provide a comprehensive end-to-end FPGA synthesis flow.


