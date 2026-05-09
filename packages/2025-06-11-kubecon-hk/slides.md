---
layout: center
highlighter: shiki
css: unocss
colorSchema: dark
transition: fade-out
title: Taming Dependency Chaos for LLM in K8S
exportFilename: KubeCon HK 2025.06 - Taming Dependency Chaos for LLM in K8S
lineNumbers: false
drawings:
  persist: false
mdc: true
clicks: 0
preload: false
glowSeed: 229
routerMode: hash
---

<div translate-x--14>

<h1 class="cover-cn-title">
  自我介绍及个人技术能力展示
</h1>

<div class="cover-cn-author">汇报人：齐鹏宇</div>

</div>

<div w-full absolute bottom-0 left-0 flex items-center transform="translate-x--10 translate-y--10">
  <div w-full flex items-center justify-end>
    <div class="cover-tech-badge">
      <div class="cover-tech-badge-top">
        <div class="cover-tech-badge-unit">
          <div i-carbon:machine-learning-model class="cover-tech-icon" />
          <div class="cover-tech-unit-title">AI</div>
        </div>
        <div class="cover-tech-divider-vertical"></div>
        <div class="cover-tech-badge-unit">
          <div i-fluent:iot-24-regular class="cover-tech-icon" />
          <div class="cover-tech-unit-title">IoT</div>
        </div>
      </div>
      <div class="cover-tech-badge-bottom">
        <div class="cover-tech-line"></div>
        <div class="cover-tech-meta">China 2026</div>
        <div class="cover-tech-line"></div>
      </div>
    </div>
  </div>
</div>

---
class: py-10
clicks: 3
glow: left
---

<SelfIntroOverview />

<!--
老师们好,接下来我将从3部分来进行我的汇报

第一部分是我的个人背景介绍

第二部分是我的个人综合能力的展示

第三名部分是我个人技术能力的展示
-->

---
layout: center
class: text-center
clicks: 3
---

<EducationSwitch />

<!--
首先是对于我个人的情况进行介绍

本人今年26岁,籍贯是河北保定人,并且政治面貌是共产党员,是大学中同一届中最早成为共产党员的

本人的本科毕业国内的211大学郑州大学,所学的专业是轨道交通信号与控制专业,是自动化方向的专业,主修的课程有电磁场,数电模电,计算机网络和单片机原理等为后续在嵌入式方面的研究打下了基础

之后的研究生就读于世界QS排名前100的南安普顿大学,物联网专业,主修的课程主要包括嵌入式基础,物联网网络,嵌入式处理器等
-->

---
class: p-0
clicks: 2
---

<ComprehensiveAbilitySlide />

<!--
在介绍本人的技术能力之前,首先展示一下本人的综合能力

本人的综合能力概括来说就是

在组织中可以有效的沟通推动协调整个组织的协作.

本人在郑州大学的学习期间曾担任过电气工程学院的学生会主席
在组织安排活动过程中,锻炼的能力有

任务拆解能力:在面对大型任务的时候,可以合理拆解任务,明确任务流程

沟通汇报能力:注重在任务的关键节点进行同步,减少信息不对成造成的问题

过程沉淀能力:在问题解决的过程中,随时保持整理材料,问题复盘,保留记录

可以证明我的工作成果的是每年的校级荣誉和省级优秀学生干部荣誉
-->

---
class: p-0
clicks: 2
---

<ProjectIntroSlide />

<!--
接下来我将通过我最后代表性的项目来展示我的技术能力

这个项目是基于 ESP32-S3 的 AI 语音助手 + 硬件控制完整实现

它是一个跑在 ESP32-S3 上的嵌入式 AI 语音助手，

通过一套叫 MCP 的协议，把云端大模型和本地物理硬件连接起来

让 AI 不只是回答问题，而是能直接调用设备上的功能，

控制舵机转动、设置定时提醒、和 Home Assistant 智能家居系统联动。
-->

---
class: p-0
glowSeed: 175
clicks: 4
---

<ProjectFeatures />

<!--
接下里我要具体展开这个项目,按照系统能力分层来看

[click] 第一层是感知层，负责端侧语音采集、前端处理、编码上传和音频播放，是整个对话系统的输入输出基础。

[click] 第二层是理解与调度层，核心是 MCP 工具拓展，把 AI 的语义意图转换成结构化工具调用。

[click] 第三层是执行与记忆层，负责舵机硬件控制，以及提醒、闹钟等可以持久保存和恢复的本地状态。

[click] 第四层是联动层，包括设备主动触发和 Home Assistant 联动，让设备从单点控制扩展到智能家居生态。
-->

---
class: p-0
glowSeed: 145
clicks: 3
---

<ProjectArchitecture />

<!--
这一页先总览 3 条核心链路：音频处理管道、MCP 协议桥接 AI 与硬件、HA MQTT 链路。

[click] 先看音频处理管道。这里重点说明语音从采集、前端处理、编码上传，到服务器回复后再解码播放，是一条完整的上下行音频链路。

[click] 整个链路分两个阶段：注册阶段（设备启动时一次性）和调用阶段（AI 每次想用工具时）。

注册阶段做的是“用自然语言告诉 AI 这个设备能做什么”。description 字段是用人话写的，AI 直接读懂，这就是“用语言给 AI 编程”。

整个 MCP 链路的关键设计：

第一：JSON-RPC 2.0 是协议骨架。每个消息都有 id，请求和响应通过 id 配对。设备可以并发处理多个调用，不会乱套。

第二：工具描述就是给 AI 的“接口文档”。AddTool 时写的描述质量直接决定 AI 调用的准确性。描述越精确，比如“必须 0-180 整数”“超出范围会报错”，AI 越不会传错参数。

第三：std::thread 隔离工具执行。工具执行可能慢，比如写 NVS、查询硬件状态，如果在主任务跑会阻塞所有事件处理。每个工具调用单独开线程，主任务立刻返回继续处理别的事，保证响应速度。

第四：双向异步。设备不是被动等待，服务器可以发请求让设备执行，设备也可以主动发请求，比如 notifications/tools/list_changed 通知服务器工具列表变了。WebSocket 长连接支持随时双向消息。

MCP 方式是：AI 自主决定调用哪个工具、传什么参数；设备只负责“工具被调用了就执行”，完全不参与语义理解。

所有的“理解”工作都在云端 AI，所有的“执行”工作都在设备端，两者通过结构化的 JSON-RPC 协议传递，这就是 MCP 协议桥接 AI 与硬件的本质。

加新功能时，只需要 AddTool() 注册，设备重启后 AI 自动知道并能调用。这个项目里的 set_servo_angle、add_reminder、delete_a_reminder、cleanup_reminder 都是这样加进来的。

[click] ESP32-S3 设备不只是被 AI 控制，也能接入 Home Assistant，成为智能家居系统里的一个可视化、可联动设备。

首先是初始化阶段，ESP32-S3 启动后会连接 MQTT broker，然后把自己支持的能力注册成 Home Assistant 可以识别的 Feature，比如舵机角度控制。

第一个方向是上行，也就是设备状态上报到 Home Assistant。
比如舵机转到 90 度，设备会通过 state topic 把当前状态发布出去，MQTT broker 再转发给 Home Assistant，最后 HA 面板上的滑块状态也会同步更新。

第二个方向是下行，也就是 Home Assistant 反向控制设备。
比如用户在 HA 面板上把滑块拖到 45 度，HA 会向 set topic 发布控制指令，设备收到后通过 HaMqttBus 做 topic 路由，交给对应的 ServoFeature 处理，最后由 ServoController 控制舵机实际转动。

这条链路不是简单地发一条 MQTT 消息，而是把设备能力抽象成 Feature，再通过 topic 做状态同步和控制分发。

这样做的好处是后续扩展新的家居能力时，不需要重写整套通信逻辑，只需要新增对应的 Feature，就可以接入 Home Assistant 的统一控制体系。
-->

---
class: p-0
glowSeed: 123
clicks: 8
---

<EngineeringJudgmentSlide />

<!--
这一页讲的是：这个项目不只是把代码写出来，更重要的是背后的技术选型和设计取舍。

ESP-IDF 框架：
选 ESP-IDF 而不是 Arduino，是这个项目能做成的前提。
Arduino 的 ESP32 库简单易用，但它屏蔽了关键的底层能力，比如双核任务的精细调度、AFE 音频前端、esp-mqtt 全功能客户端、组件管理器。这些在 Arduino 层很难完整拿到。
所以这里选 ESP-IDF，本质上是选择控制权，而不是只追求易用性。

AFE 音频前端：
选用 AFE 是这个项目里最容易被低估的决策之一。
AFE 不是一个单独算法，而是一整套前端处理流水线：AEC 回声消除、NS 噪声抑制、VAD 语音活动检测、WakeNet 唤醒词检测。
如果不用 AFE 自己实现，每一个模块都可能是几个月到半年的工作量。
一开始其实没有专门做这一层，后来发现两个问题：一是噪声会误触发，在没有唤醒或者说话的时候识别到奇怪的字；二是播放语音时，麦克风会同时监听到扬声器内容。AFE 就是为了解决这些真实问题。

Opus 编码：
对话式 AI 对音频编码有两个看似矛盾的要求：延迟要低，不然对话不流畅；质量要高，不然识别率下降。
原始 PCM 几乎没有编码延迟，但带宽太大，16kHz PCM 大约 32KB/s，对端侧 WiFi 和持续传输都不友好。
Opus 是 WebRTC 标准编码，专门针对实时通信设计。在大约 3KB/s 的带宽下，延迟可以控制在 5-25ms，压缩比约 10:1，人耳基本听不出明显差别。

WebSocket 通信：
WebSocket 最适合这种持续对话场景。
用户说话时音频每 60ms 一帧持续上传，AI 的回复音频也要持续返回，而且整个对话期间连接不能断。这是高频、双向、长连接的需求。
HTTP 短连接每次都要重新握手，延迟受不了；长轮询只是模拟双向通信，资源浪费也更大。
WebSocket 握手一次后保持长连接，协议本身支持文本帧和二进制帧，正好适合语音流和控制消息混合传输。

本地唤醒词检测：
这是隐私、省电、省带宽三赢的设计。
平时用户不说话时，如果一直把麦克风音频送到云端，隐私和流量都不合适。
所以把 WakeNet 唤醒词模型放在本地。每一帧音频先在本地检测，只有匹配唤醒词才建立 WebSocket、开始上传音频、进入对话流程。
这个决策同时解决三个问题：平时不上传，隐私不泄露；WebSocket 懒连接，网络流量几乎为零；唤醒前 CPU 负载低，功耗也低。

NVS Blob 序列化：
提醒数据本质上是少量结构化数据，不适合为了它引入文件系统。
ESP32 上文件系统有掉电损坏风险，尤其是 SPIFFS 在异常掉电时可能留下损坏文件；而 NVS 面向配置数据设计，冷启动读取快，commit 具备事务保护。
用 Blob 整体序列化有几个好处：
第一，Flash 寿命更好，N 条变化可以合并成一次写入；
第二，原子性更好，掉电不会出现半旧半新的提醒列表；
第三，加载更快，一次查询读出整体数据；
第四，schema 演进更方便，加字段时在序列化里加 version 判断即可。

双核任务分配 + 优先级：
这里的关键判断是：Core 0 上 WiFi 驱动任务优先级很高，会持续抢占低优先级任务。
如果音频采集任务跑到 Core 0，每次 WiFi 处理网络包，音频采集就会被打断，累积起来就是音频帧延迟。
所以要把网络密集任务和实时音频任务分开，Core 0 主要承担网络，Core 1 承担业务和实时音频，再通过优先级分层保证音频链路稳定。
-->

---
class: p-0
glowSeed: 180
clicks: 5
---

<EngineeringChallengesSlide />

<!--
第一个案例是唤醒词识别率突然下降。测试到一半发现唤醒词识别率从 95% 掉到 60%，要说两三次“你好小智”才能唤醒。
最初怀疑是 CPU 跑不动，于是加了 vTaskGetRunTimeStats 打印 CPU 占用，发现两个核 IDLE 时间都还有 50% 以上，CPU 不是瓶颈。
接着用 vTaskList 看任务状态分布，注意到 audio_input 任务跑在 Core 0 上，正好和 WiFi 驱动在同一个核。
WiFi 优先级 23 远高于 audio_input 的 8，每次有网络包，audio_input 就被抢占。
单帧音频原本 5ms 能处理完，被抢占后变成 30ms 以上，AFE 累积延迟超过算法容忍阈值，唤醒就漏识别了。
最后把 audio_input 钉到 Core 1，物理隔离 WiFi 抢占，验证后识别率回到 95% 以上。
这个 bug 让我学到：双核不等于自动并行，任务亲和性是要主动设计的。

第二个案例很典型，因为它没有任何错误信息，但功能就是不对。
现象是 HA 面板拖动滑块控制舵机时，舵机有时候不动。日志干干净净，没有任何错误。
我先在 MQTT 的 OnMessage 回调里加日志，发现消息根本没进设备。
然后在 broker 端用 mosquitto_sub 订阅同一个 topic，发现 broker 是收到 HA 消息的，但没有转发给设备。
真相是项目用的 MQTT 是 CleanSession=true，设备断线之后 broker 会清掉所有订阅记录。
设备由于网络抖动会偶尔断线重连，重连这部分 MqttProtocol 自己处理了，看起来一切正常，但重连后没有重新订阅任何 topic。
broker 收到 HA 消息时，发现订阅列表里没有这个设备，就把消息静默丢弃了。
解决方案是在 HaMqttBus 里注册 OnConnected 回调，每次重连成功就遍历所有 Feature 注册过的 topic，全部重订阅。
这个 bug 让我体会到：“没报错”不等于“没出错”。写网络相关代码时，一定要问自己这条路径上的失败会不会被静默吞掉。

第三个案例是长稳问题。设备短时间跑都正常，但运行 3-4 小时后会偶发重启。
串口里看到 Guru Meditation Error，地址通过 idf.py monitor 自动反汇编，定位到一处 malloc 失败。
直接看那行代码看不出问题，它只是普通的内存分配。但“长跑必现”这个特征指向累积性问题，要么内存泄漏，要么内存碎片。
我加了一段调试代码，每 5 秒打印 heap_caps_get_minimum_free_size。这个值表示自开机以来堆内存的历史最低值，比当前空闲值更能反映曾经有多紧张。
跑了一个小时发现 min_heap 持续下降，每小时降几 KB。
顺着这条线索查代码，发现 WebSocket 模块每次重连时 new 一个新对象，但旧对象没有显式释放。
短期看不出来，长期累积后内存碎片严重，最终某次 malloc 拿不到连续空间就崩了。
解决方案是用 unique_ptr 管理重连相关资源，让 RAII 自动析构。
这个案例让我意识到：长稳问题要看趋势，不能只看单次值。min_heap 历史最低值是发现累积性内存问题的有效指标。

最后一个案例是并发问题。这类 bug 最难定位，但也最能体现工程能力。
现象是某些特定操作之后，整个设备完全静止。不是崩溃，崩溃会有 Guru Meditation 报错；它是真的完全不动，串口什么都不打，按键也没反应。
这种“看起来死了但没崩溃”的症状，第一反应应该是死锁。
重启前我用 vTaskList 抓了一份任务状态快照，发现所有相关任务都是 B（Blocked）状态，但 IDLE 任务还在正常跑。
这就是死锁的典型特征：CPU 是空的，IDLE 能跑，但所有业务任务都卡在等锁。
顺着任务状态查到底是哪把锁，定位到 Application::mutex_。
具体场景是：主任务持着 mutex 时，遍历执行回调队列里的 Lambda。其中一个 Lambda 内部又调用 Schedule()，而 Schedule 内部也要拿这把 mutex。
于是主任务自己卡在自己持有的锁上，形成经典的递归锁死锁。
解决方案是改成先在持锁期间把数据移出来，立刻解锁，再执行回调。这样回调内部就算再调 Schedule 也安全。
这个 bug 让我形成一个原则：持锁期间只做最小操作，取数据、改数据，然后立刻解锁，绝对不在持锁期间执行任何外部回调。

[click] 把前面 4 个案例抽象成一套调试方法
这几个问题表面上分别是唤醒不灵敏、HA 控制失效、设备长时间运行后重启，以及整体卡死无响应。

但它们背后其实对应的是同一套调试路径。

第一步是量化现象。
不能只说“不灵敏”“偶尔失效”“卡住了”，而是要把问题转成可以观察的数据，比如唤醒识别率、单帧音频延迟、任务状态、内存最低水位这些指标。

第二步是验证链路。
嵌入式系统的问题通常不只发生在某一行代码里，而是发生在设备、网络、broker、任务调度这些链路之间。所以需要在多个节点打点，确认问题到底断在哪一层。

第三步是定位机制。
真正的根因往往不是表面现象，而是调度抢占、MQTT 订阅丢失、内存生命周期管理、锁竞争这些系统机制。

第四步是沉淀原则。
比如唤醒词问题最后沉淀成任务钉核原则，MQTT 问题沉淀成重连后必须重订阅，内存问题沉淀成 RAII 管理生命周期，死锁问题沉淀成持锁期间只做最小操作。

所以这一页我想表达的是，我对工程问题的理解不是只把 bug 修好，而是通过真实问题把系统机制理解清楚，并把一次问题修复沉淀成后续可以复用的工程原则。
-->

---
class: p-0
glowSeed: 206
clicks: 0
---

<EngineeringTakeawaysSlide />

<!--
这一页是对前面内容的个人能力总结。

我想表达的是：通过学生会经历与端侧 AI 家居项目，我形成了“能组织推进，也能工程落地”的复合型能力。

第一，任务拆解与从 0 到 1 落地能力。这个项目不是在现有项目中做局部修改，而是从需求拆解、技术选型、系统搭建到功能闭环独立推进，把端侧 AI 家居控制系统完整落地。

第二，沟通对齐与协作推进能力。学生会经历和项目推进让我形成了比较稳定的沟通习惯，能主动同步进度、暴露风险、及时汇报问题，减少信息差，保证任务按节点推进。

第三，底层理解与问题定位能力。遇到问题时，我不会只停留在功能表象，而是继续深入任务调度、音频链路、MQTT 会话、内存管理和并发锁机制，用工具逐层定位真实根因。

第四，工程复盘与长期维护能力。我不会把 bug 修复停留在“当前能跑”，而是进一步沉淀成钉核、重订阅、RAII、持锁最小化等设计原则，让系统后续更稳定、更可维护。

所以我想总结的是：我的特点不是只完成一个功能，而是能把任务拆清楚、把进度对齐好、把问题及时汇报出来，并把想法转化成可落地、可维护的工程系统。
-->

---
class: p-0
glowSeed: 229
clicks: 0
---

<div style="position: absolute; inset: 0; width: 100%; height: 100%; overflow: hidden;">
  <div style="position: absolute; left: 50%; top: 48%; transform: translate(-50%, -50%); text-align: center;">
    <div class="font-cn" style="font-size: 56px; font-weight: 700; line-height: 1.12; color: rgba(15,32,51,0.96); letter-spacing: 0; white-space: nowrap;">谢谢观看</div>
    <div class="font-cn" style="margin-top: 18px; font-size: 24px; font-weight: 650; color: rgba(51,65,85,0.72); letter-spacing: 0; white-space: nowrap;">恳请老师批评指正</div>
    <div class="font-cn" style="margin-top: 26px; font-size: 22px; font-weight: 600; color: rgba(100,116,139,0.72); letter-spacing: 0; white-space: nowrap;">齐鹏宇</div>
  </div>

  <div w-full absolute bottom-0 left-0 flex items-center transform="translate-x--10 translate-y--10">
    <div w-full flex items-center justify-end>
      <div class="cover-tech-badge">
        <div class="cover-tech-badge-top">
          <div class="cover-tech-badge-unit">
            <div i-carbon:machine-learning-model class="cover-tech-icon" />
            <div class="cover-tech-unit-title">AI</div>
          </div>
          <div class="cover-tech-divider-vertical"></div>
          <div class="cover-tech-badge-unit">
            <div i-fluent:iot-24-regular class="cover-tech-icon" />
            <div class="cover-tech-unit-title">IoT</div>
          </div>
        </div>
        <div class="cover-tech-badge-bottom">
          <div class="cover-tech-line"></div>
          <div class="cover-tech-meta">China 2026</div>
          <div class="cover-tech-line"></div>
        </div>
      </div>
    </div>
  </div>
</div>
