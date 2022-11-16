---
# 语言 （可选）
lang: zh-cn
# 网页关键词和描述
keywords: 简历, Hexo
description: 18817337226 &nbsp cuzperf@outlook.com
# 简历标题
resume_title: 陈智鹏的简历
# 应聘者姓名
name: 陈智鹏
avatar: ../img/cuzperf.jpg
# 联系方式
contact:
  - icon: fas fa-globe-asia
    text: cuzperf.cn
    url: https://cuzperf.cn
  # 邮箱
  - icon: fas fa-envelope
    text: cuzperf@outlook.com
    url: mailto:cuzperf@outlook.com
  # 电话号码
  - icon: fas fa-phone-alt
    text: 18817337226
    url: tel:18817337226
# PDF下载链接
download:
  title: 我的博客
  icon: fas fa-user-tie
  url: https://cuzperf.cn
---


## <i class="fas fa-user-graduate"></i> 教育背景

- 2015.9 ~ 2021.6 复旦大学 方向：基础数学非交换代数 直博（结业，无双证）
- 2011.9 ~ 2015.7 华东理工大学 专业：数学与应用数学 学历：学士

## <i class="fas fa-briefcase"></i> 工作经历


2021.07.07 ~ 2022.10.24 声网 Agora

- 统计优化：通过类似 RingBuffer 的数据结构，把统计模块 cpu 占比从 2% 降到 0.1%

这个统计模块每 2s 统计一次丢包率，抖动 jitterbuffer, 95% 延迟等一些信息。基本计算为把数据的 seq number 和 receive time 用 map 保存下来，然后根据 map 自带的排序搞定。后来发现接受的到的 seq number 虽然不一定有序，但是每次计算的时间间隔，它们总在一个很小的区间，于是就用 RingBuffer 存当前的 seq，然后在不改变原来逻辑（完善 UT，改完之后 UT 依然正常），优化了 CPU


- 通过 trace 分析出，转线程中 Location 信息占比较大，优化后实测这部分 cpu 占比成原来的 1/3

通过火焰图分析，观察到这里 Location 的一些字符很不合理，然后发现里面有很多不必要的 copy 操作，实测用 shared_ptr（也会有性能消耗） 可以有效降低 CPU


- 利用内部 trace 工具配合 [perfetto](https://www.ui.perfetto.dev/#!/) 协助分析问题

trace perfetto 这一套 google 的方式，除了分析性能外，还可以检测 SDK 从初始化到结束过程中调用时序和调用关系。根据功能定制给出每个模块关心的过程图，协助分析问题

- log 重构：确保线程安全，分层 loglevel 提前退出，支持私有参数和配置下发，开启 Wformat，规范接口，细节完善，spdlog 改进，完备内部文档。

具体说来

- 很多不检测 service 是否为空就直接使用，并且迭代过程中添加了一些功能破坏了线程安全
- 分层 loglevel 提高了性能（主要是想 printf 这种不变参的函数，处理起来比较消耗性能），去掉了一些不必要的 map
- 私有参数和配置下发有效控制客户乱设 loglevel 或者 loglevel 设置不符合预期的情况
- Wformat 有效的控制了开发人员打 log 时候的低级错误（参数不一致，格式不匹配等问题）
- 规范了接口，不必要的接口不向外（SDK开发人员）暴露
- 其它琐碎的细节优化： 文件路径五权限，获取 log 路径，webrtc log 的处理, console log 带时间戳等等
- spdlog: 线程名，buffer 大小根据场景设置
- 内部文档： 架构图，注意事项（分使用者和开发者），常见 loglevel 设置，log 的格式，根据 log 确定向前线程

总体性能改进了 3% 左右

- 借助 log 和堆栈信息结合汇编和源代码协助处理 crash 和 ANR 等稳定性问题

借助 Agora 内部的 Mahatton 功能，聚类，可以快速在客户提供比较少的信息情况下分析问题，不细讲了

- 利用 clang 的一些编译选项白盒检测并修复潜在 bug，以及 Asan, Lsan, Msan, Tsan, UBsan 等提前检测可能稳定性问题


performance-move-const-arg
performance-inefficient-vector-operation
performance-move-constructor-init
performance-unnecessary-copy-initialization
performance-unnecessary-value-param
clang-analyzer-optin.cplusplus.VirtualCall
cppcoreguidelines-avoid-non-const-global-variables

这个属于通用技术： clang 有完整的文档： <https://clang.llvm.org/docs/>, DFsan 不了解（目前还在开发阶段）

- Asan 和 Tsan 不能同时开启
- Asan 2倍速度
- Lsan(内存泄漏)
- Msan(未初始化就读 3 倍内存)
- UBsan 无所谓
- Tsan 5x-15x. 单次不一定能跑出，即使是官方文档中的最简示例


Agora 当前策略： 两个 gn 变量 feature_enable_sanitizer(ci/cd 过 PR), feature_enable_lsanitizer(本地开发人员使用)

- feature_enable_sanitizer： Asan Lsan Msan UBsan
- 发版的时候关闭


- 增加上行音频分段延迟统计功能

上行： 可以快速定位延迟高的原因。从采集开始，前处理，编码，webrtc 转到 sdk，发送到大网前。

下行（别人做的）： 接收到大网数据，转到 webrtc 解码，后处理，准备渲染

- 在特殊版上提供主动增加延迟的功能（远比想象中复杂）

通过 hook 的方式

主动添加延迟是通用场景
在比赛场景、主播打游戏防窥屏场景 delay 上限甚至可能达到 10 分钟
4. 技术设计
Delay 可以从三个地方设置：
发送端（当前选择）
服务器（服务端成本太高，用户量一大，内存直接撑不住）
接收端（不可控 1. 对于不更新的观众端用户无效，更新了反而增加了 delay 并且更吃内存，会导致用户不愿意更新；2. 接收测的播放
延迟由发送测控制也不合理；3. 高端用户能劫持流然后提前播放）
发送端设置 delay存在一个较为无解的问题：例如设置 delay 1 分钟，主播要下播了（关闭直播软件），最后一分钟的流就没了。
如果想要最后的 delay 时长的流，客户可以帮助主播用户根据设置的 delay 管理关闭直播软件的时机。主播自己也可以用其它设备作为观众端判
断最佳下播时刻。
实现策略（hook 方式）：
用一个 queue，里面存放 时间和包，取的时候检测头部 丢进来的时间 + delay 是否 大于 当前时间，若是，则把头部 push 出去（性能
好，不改变线程模型）直到不满足检测条件
用 libevent 进行 mute/unmute，丢给 libevent 去schedule（ AgMajor 线程上），这里不用 queue 的做法是因为 mute/unmute 是单次
行为（无法使用 push 方式）
mute/unmute 跟着 delay 走
delay 大于 1s 是就应该发送周期 I 帧
如果用户设置的 delay 时间过长，会占用过高的内存，会有卡顿问题，目前建议 5 分钟以内，目前 hard code 最多只支持 10 分钟（超
过了按照 10分钟设置）
在有 delay 的情况下，主播用观众端的 app 不能实时预览，在 delay 主播会有不安全感（确保摄像头灯是暗的）
delay 设置只能增加不能减少（中途减少 delay 是不合理行为，会有混音、视频也不知道应该怎么渲染），如果客户这么设置，此次设置
会无效。
muteLocalAudio/disableLocalAudio，video 同理
会不会有多主播，主播之间是否要加延迟，看上去不需要，例如对于赛事解说类也观众，然后自己不加延迟即可
广播包要不要发送延迟（ToDo：广播包里面到底有什么）
要不要搞个 delayWorker 或者 队列
leave channel 是否要推完，mute 的时候要不要关闭摄像头（跟这个关联的一个问题）
采集的时候写到文件，然后直接读音频视频

当时 Agora 对于多主播有其它策略，也影响了此功能


- windows arm64 的编译工作（基于 gn-ninja 编译系统）

- 下载 toolchain： toolchain --addMicrosoft.VisualStudio.Component.VC.Tools.ARM--addMicrosoft.VisualStudio.Component.VC.Tools.ARM6 （VS2019支持）
- gn toolchain 模仿已有 x64 toolchain 写 arm64 版本，一些宏，汇编 a
- 之前 windows 平台都不区分 target_cpu 和 host_cpu，此次交叉编译，就出现很多需要适配的问题
- windows 的一些头文件不支持 arm64
- 下载 prebuilt 资源（x64 先替代）
- 基础库先出 win arm64 版本完成
- ffmpeg 有自己的一套汇编语言的格式，必须用 `clang-cl.exe--target=arm64-windows` 才能编译成功，并且很多 config 也要重新适配
- 一写指令集优化在 win arm64 上无法使用，例如 sse2 avx512 这些向量集优化


## <i class='fas fa-trophy'></i> 荣誉证书

- 2014.11 ACM-ICPC 国际大学生程序设计竞赛广州赛区银奖（28 名）
- 2014.10 ACM-ICPC 国际大学生程序设计竞赛西安赛区银奖（30 名）
- 2014.08 ACM-ICPC 国际大学生程序设计竞赛上海邀请赛金奖
- 2012.12 全国部分地区大学生物理竞赛（非专业A组）二等奖
- 2012.12 全国大学生数学竞赛上海赛区三等奖

## <i class="fab fa-github"></i> 开源贡献

- 给 [oi-wiki](https://oi-wiki.org/) 贡献过[平行四边形优化DP页面](https://oi-wiki.org/dp/opt/quadrangle/)
- 给 [C++ 白皮书](https://github.com/Cpp-Club/Cxx_HOPL4_zh/commit/7da2e9889b51043f6834322004a24b2e7bad776a) 修了一个逻辑错误
- 完善给当前简历模版 [resume-docs](https://github.com/xaoxuu/resume-docs/commit/966a3e46f6f3e209875547c850b12c1ed972cf8a) 和主题 [hexo-theme-resume](https://github.com/xaoxuu/hexo-theme-resume/commit/cb818740b7912983e58ed025048b0eb9d1b91821)
- 给 [cf-tool](https://github.com/izlyforever/cf-tool/releases/tag/v1.0.5) 提供了最新适配包
- 给 gcc 提交过 constexpr 的 [bug](https://gcc.gnu.org/bugzilla/show_bug.cgi?id=105565)，但由于无法避免就直接关了
- 竞赛级 [cpp 库](https://github.com/izlyforever/cpplibforCP)，并提供[文档](https://izlyforever.github.io/cpplibforCP/)
- 给 [spdlog](https://github.com/gabime/spdlog) 提了线程名相关的 [PR](https://github.com/gabime/spdlog/pull/2417)，但是作者拒绝了


## 自我介绍

本科就读与华东理工大学数学系，大学期间参加过 acm 竞赛，拿了两次银奖，2015年本科毕业后报送直博去复旦读基础数学，6年后因个人对研究课题不报希望，与 2021.6 月结业，2021.7 月入职声网 Agora 作 C++ SDK 开发，边工作便学习计算机底层知识。

目前

## <i class="fas fa-user-tie"></i> 自我评价

- 熟悉 C99/C++17，以及各种编译选项，码风规范，注重代码质量（在现代编译器的帮助下）
- 能通过 perf/perfetto, WPR/WPA, instruction/speedscope, trace 等工具找出程序瓶颈， 并对其从算法设计、算法实现、多线程等方面作性能调优，并且写出易读且易于编译器优化的代码
- 会一些简单的 Python 使用（用于 gn-ninja 构建系统）
- 全 pc 平台简单的调试解决问题的能力（通过看堆栈和寄存器的值，对照不同 arch 的汇编手册分析）
- 持续写博客，记录总结工作和学习中学到的技术



## 面试技巧：

- 自我介绍不要卡（提前写好很重要，双语版本）
- 根据简历，写拓展版本，不然介绍起来很麻烦


### 面试官在的做题情况

- 有思路之后可以跟面试官对一下方案，防止对方觉得你是在投机取巧，方式方案不合理然后写的时候花时间
- 面试官一般不说废话，即使你觉得是废话，但是很有可能他是在提示你他想要的方案，然后此时要认真思考慢慢拓展，不要急
- 多考虑内存泄漏，内存的消耗

