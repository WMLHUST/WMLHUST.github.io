---
title: 对CAP的正确理解
tags: [分布式]
categories: [分布式]
comments: true
date: 2020-05-14 11:06:27
updated: 2020-05-14 11:06:27
---
### CAP
1. C，一致性，多副本一致性，事务一致性等
2. A，可用性
3. P，分区容忍性

### 理解
1. 最大的误解：**CAP可以三选二**    
实际上P是必然存在的，只能在C和A（一致性和可用性）之间权衡。实际中大多是AP或CP系统，很少有CA的系统。
2. AP系统，追求可用性，放弃一致性。比如MySQL主从等。
3. CP系统，追求强一致性，牺牲一定的可用性。raft、zab协议。而此时的一致性，也只是对客户端看来是一致的，对内部看，是最终一致，因为同步数据总需要时间。
4. 对于CA系统，因为要实现A（高可用），就必然有冗余，有冗余就必然存在P。比如MySQL，内部事务实现强一致性C，但是单机无法保证A，单机也不存在网络延迟，因此可以满足P。
5. 只要引入冗余，实现的高可用（A），就一定存在P。如果还想兼顾一致性（C），那么一定不是真的A。**因此实际系统中，总是在CA之间做权衡。放弃某一方，就变成了AP或CP。**