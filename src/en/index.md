---
# Language (Optional)
lang: en
# Site Keywords & Description
keywords: Resume, Hexo
description: 18817337226 &nbsp cuzperf@outlook.com
# Resume Title
resume_title: cuzperf's Resume
# Job Applicant Name
name: 陈智鹏
avatar: ../img/cuzperf.jpg
# Contact
contact:
  - icon: fas fa-globe-asia
    text: cuzperf.cn
    url: https://cuzperf.cn
  # email
  - icon: fas fa-envelope
    text: cuzperf@outlook.com
    url: mailto:cuzperf@outlook.com
  # phone number
  - icon: fas fa-phone-alt
    text: 18817337226
    url: tel:18817337226
# download PDF
download:
  title: download resume
  icon: fas fa-download fa-fw
  url: cuzperf's Resume.pdf
---

## <i class="fas fa-user-graduate"></i> Education

- 2015.9 ~ 2021.6 FDU, Noncommutative Algebra, doctorate in math but __quit__
- 2011.9 ~ 2015.7 ECUST, Math, Bachelor

## <i class="fas fa-briefcase"></i> Work Experience

2021.07.07 ~ 2022.10.24 Agora.io

- Statistical optimization: Through a data structure similar to RingBuffer, the cpu ratio of the statistical module is reduced from 2% to 0.1%
- Through trace analysis, it is found that the location information in the transfer thread that counts. After optimization, the actual measurement of this part of the cpu accounts for 1/3 of the original.
- log refactor: thread-safe, hierarchical loglevel early return, support scrite key and configuration delivery, enable Wformat, specification interface, refine details, refine spdlog, Complete internal documentation
- Use internal trace with [perfetto](https://www.ui.perfetto.dev/#!/) to assist in problem analysis
- Find potential bugs with the help of some complie options of clang. Keep stability in owned to sanitizer like Asan, Lsan, Msan, Tsan, UBsan
- Add feature: big delay in special version
- help fix crash and ANR using log and dump
- fix some bugs report by QA or Customers
- support compile for windows arm64 (base on gn-ninja build system)

<div STYLE="page-break-after: always;"></div>

## <i class='fas fa-trophy'></i> Honor Certificate

- 2014.11 ICPC Silver award (28th places) Guangzhou site
- 2014.10 ICPC Silver award (30th places) Xi'an site
- 2014.08 ICPC Invitational Gold Award Shanghai site

## <i class="fab fa-github"></i> Open Source Contributions

- contribute to [oi-wiki]((https://oi-wiki.org/dp/opt/quadrangle/)) and [Cxx_HOPL4_zh](https://github.com/Cpp-Club/Cxx_HOPL4_zh/commit/7da2e9889b51043f6834322004a24b2e7bad776a)
- contribute to [resume-docs](https://github.com/xaoxuu/resume-docs/commit/966a3e46f6f3e209875547c850b12c1ed972cf8a) and [hexo-theme-resume](https://github.com/xaoxuu/hexo-theme-resume/commit/cb818740b7912983e58ed025048b0eb9d1b91821)
- adapt codeforces new format and language for [cf-tool](https://github.com/izlyforever/cf-tool/releases/tag/v1.0.5)
- report [issue about constexpr](https://gcc.gnu.org/bugzilla/show_bug.cgi?id=105565) to gcc, but closed with unsolved
- write small [cpplib](https://github.com/izlyforever/cpplibforCP) at competition level, and [document](https://izlyforever.github.io/cpplibforCP/)
- [PR](https://github.com/gabime/spdlog/pull/2417) about thread name to [spdlog](https://github.com/gabime/spdlog) but refused

## <i class="fas fa-user-tie"></i> Self-Evaluation

- familiar to C99/C++17, focus on code quality(in owned to modern complier)
- find timeconsuming part using perf/perfetto, WPR/WPA, instruction/speedscope and trace. Write easy-to-read and easy-to-compiler-optimized code
- Know every little about Python(used for gn-ninja build system)
- keep on writing blog
- At this stage, there is still a lot of low-level computer knowledge (such as: network, database) which I am missing. Clear goal of learing and work make me full of hope and confidence in life
- Current goal: Focus on stability and high-performance skills, learn more basic computer knowledge, and strive to become a qualified computer practitioner
