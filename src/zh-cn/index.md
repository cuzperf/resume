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
  - icon: fa fa-birthday-cake
    text: 1994.02
    url:
# PDF下载链接
download:
  title: 下载简历
  icon: fas fa-download fa-fw
  url: 陈智鹏的简历.pdf
---

## <i class="fas fa-user-graduate"></i> 教育背景

- 2015.9 ~ 2021.6 复旦大学 方向：基础数学非交换代数 直博（结业，有结业证，无毕业证学位证）
- 2011.9 ~ 2015.7 华东理工大学 专业：数学与应用数学 学历：学士

## <i class="fas fa-briefcase"></i> 工作经历


2021.07.07 ~ 2022.10.24 声网 Agora C++ SDK 开发工程师

- 统计优化：通过类似 RingBuffer 的数据结构，把统计模块 cpu 占比从 2% 降到 0.1%
- 通过 trace 分析出，转线程中 Location 信息占比较大，优化后实测这部分 cpu 占比成原来的 1/3
- 利用内部 trace 工具配合 [perfetto](https://www.ui.perfetto.dev/#!/) 协助分析问题
- log 重构：确保线程安全，分层 loglevel 提前退出，支持私有参数和配置下发，开启 Wformat，规范接口，细节完善，spdlog 改进，完备内部文档。log 模块负责人, reviewer
- 借助 log 和堆栈信息结合汇编和源代码协助处理 crash 和 ANR 等稳定性问题
- 利用 clang 的一些编译选项白盒检测并修复潜在 bug，以及 Asan, Lsan, Msan, Tsan, UBsan 等提前检测可能稳定性问题
- 增加上行音频分段延迟统计功能
- 在特殊版上提供主动增加延迟的功能
- windows arm64 的编译工作（基于 gn-ninja 编译系统）

<div STYLE="page-break-after: always;"></div>

## <i class='fas fa-trophy'></i> 荣誉证书

- 2014.11 ACM-ICPC 国际大学生程序设计竞赛广州赛区银奖（28 名）
- 2014.10 ACM-ICPC 国际大学生程序设计竞赛西安赛区银奖（30 名）
- 2014.08 ACM-ICPC 国际大学生程序设计竞赛上海邀请赛金奖
- 2012.12 全国部分地区大学生物理竞赛（非专业A组）二等奖
- 2012.12 全国大学生数学竞赛上海赛区三等奖

## <i class="fab fa-github"></i> 开源贡献

- 给 [oi-wiki](https://oi-wiki.org/) 贡献过[平行四边形优化DP页面](https://oi-wiki.org/dp/opt/quadrangle/)
- 给 [C++ 白皮书](https://github.com/Cpp-Club/Cxx_HOPL4_zh/commit/7da2e9889b51043f6834322004a24b2e7bad776a) 修了一个逻辑错误
- 完善了当前简历模版 [resume-docs](https://github.com/xaoxuu/resume-docs/commit/966a3e46f6f3e209875547c850b12c1ed972cf8a) 和主题 [hexo-theme-resume](https://github.com/xaoxuu/hexo-theme-resume/commit/cb818740b7912983e58ed025048b0eb9d1b91821)
- 给 [cf-tool](https://github.com/izlyforever/cf-tool/releases/tag/v1.0.5) 提供了最新适配包
- 给 gcc 提交过 constexpr 的 [bug](https://gcc.gnu.org/bugzilla/show_bug.cgi?id=105565)，但由于无法避免就直接关了
- 竞赛级 [cpp 库](https://github.com/izlyforever/cpplibforCP)，并提供[文档](https://izlyforever.github.io/cpplibforCP/)
- 给 [spdlog](https://github.com/gabime/spdlog) 提了线程名相关的 [PR](https://github.com/gabime/spdlog/pull/2417)，但是作者拒绝了

## <i class="fas fa-user-tie"></i> 自我评价

- 熟悉 C99/C++17，码风规范，注重代码质量（在现代编译器的帮助下）
- 能通过 perf/perfetto, WPR/WPA, instruction/speedscope, trace 等工具找出程序瓶颈， 并对其从算法设计、算法实现、多线程等方面作性能调优，并且写出易读且易于编译器优化的代码
- 会一些简单的 Python 使用（用于 gn-ninja 构建系统）
- 全 pc 平台简单的调试解决问题的能力（通过看堆栈和寄存器的值，对照不同 arch 的汇编手册分析）
- 持续写博客，记录总结工作和学习中学到的技术
