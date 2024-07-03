---
title: '内置加速度计的实用智能手机窃听方案'
date: 2022-09-26 19:13:40
tags: [knowledge]
published: true
hideInList: false
feature: 
isTop: false
---
原文
>Learning-based Practical Smartphone Eavesdropping with Built-in Acceleromete
>>Zhongjie Ba (Zhejiang University and McGill University), Tianhang Zheng (University of Toronto), Xinyu Zhang (Zhejiang University), Zhan Qin (Zhejiang University), Baochun Li (University of Toronto), Xue Liu (McGill University), Kui Ren (Zhejiang University)
>>>Motion sensors on current smartphones have been exploited for audio eavesdropping due to their sensitivity to vibrations. However, this threat is considered low-risk because of two widely acknowledged limitations: First, unlike microphones, motion sensors can only pick up speech signals traveling through a solid medium. Thus the only feasible setup reported previously is to use a smartphone gyroscope to eavesdrop on a loudspeaker placed on the same table. The second limitation comes from a common sense that these sensors can only pick up a narrow band (85-100Hz) of speech signals due to a sampling ceiling of 200Hz. In this paper, we revisit the threat of motion sensors to speech privacy and propose AccelEve, a new side-channel attack that employs a smartphone's accelerometer to eavesdrop on the speaker in the same smartphone. Specifically, it utilizes the accelerometer measurements to recognize the speech emitted by the speaker and to reconstruct the corresponding audio signals. In contrast to previous works, our setup allows the speech signals to always produce strong responses in accelerometer measurements through the shared motherboard, which successfully addresses the first limitation and allows this kind of attacks to penetrate into real-life scenarios. Regarding the sampling rate limitation, contrary to the widely-held belief, we observe up to 500Hz sampling rates in recent smartphones, which almost covers the entire fundamental frequency band (85-255Hz) of adult speech. On top of these pivotal observations, we propose a novel deep learning based system that learns to recognize and reconstruct speech information from the spectrogram representation of acceleration signals. This system employs adaptive optimization on deep neural networks with skip connections using robust and generalizable losses to achieve robust recognition and reconstruction performan

[原文地址](https://www.ndss-symposium.org/ndss-paper/learning-based-practical-smartphone-eavesdropping-with-built-in-accelerometer/)

# 原文大意
由于对振动的敏感性,当前智能手机上的运动传感器已被用于音频窃听.然而,这种威胁被认为是低风险的,因为有两个公认的限制:首先,与麦克风不同,运动传感器只能拾取通过固体介质传播的语音信号.因此,之前报道的唯一可行的设置是使用智能手机陀螺仪来窃听放在同一张桌子上的扬声器.第二个限制来自一个常识,即由于 200Hz 的采样上限,这些传感器只能拾取窄带(85-100Hz)的语音信号.在本文中,我们重新审视了运动传感器对语音隐私的威胁,并提出了 AccelEve,这是一种新的侧信道攻击,它利用智能手机的加速度计窃听同一智能手机中的扬声器.具体来说,它利用加速度计测量来识别扬声器发出的语音并重建相应的音频信号.与之前的工作相比,我们的设置允许语音信号始终通过共享主板在加速度计测量中产生强烈的响应,这成功地解决了第一个限制并使这种攻击渗透到现实生活场景中.关于采样率限制,与广泛持有的看法相反,我们在最近的智能手机中观察到高达 500Hz 的采样率,这几乎涵盖了成人语音的整个基本频段 (85-255Hz).在这些关键观察之上,我们提出了一种新的基于深度学习的系统,该系统学习从加速度信号的频谱图表示中识别和重建语音信息.该系统对具有跳跃连接的深度神经网络采用自适应优化,使用鲁棒且可推广的损失来实现鲁棒的识别和重建性能.广泛的评估证明了我们的攻击在各种设置下的有效性和高精度.