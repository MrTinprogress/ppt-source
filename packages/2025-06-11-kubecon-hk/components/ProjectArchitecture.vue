<script setup lang="ts">
import { useSlideContext } from '@slidev/client'
import { computed, ref, watch } from 'vue'

const selected = ref(0)
const { $clicks } = useSlideContext()
const clickLink = computed(() => Math.min(Math.max($clicks.value, 1), 3))
const activeLink = computed(() => selected.value || clickLink.value)

watch($clicks, () => {
  selected.value = 0
})
</script>

<template>
  <section class="project-architecture">
    <header class="project-architecture__header">
      <h1>项目架构：3条核心链路</h1>
      <p>把语音入口、AI 工具协议与家居联动拆成三条可维护的系统链路</p>
    </header>

    <div class="architecture-morph" :class="{ 'architecture-morph--detail': $clicks > 0 }">
      <button
        class="architecture-node architecture-node--audio"
        :class="{ 'architecture-node--active': $clicks > 0 && activeLink === 1 }"
        type="button"
        @click.stop="selected = 1"
      >
        <div class="architecture-node__icon i-carbon:volume-up" />
        <div class="architecture-node__index">01</div>
        <h2>音频处理管道</h2>
        <p>采集、唤醒、播放与语音交互状态管理。</p>
      </button>

      <button
        class="architecture-node architecture-node--mcp"
        :class="{ 'architecture-node--active': $clicks > 0 && activeLink === 2 }"
        type="button"
        @click.stop="selected = 2"
      >
        <div class="architecture-node__icon i-carbon:tool-kit" />
        <div class="architecture-node__index">02</div>
        <h2>MCP 协议桥接 AI 与硬件</h2>
        <p>将模型意图转换为可调用、可扩展的设备工具。</p>
      </button>

      <button
        class="architecture-node architecture-node--mqtt"
        :class="{ 'architecture-node--active': $clicks > 0 && activeLink === 3 }"
        type="button"
        @click.stop="selected = 3"
      >
        <div class="architecture-node__icon i-carbon:network-4" />
        <div class="architecture-node__index">03</div>
        <h2>HA MQTT 链路</h2>
        <p>通过 MQTT 与 Home Assistant 完成状态同步和设备联动。</p>
      </button>
    </div>

    <Transition name="architecture-panel">
      <div v-if="$clicks > 0" class="architecture-detail-panel">
        <article v-show="activeLink === 1" class="architecture-detail-card architecture-detail-card--audio">
          <h2>音频处理管道</h2>
          <div class="architecture-detail-card__tags">
            <span>Core 1 pinned</span>
            <span>16kHz PCM</span>
            <span>Opus 10:1</span>
            <span>Binary Frame</span>
          </div>
          <div class="audio-pipeline">
            <div class="audio-pipeline__section-title">上行链路</div>
            <div class="audio-pipeline__main">
              <div class="audio-pipeline__node" data-layer="感知层">
                <strong>I2S 硬件采集</strong>
                <span>16kHz PCM</span>
              </div>
              <div class="audio-pipeline__link" />
              <div class="audio-pipeline__node audio-pipeline__node--afe" data-layer="前端算法层">
                <strong>AFE 前端处理</strong>
                <span>回声消除 / 降噪 / 唤醒检测</span>
              </div>
              <div class="audio-pipeline__link" />
              <div class="audio-pipeline__node" data-layer="编码层">
                <strong>Opus 编码</strong>
                <span>压缩音频，降低传输带宽</span>
              </div>
              <div class="audio-pipeline__link" />
              <div class="audio-pipeline__node" data-layer="传输层">
                <strong>WebSocket</strong>
                <span>二进制帧 → 服务器</span>
              </div>
            </div>

            <div class="audio-pipeline__afe-row">
              <div class="audio-pipeline__subgraph">
                <div class="audio-pipeline__subnode">AEC<span>消除回声</span></div>
                <div class="audio-pipeline__subnode">NS<span>抑制噪音</span></div>
                <div class="audio-pipeline__subnode">VAD<span>活动检测</span></div>
                <div class="audio-pipeline__subnode">WakeNet<span>唤醒词检测</span></div>
              </div>
            </div>

            <div class="audio-pipeline__section-title audio-pipeline__section-title--down">下行链路</div>
            <div class="audio-pipeline__down">
              <div class="audio-pipeline__down-node" data-layer="输出层">扬声器发声</div>
              <div class="audio-pipeline__down-link" />
              <div class="audio-pipeline__down-node" data-layer="DAC">I2S0 转模拟信号</div>
              <div class="audio-pipeline__down-link" />
              <div class="audio-pipeline__down-node" data-layer="解码层">解码成 PCM</div>
              <div class="audio-pipeline__down-link" />
              <div class="audio-pipeline__down-node" data-layer="解包层">取出 Opus 数据</div>
              <div class="audio-pipeline__down-link" />
              <div class="audio-pipeline__down-node audio-pipeline__down-node--server" data-layer="服务端">
                服务器下发
                <span class="audio-pipeline__down-return"><i /></span>
              </div>
            </div>
          </div>
      </article>

      <article v-show="activeLink === 2" class="architecture-detail-card architecture-detail-card--mcp">
        <h2>MCP 协议桥接 AI 与硬件</h2>
        <div class="architecture-detail-card__tags">
          <span>JSON-RPC 2.0</span>
          <span>Tool Schema</span>
          <span>Request ID</span>
          <span>Async Thread</span>
        </div>
        <div class="mcp-pipeline">
          <div class="mcp-pipeline__section-title">注册阶段：设备启动一次</div>
          <div class="mcp-pipeline__register">
            <div class="mcp-pipeline__node" data-layer="设备层">设备启动</div>
            <div class="mcp-pipeline__link" />
            <div class="mcp-pipeline__node mcp-pipeline__node--tool" data-layer="工具层">各模块调用<span>AddTool 注册工具</span></div>
            <div class="mcp-pipeline__link" />
            <div class="mcp-pipeline__node" data-layer="注册表">McpServer 维护<span>工具表</span></div>
            <div class="mcp-pipeline__link" />
            <div class="mcp-pipeline__node" data-layer="协议层">AI 服务器请求<span>tools/list</span></div>
            <div class="mcp-pipeline__link" />
            <div class="mcp-pipeline__node" data-layer="接口文档">设备返回工具清单<span>名字 / 描述 / 参数</span></div>
            <div class="mcp-pipeline__link" />
            <div class="mcp-pipeline__node" data-layer="模型上下文">AI 缓存<span>工具列表</span></div>
          </div>

          <div class="mcp-pipeline__ready">工具列表已就绪</div>

          <div class="mcp-pipeline__section-title mcp-pipeline__section-title--call">调用阶段：每次用户对话</div>
          <div class="mcp-pipeline__call">
            <div class="mcp-pipeline__node" data-layer="输入">用户说话</div>
            <div class="mcp-pipeline__link" />
            <div class="mcp-pipeline__node" data-layer="会话层">音频上行<span>到 AI 服务器</span></div>
            <div class="mcp-pipeline__link" />
            <div class="mcp-pipeline__node mcp-pipeline__node--model" data-layer="决策层">大模型推理<span>决定调用工具</span></div>
            <div class="mcp-pipeline__link" />
            <div class="mcp-pipeline__node" data-layer="协议调用">tools/call<span>name + arguments</span></div>
            <div class="mcp-pipeline__link" />
            <div class="mcp-pipeline__node" data-layer="传输层">设备 WebSocket<span>收到文本帧</span></div>
            <div class="mcp-pipeline__link" />
            <div class="mcp-pipeline__node mcp-pipeline__node--parse" data-layer="解析层">
              McpServer 解析
              <span>查找工具</span>
              <span class="mcp-pipeline__drop"><i /></span>
            </div>

            <div class="mcp-pipeline__node" data-layer="输出">音频下发<span>用户听到</span></div>
            <div class="mcp-pipeline__link mcp-pipeline__link--left" />
            <div class="mcp-pipeline__node" data-layer="回复生成">AI 收到结果<span>生成自然回复</span></div>
            <div class="mcp-pipeline__link mcp-pipeline__link--left" />
            <div class="mcp-pipeline__node" data-layer="响应配对">返回结果<span>ReplyResult</span></div>
            <div class="mcp-pipeline__link mcp-pipeline__link--left" />
            <div class="mcp-pipeline__node mcp-pipeline__node--hardware" data-layer="执行层">硬件实际动作<span>舵机 / 提醒</span></div>
            <div class="mcp-pipeline__link mcp-pipeline__link--left" />
            <div class="mcp-pipeline__node" data-layer="业务层">lambda 调用<span>业务函数</span></div>
            <div class="mcp-pipeline__link mcp-pipeline__link--left" />
            <div class="mcp-pipeline__node mcp-pipeline__node--thread" data-layer="异步隔离">新建 std::thread<span>执行 lambda</span></div>
          </div>
        </div>
      </article>

      <article v-show="activeLink === 3" class="architecture-detail-card architecture-detail-card--mqtt">
        <h2>HA MQTT 链路</h2>
        <div class="architecture-detail-card__tags">
          <span>MQTT Broker</span>
          <span>State Topic</span>
          <span>Set Topic</span>
          <span>Reconnect</span>
        </div>
        <div class="ha-pipeline">
          <div class="ha-pipeline__section-title">初始化：设备接入 Home Assistant</div>
          <div class="ha-pipeline__row ha-pipeline__row--init">
            <div class="ha-pipeline__node" data-layer="设备层">设备启动</div>
            <div class="ha-pipeline__link" />
            <div class="ha-pipeline__node" data-layer="通信层">连接 MQTT broker</div>
            <div class="ha-pipeline__link" />
            <div class="ha-pipeline__node ha-pipeline__node--register" data-layer="抽象层">RegisterHaFeatures<span>注册 IHaFeature</span></div>
            <div class="ha-pipeline__link" />
            <div class="ha-pipeline__node" data-layer="Topic 映射">订阅 set topic<span>发布 state topic</span></div>
            <div class="ha-pipeline__link" />
            <div class="ha-pipeline__node" data-layer="展示层">HA 面板显示</div>
          </div>

          <div class="ha-pipeline__ready">连接就绪：状态上报与控制下发双向可用</div>

          <div class="ha-pipeline__section-title">上行：设备状态 → HA</div>
          <div class="ha-pipeline__row ha-pipeline__row--up">
            <div class="ha-pipeline__node" data-layer="硬件层">硬件状态变化<span>舵机到 90°</span></div>
            <div class="ha-pipeline__link" />
            <div class="ha-pipeline__node ha-pipeline__node--state" data-layer="Feature 层">ServoFeature<span>PublishState</span></div>
            <div class="ha-pipeline__link" />
            <div class="ha-pipeline__node" data-layer="状态上报">发布 state topic<span>servo/state=90</span></div>
            <div class="ha-pipeline__link" />
            <div class="ha-pipeline__node" data-layer="消息中转">MQTT broker 转发</div>
            <div class="ha-pipeline__link" />
            <div class="ha-pipeline__node" data-layer="可视化">HA 面板<span>滑块更新到 90</span></div>
          </div>

          <div class="ha-pipeline__section-title">下行：HA 控制 → 设备</div>
          <div class="ha-pipeline__row ha-pipeline__row--down">
            <div class="ha-pipeline__node" data-layer="控制入口">HA 滑块拖到 45°</div>
            <div class="ha-pipeline__link" />
            <div class="ha-pipeline__node" data-layer="控制指令">发布 set topic<span>servo/set=45</span></div>
            <div class="ha-pipeline__link" />
            <div class="ha-pipeline__node ha-pipeline__node--dispatch" data-layer="路由层">HaMqttBus.Dispatch<span>按 topic 路由</span></div>
            <div class="ha-pipeline__link" />
            <div class="ha-pipeline__node" data-layer="Feature 层">ServoFeature<span>HandleSet</span></div>
            <div class="ha-pipeline__link" />
            <div class="ha-pipeline__node" data-layer="驱动层">ServoController<span>SetAngle 45</span></div>
            <div class="ha-pipeline__link" />
            <div class="ha-pipeline__node" data-layer="执行线程">servo_task 执行<span>PWM → 舵机</span></div>
          </div>

          <div class="ha-pipeline__note">断线重连：MqttProtocol 自动重连后触发 OnConnected，HaMqttBus 遍历 Feature 重新订阅 set topic，HA 控制恢复。</div>
        </div>
        </article>
      </div>
    </Transition>
  </section>
</template>

<style scoped>
.project-architecture {
  position: absolute;
  inset: 0;
  overflow: hidden;
  font-family: var(--deck-cn-serif);
}

.project-architecture__header {
  position: absolute;
  left: 6%;
  top: 10%;
}

.project-architecture__header h1 {
  margin: 0;
  color: rgba(255, 255, 255, 0.96);
  font-size: 30px;
  font-weight: 700;
  letter-spacing: 0;
  line-height: 1.12;
}

.project-architecture__header p {
  margin: 12px 0 0;
  color: rgba(255, 255, 255, 0.48);
  font-size: 13px;
  font-weight: 600;
  letter-spacing: 0;
}

.architecture-morph {
  position: absolute;
  inset: 0;
  pointer-events: none;
}

.architecture-node {
  position: absolute;
  top: 31%;
  width: calc((86% - 56px) / 3);
  height: 54%;
  overflow: hidden;
  border: 1px solid rgba(14, 165, 233, 0.22);
  border-radius: 18px;
  padding: 26px 28px;
  background:
    radial-gradient(circle at 76% 18%, rgba(125, 211, 252, 0.2), transparent 38%),
    linear-gradient(180deg, rgba(255, 255, 255, 0.72), rgba(240, 249, 255, 0.44));
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.86),
    0 18px 54px rgba(59, 130, 246, 0.13),
    0 0 0 1px rgba(255, 255, 255, 0.34);
  color: inherit;
  cursor: pointer;
  font-family: var(--deck-cn-serif);
  pointer-events: auto;
  text-align: left;
  transition:
    left 900ms cubic-bezier(0.2, 0.85, 0.2, 1),
    top 900ms cubic-bezier(0.2, 0.85, 0.2, 1),
    width 900ms cubic-bezier(0.2, 0.85, 0.2, 1),
    height 900ms cubic-bezier(0.2, 0.85, 0.2, 1),
    padding 900ms cubic-bezier(0.2, 0.85, 0.2, 1),
    border-radius 900ms cubic-bezier(0.2, 0.85, 0.2, 1),
    background 620ms ease,
    border-color 620ms ease,
    box-shadow 620ms ease,
    opacity 620ms ease,
    transform 620ms ease;
}

.architecture-node::after {
  position: absolute;
  right: -18%;
  bottom: -24%;
  width: 70%;
  height: 58%;
  content: "";
  background: radial-gradient(circle, rgba(95, 197, 216, 0.13), rgba(95, 197, 216, 0));
}

.architecture-node--audio {
  left: 7%;
}

.architecture-node--mcp {
  left: calc(7% + ((86% - 56px) / 3) + 28px);
  border-color: rgba(6, 182, 212, 0.22);
  background:
    radial-gradient(circle at 76% 18%, rgba(45, 212, 191, 0.18), transparent 38%),
    linear-gradient(180deg, rgba(255, 255, 255, 0.7), rgba(236, 254, 255, 0.42));
}

.architecture-node--mqtt {
  left: calc(7% + 2 * (((86% - 56px) / 3) + 28px));
  border-color: rgba(99, 102, 241, 0.2);
  background:
    radial-gradient(circle at 76% 18%, rgba(167, 139, 250, 0.16), transparent 38%),
    linear-gradient(180deg, rgba(255, 255, 255, 0.7), rgba(239, 246, 255, 0.42));
}

.architecture-node__icon {
  position: relative;
  z-index: 1;
  color: rgba(255, 255, 255, 0.9);
  font-size: 48px;
  transition:
    font-size 860ms cubic-bezier(0.2, 0.85, 0.2, 1),
    transform 860ms cubic-bezier(0.2, 0.85, 0.2, 1);
}

.architecture-node__index {
  position: absolute;
  top: 24px;
  right: 26px;
  color: rgba(255, 255, 255, 0.24);
  font-size: 24px;
  font-weight: 700;
  transition: opacity 360ms ease;
}

.architecture-node h2 {
  position: relative;
  z-index: 1;
  margin: 28px 0 0;
  color: rgba(255, 255, 255, 0.96);
  font-size: 21px;
  font-weight: 700;
  letter-spacing: 0;
  line-height: 1.25;
  transition:
    opacity 320ms ease,
    transform 520ms ease;
}

.architecture-node p {
  position: relative;
  z-index: 1;
  margin: 14px 0 0;
  color: rgba(255, 255, 255, 0.68);
  font-size: 13px;
  line-height: 1.72;
  transition:
    opacity 320ms ease,
    transform 520ms ease;
}

.architecture-morph--detail .architecture-node {
  left: 6%;
  width: 46px;
  height: 46px;
  padding: 0;
  border-color: rgba(163, 225, 235, 0.16);
  border-radius: 999px;
  background:
    radial-gradient(circle at 50% 18%, rgba(125, 211, 252, 0.18), transparent 42%),
    rgba(255, 255, 255, 0.48);
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.82),
    0 10px 28px rgba(59, 130, 246, 0.12);
  opacity: 0.82;
}

.architecture-morph--detail .architecture-node--audio {
  border-color: rgba(14, 165, 233, 0.34);
  background:
    radial-gradient(circle at 50% 18%, rgba(125, 211, 252, 0.24), transparent 42%),
    rgba(255, 255, 255, 0.58);
}

.architecture-morph--detail .architecture-node--mcp {
  border-color: rgba(6, 182, 212, 0.34);
  background:
    radial-gradient(circle at 50% 18%, rgba(45, 212, 191, 0.24), transparent 42%),
    rgba(255, 255, 255, 0.58);
}

.architecture-morph--detail .architecture-node--mqtt {
  border-color: rgba(99, 102, 241, 0.3);
  background:
    radial-gradient(circle at 50% 18%, rgba(167, 139, 250, 0.22), transparent 42%),
    rgba(255, 255, 255, 0.58);
}

.architecture-morph--detail .architecture-node--audio {
  top: 31%;
}

.architecture-morph--detail .architecture-node--mcp {
  top: calc(31% + 58px);
}

.architecture-morph--detail .architecture-node--mqtt {
  top: calc(31% + 116px);
}

.architecture-morph--detail .architecture-node__icon {
  position: absolute;
  left: 50%;
  top: 50%;
  font-size: 22px;
  transform: translate(-50%, -50%);
}

.architecture-morph--detail .architecture-node__index,
.architecture-morph--detail .architecture-node h2,
.architecture-morph--detail .architecture-node p {
  opacity: 0;
  transform: translateY(12px);
}

.architecture-morph--detail .architecture-node--active {
  color: rgba(255, 255, 255, 0.96);
  border-color: rgba(182, 238, 255, 0.48);
  background:
    radial-gradient(circle at 50% 18%, rgba(139, 231, 238, 0.18), transparent 42%),
    rgba(34, 109, 130, 0.32);
  box-shadow:
    0 0 0 1px rgba(255, 255, 255, 0.08) inset,
    0 10px 28px rgba(34, 142, 184, 0.16),
    0 0 22px rgba(104, 219, 234, 0.2);
  opacity: 1;
  transform: scale(1.08);
}

.architecture-detail-panel {
  position: absolute;
  left: calc(6% + 66px);
  right: 6%;
  top: 25%;
  bottom: 7%;
}

.project-architecture__cards {
  position: absolute;
  left: 7%;
  right: 7%;
  top: 31%;
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 28px;
  height: 54%;
}

.architecture-card {
  position: relative;
  overflow: hidden;
  border: 2px solid rgba(67, 155, 150, 0.5);
  border-radius: 18px;
  padding: 26px 28px;
  background:
    radial-gradient(circle at 78% 18%, rgba(127, 227, 226, 0.14), transparent 34%),
    linear-gradient(180deg, rgba(33, 112, 110, 0.52) 0%, rgba(20, 78, 92, 0.36) 56%, rgba(39, 119, 126, 0.56) 100%);
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.08),
    0 22px 54px rgba(0, 0, 0, 0.22);
}

.architecture-card--mcp {
  border-color: rgba(61, 139, 174, 0.54);
  background:
    radial-gradient(circle at 78% 18%, rgba(116, 190, 236, 0.16), transparent 34%),
    linear-gradient(180deg, rgba(32, 102, 128, 0.54) 0%, rgba(20, 80, 108, 0.38) 56%, rgba(45, 114, 144, 0.58) 100%);
}

.architecture-card--mqtt {
  border-color: rgba(52, 112, 178, 0.56);
  background:
    radial-gradient(circle at 78% 18%, rgba(113, 172, 246, 0.16), transparent 34%),
    linear-gradient(180deg, rgba(35, 94, 139, 0.56) 0%, rgba(23, 74, 112, 0.4) 56%, rgba(47, 105, 158, 0.6) 100%);
}

.architecture-card::after {
  position: absolute;
  right: -18%;
  bottom: -24%;
  width: 70%;
  height: 58%;
  content: "";
  background: radial-gradient(circle, rgba(95, 197, 216, 0.16), rgba(95, 197, 216, 0));
}

.architecture-card__icon {
  color: rgba(255, 255, 255, 0.9);
  font-size: 48px;
}

.architecture-card__index {
  position: absolute;
  top: 24px;
  right: 26px;
  color: rgba(255, 255, 255, 0.26);
  font-size: 24px;
  font-weight: 700;
}

.architecture-card h2 {
  position: relative;
  z-index: 1;
  margin: 28px 0 0;
  color: rgba(255, 255, 255, 0.96);
  font-size: 21px;
  font-weight: 700;
  letter-spacing: 0;
  line-height: 1.25;
}

.architecture-card p {
  position: relative;
  z-index: 1;
  margin: 14px 0 0;
  color: rgba(255, 255, 255, 0.68);
  font-size: 13px;
  line-height: 1.72;
}

.architecture-detail {
  position: absolute;
  left: 6%;
  right: 6%;
  top: 31%;
  bottom: 12%;
  display: grid;
  grid-template-columns: 72px minmax(0, 1fr);
  gap: 22px;
}

.architecture-rail {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 16px;
}

.architecture-rail__item {
  width: 56px;
  height: 56px;
  border: 1px solid rgba(163, 225, 235, 0.16);
  border-radius: 999px;
  background:
    radial-gradient(circle at 50% 18%, rgba(111, 214, 224, 0.08), transparent 42%),
    rgba(18, 70, 88, 0.18);
  color: rgba(255, 255, 255, 0.5);
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: var(--deck-cn-serif);
  transition:
    opacity 280ms ease,
    transform 280ms ease,
    border-color 280ms ease,
    background 280ms ease,
    box-shadow 280ms ease;
}

.architecture-rail__item span:not(.architecture-rail__icon) {
  display: none;
}

.architecture-rail__item--active {
  color: rgba(255, 255, 255, 0.96);
  border-color: rgba(182, 238, 255, 0.48);
  background:
    radial-gradient(circle at 50% 18%, rgba(139, 231, 238, 0.18), transparent 42%),
    rgba(34, 109, 130, 0.32);
  box-shadow:
    0 0 0 1px rgba(255, 255, 255, 0.08) inset,
    0 10px 28px rgba(34, 142, 184, 0.16),
    0 0 22px rgba(104, 219, 234, 0.2);
  transform: translateX(4px) scale(1.08);
}

.architecture-rail__icon {
  font-size: 27px;
}

.architecture-detail-card {
  position: relative;
  box-sizing: border-box;
  height: 100%;
  overflow: hidden;
  border: 2px solid rgba(79, 164, 175, 0.52);
  border-radius: 20px;
  padding: 16px 24px;
  background:
    radial-gradient(circle at 82% 18%, rgba(120, 225, 232, 0.15), transparent 32%),
    linear-gradient(180deg, rgba(29, 101, 109, 0.62), rgba(18, 71, 91, 0.46));
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.1),
    0 24px 60px rgba(0, 0, 0, 0.24);
}

.architecture-detail-card--mcp {
  border-color: rgba(72, 148, 188, 0.54);
  background:
    radial-gradient(circle at 82% 18%, rgba(124, 196, 245, 0.16), transparent 32%),
    linear-gradient(180deg, rgba(30, 95, 130, 0.64), rgba(19, 73, 106, 0.48));
}

.architecture-detail-card--mqtt {
  border-color: rgba(62, 124, 196, 0.56);
  background:
    radial-gradient(circle at 82% 18%, rgba(123, 181, 255, 0.16), transparent 32%),
    linear-gradient(180deg, rgba(34, 88, 139, 0.66), rgba(21, 68, 112, 0.5));
}

.architecture-detail-card__eyebrow {
  color: rgba(255, 255, 255, 0.48);
  font-size: 15px;
  font-weight: 700;
}

.architecture-detail-card h2 {
  max-width: 38%;
  margin: 0;
  color: rgba(255, 255, 255, 0.96);
  font-size: 16px;
  font-weight: 700;
  line-height: 1.22;
}

.architecture-detail-card__tags {
  position: absolute;
  right: 24px;
  top: 15px;
  z-index: 3;
  display: flex;
  flex-wrap: wrap;
  justify-content: flex-end;
  gap: 5px;
  max-width: 62%;
}

.architecture-detail-card__tags span {
  display: inline-flex;
  align-items: center;
  min-height: 17px;
  padding: 2px 7px;
  border: 1px solid rgba(149, 218, 235, 0.26);
  border-radius: 999px;
  background: rgba(7, 30, 45, 0.24);
  color: rgba(205, 238, 246, 0.8);
  font-family: 'Inter', 'Noto Sans SC', sans-serif;
  font-size: 6.6px;
  font-weight: 750;
  letter-spacing: 0.02em;
  line-height: 1;
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.08),
    0 0 12px rgba(98, 210, 235, 0.08);
}

.architecture-detail-card p {
  max-width: 760px;
  margin: 14px 0 0;
  color: rgba(255, 255, 255, 0.72);
  font-size: 14px;
  line-height: 1.72;
}

.audio-pipeline {
  position: absolute;
  left: 20px;
  right: 20px;
  top: 48px;
  bottom: 14px;
  display: grid;
  grid-template-rows: auto 1.25fr 1fr auto 1fr;
  align-items: stretch;
  gap: 10px;
  min-height: 0;
  padding: 10px 12px;
  border: 1px solid rgba(255, 255, 255, 0.11);
  border-radius: 14px;
  background: rgba(6, 22, 34, 0.2);
}

.audio-pipeline__section-title {
  color: rgba(188, 230, 238, 0.72);
  font-size: 9px;
  font-weight: 750;
  line-height: 1;
}

.audio-pipeline__section-title--down {
  margin-top: 2px;
}

.audio-pipeline__main {
  display: grid;
  grid-template-columns: minmax(86px, 1fr) 28px minmax(106px, 1.08fr) 28px minmax(96px, 1fr) 28px minmax(92px, 1fr);
  align-items: center;
  align-self: stretch;
  gap: 0;
  width: 100%;
}

.audio-pipeline__node {
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 58px;
  padding: 12px 7px 6px;
  border: 1px solid rgba(161, 226, 238, 0.22);
  border-radius: 10px;
  background: rgba(8, 24, 38, 0.36);
  color: rgba(255, 255, 255, 0.92);
  line-height: 1.25;
  text-align: center;
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.06),
    0 0 16px rgba(112, 214, 232, 0.08);
}

.audio-pipeline__node strong {
  font-size: 10.2px;
  font-weight: 750;
}

.audio-pipeline__node span {
  margin-top: 3px;
  color: rgba(204, 230, 235, 0.7);
  font-size: 7.4px;
  font-weight: 650;
}

.audio-pipeline__node[data-layer]::before,
.audio-pipeline__down-node[data-layer]::before,
.mcp-pipeline__node[data-layer]::before,
.ha-pipeline__node[data-layer]::before {
  position: absolute;
  left: 7px;
  top: 5px;
  content: attr(data-layer);
  color: rgba(125, 211, 252, 0.72);
  font-family: 'Inter', 'Noto Sans SC', sans-serif;
  font-size: 4.9px;
  font-weight: 800;
  letter-spacing: 0.03em;
  line-height: 1;
}

.audio-pipeline__node--afe {
  position: relative;
}

.audio-pipeline__node--afe::after {
  position: absolute;
  left: 50%;
  top: calc(100% - 1px);
  width: 2px;
  height: 62px;
  content: "";
  background: rgba(185, 229, 239, 0.58);
  box-shadow: 0 0 8px rgba(115, 217, 235, 0.28);
  transform: translateX(-50%);
}

@keyframes pipeline-glow-right {
  0% {
    opacity: 0;
    transform: translate(-50%, -50%) translateX(-18px);
  }

  22% {
    opacity: 1;
  }

  100% {
    opacity: 0;
    transform: translate(-50%, -50%) translateX(18px);
  }
}

@keyframes pipeline-glow-left {
  0% {
    opacity: 0;
    transform: translate(-50%, -50%) translateX(18px);
  }

  22% {
    opacity: 1;
  }

  100% {
    opacity: 0;
    transform: translate(-50%, -50%) translateX(-18px);
  }
}

@keyframes pipeline-glow-down {
  0% {
    opacity: 0;
    transform: translateX(-50%) translateY(-16px);
  }

  22% {
    opacity: 1;
  }

  100% {
    opacity: 0;
    transform: translateX(-50%) translateY(86px);
  }
}

@keyframes audio-return-glow-down {
  0% {
    opacity: 0;
    transform: translateX(-50%) translateY(-12px);
  }

  18% {
    opacity: 1;
  }

  100% {
    opacity: 0;
    transform: translateX(-50%) translateY(124px);
  }
}

.audio-pipeline__link {
  position: relative;
  align-self: center;
  overflow: hidden;
  min-width: 24px;
  height: 2px;
  background: rgba(185, 229, 239, 0.76);
  box-shadow: 0 0 10px rgba(115, 217, 235, 0.34);
}

.audio-pipeline__link::before {
  position: absolute;
  left: 50%;
  top: 50%;
  width: 14px;
  height: 4px;
  content: "";
  border-radius: 999px;
  background: rgba(230, 255, 255, 0.95);
  box-shadow:
    0 0 8px rgba(145, 235, 248, 0.95),
    0 0 16px rgba(92, 206, 230, 0.58);
  transform: translate(-50%, -50%);
  animation: pipeline-glow-right 1.45s linear infinite;
}

.audio-pipeline__link::after {
  position: absolute;
  right: -1px;
  top: 50%;
  width: 7px;
  height: 7px;
  content: "";
  border-top: 2px solid rgba(185, 229, 239, 0.9);
  border-right: 2px solid rgba(185, 229, 239, 0.9);
  filter: drop-shadow(0 0 4px rgba(115, 217, 235, 0.42));
  transform: translateY(-50%) rotate(45deg);
}

.audio-pipeline__afe-row {
  position: relative;
  display: grid;
  grid-template-columns: minmax(86px, 1fr) 28px minmax(106px, 1.08fr) 28px minmax(96px, 1fr) 28px minmax(92px, 1fr);
  align-self: stretch;
  align-items: start;
  margin-top: 0;
  padding-top: 38px;
  width: 100%;
}

.audio-pipeline__subgraph {
  position: relative;
  grid-column: 3;
  display: grid;
  grid-template-columns: repeat(4, minmax(0, 1fr));
  gap: 3px;
  width: 100%;
}

.audio-pipeline__subgraph::before {
  content: none;
}

.audio-pipeline__subgraph::after {
  position: absolute;
  left: 8%;
  right: 8%;
  top: -2px;
  height: 2px;
  content: "";
  background: rgba(185, 229, 239, 0.48);
  box-shadow: 0 0 8px rgba(115, 217, 235, 0.24);
}

.audio-pipeline__subnode {
  min-height: 32px;
  padding: 3px 3px;
  border: 1px solid rgba(161, 226, 238, 0.18);
  border-radius: 6px;
  background: rgba(255, 255, 255, 0.06);
  color: rgba(255, 255, 255, 0.88);
  font-size: 6.8px;
  font-weight: 750;
  line-height: 1.18;
  text-align: center;
  box-shadow: 0 0 10px rgba(112, 214, 232, 0.06);
}

.audio-pipeline__subnode span {
  display: block;
  margin-top: 1px;
  color: rgba(208, 229, 236, 0.68);
  font-size: 5.4px;
  font-weight: 600;
}

.audio-pipeline__down {
  position: relative;
  display: grid;
  grid-template-columns: minmax(58px, 1fr) 18px minmax(72px, 1.05fr) 18px minmax(58px, 1fr) 18px minmax(66px, 1fr) 18px minmax(58px, 1fr);
  align-items: center;
  align-self: stretch;
  width: 100%;
}

.audio-pipeline__down-return {
  position: absolute;
  left: 50%;
  bottom: calc(100% - 1px);
  width: 2px;
  height: 128px;
  content: "";
  overflow: hidden;
  background: rgba(185, 229, 239, 0.72);
  box-shadow:
    0 0 8px rgba(115, 217, 235, 0.46),
    0 0 18px rgba(73, 194, 222, 0.22);
  transform: translateX(-50%);
}

.audio-pipeline__down-return::after {
  content: none;
}

.audio-pipeline__down-return i {
  position: absolute;
  left: 50%;
  top: 0;
  width: 4px;
  height: 16px;
  border-radius: 999px;
  background: rgba(230, 255, 255, 0.95);
  box-shadow:
    0 0 9px rgba(145, 235, 248, 0.96),
    0 0 18px rgba(92, 206, 230, 0.6);
  transform: translateX(-50%);
  animation: audio-return-glow-down 1.45s linear infinite;
}

.audio-pipeline__down-node {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 42px;
  padding: 10px 5px 4px;
  border: 1px solid rgba(161, 226, 238, 0.18);
  border-radius: 8px;
  background: rgba(8, 24, 38, 0.28);
  color: rgba(255, 255, 255, 0.84);
  font-size: 7.2px;
  font-weight: 700;
  line-height: 1.18;
  text-align: center;
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.04),
    0 0 10px rgba(112, 214, 232, 0.06);
}

.audio-pipeline__down-link {
  position: relative;
  overflow: hidden;
  min-width: 16px;
  height: 2px;
  background: rgba(185, 229, 239, 0.68);
  box-shadow: 0 0 8px rgba(115, 217, 235, 0.3);
}

.audio-pipeline__down-link::before {
  position: absolute;
  left: 50%;
  top: 50%;
  width: 12px;
  height: 4px;
  content: "";
  border-radius: 999px;
  background: rgba(230, 255, 255, 0.9);
  box-shadow:
    0 0 7px rgba(145, 235, 248, 0.9),
    0 0 14px rgba(92, 206, 230, 0.52);
  transform: translate(-50%, -50%);
  animation: pipeline-glow-left 1.45s linear infinite;
}

.audio-pipeline__down-link::after {
  position: absolute;
  left: -1px;
  top: 50%;
  width: 5px;
  height: 5px;
  content: "";
  border-left: 2px solid rgba(185, 229, 239, 0.82);
  border-bottom: 2px solid rgba(185, 229, 239, 0.82);
  filter: drop-shadow(0 0 4px rgba(115, 217, 235, 0.42));
  transform: translateY(-50%) rotate(45deg);
}

.mcp-pipeline {
  position: absolute;
  left: 20px;
  right: 20px;
  top: 48px;
  bottom: 14px;
  display: grid;
  grid-template-rows: auto 1fr auto auto 1.65fr;
  align-items: stretch;
  gap: 8px;
  min-height: 0;
  padding: 10px 12px;
  border: 1px solid rgba(255, 255, 255, 0.11);
  border-radius: 14px;
  background: rgba(6, 22, 34, 0.2);
}

.mcp-pipeline__section-title {
  color: rgba(188, 230, 238, 0.72);
  font-size: 9px;
  font-weight: 750;
  line-height: 1;
}

.mcp-pipeline__section-title--call {
  margin-top: 1px;
}

.mcp-pipeline__register,
.mcp-pipeline__call {
  display: grid;
  grid-template-columns: minmax(52px, 1fr) 14px minmax(62px, 1.1fr) 14px minmax(62px, 1.1fr) 14px minmax(62px, 1.1fr) 14px minmax(66px, 1.15fr) 14px minmax(52px, 1fr);
  align-items: center;
  align-self: stretch;
  width: 100%;
}

.mcp-pipeline__call {
  align-content: space-between;
  row-gap: 34px;
}

.mcp-pipeline__node {
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 42px;
  padding: 12px 5px 5px;
  border: 1px solid rgba(161, 226, 238, 0.18);
  border-radius: 8px;
  background: rgba(8, 24, 38, 0.3);
  color: rgba(255, 255, 255, 0.88);
  font-size: 7.4px;
  font-weight: 750;
  line-height: 1.15;
  text-align: center;
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.04),
    0 0 10px rgba(112, 214, 232, 0.06);
}

.mcp-pipeline__node > span:not(.mcp-pipeline__drop) {
  display: block;
  margin-top: 1px;
  color: rgba(208, 229, 236, 0.68);
  font-size: 5.4px;
  font-weight: 600;
}

.mcp-pipeline__node--tool {
  border-color: rgba(143, 229, 255, 0.28);
  background: rgba(35, 109, 127, 0.42);
}

.mcp-pipeline__node--model {
  border-color: rgba(145, 224, 176, 0.28);
  background: rgba(42, 102, 68, 0.35);
}

.mcp-pipeline__node--thread {
  border-color: rgba(246, 203, 131, 0.3);
  background: rgba(115, 82, 35, 0.35);
}

.mcp-pipeline__node--hardware {
  border-color: rgba(246, 151, 151, 0.3);
  background: rgba(117, 48, 55, 0.34);
}

.mcp-pipeline__link {
  position: relative;
  overflow: hidden;
  min-width: 14px;
  height: 2px;
  background: rgba(185, 229, 239, 0.68);
  box-shadow: 0 0 8px rgba(115, 217, 235, 0.3);
}

.mcp-pipeline__link::before {
  position: absolute;
  left: 50%;
  top: 50%;
  width: 11px;
  height: 4px;
  content: "";
  border-radius: 999px;
  background: rgba(230, 255, 255, 0.9);
  box-shadow:
    0 0 7px rgba(145, 235, 248, 0.9),
    0 0 14px rgba(92, 206, 230, 0.52);
  transform: translate(-50%, -50%);
  animation: pipeline-glow-right 1.45s linear infinite;
}

.mcp-pipeline__link::after {
  position: absolute;
  right: -1px;
  top: 50%;
  width: 5px;
  height: 5px;
  content: "";
  border-top: 2px solid rgba(185, 229, 239, 0.84);
  border-right: 2px solid rgba(185, 229, 239, 0.84);
  filter: drop-shadow(0 0 4px rgba(115, 217, 235, 0.42));
  transform: translateY(-50%) rotate(45deg);
}

.mcp-pipeline__link--left::before {
  animation-name: pipeline-glow-left;
}

.mcp-pipeline__link--left::after {
  left: -1px;
  right: auto;
  border: 0;
  border-left: 2px solid rgba(185, 229, 239, 0.84);
  border-bottom: 2px solid rgba(185, 229, 239, 0.84);
  transform: translateY(-50%) rotate(45deg);
}

.mcp-pipeline__drop {
  position: absolute;
  left: 50%;
  top: 100%;
  overflow: hidden;
  width: 2px;
  height: 92px;
  background: rgba(185, 229, 239, 0.68);
  box-shadow:
    0 0 8px rgba(115, 217, 235, 0.42),
    0 0 16px rgba(73, 194, 222, 0.2);
  transform: translateX(-50%);
}

.mcp-pipeline__drop::after {
  content: none;
}

.mcp-pipeline__drop i {
  position: absolute;
  left: 50%;
  top: 0;
  width: 4px;
  height: 14px;
  border-radius: 999px;
  background: rgba(230, 255, 255, 0.92);
  box-shadow:
    0 0 8px rgba(145, 235, 248, 0.92),
    0 0 16px rgba(92, 206, 230, 0.56);
  animation: pipeline-glow-down 1.45s linear infinite;
}

.mcp-pipeline__ready {
  align-self: center;
  padding: 2px 10px;
  border: 1px dashed rgba(185, 229, 239, 0.34);
  border-radius: 999px;
  color: rgba(208, 229, 236, 0.66);
  font-size: 6.4px;
  font-weight: 650;
  line-height: 1.15;
}

.ha-pipeline {
  position: absolute;
  left: 20px;
  right: 20px;
  top: 46px;
  bottom: 12px;
  display: grid;
  grid-template-rows: auto 1fr auto auto 1fr auto 1fr auto;
  align-items: stretch;
  gap: 8px;
  min-height: 0;
  padding: 11px 12px;
  border: 1px solid rgba(255, 255, 255, 0.11);
  border-radius: 14px;
  background: rgba(6, 22, 34, 0.2);
}

.ha-pipeline__section-title {
  color: rgba(188, 230, 238, 0.72);
  font-size: 9px;
  font-weight: 750;
  line-height: 1;
}

.ha-pipeline__row {
  display: grid;
  align-items: center;
  align-self: stretch;
  width: 100%;
}

.ha-pipeline__row--init,
.ha-pipeline__row--up {
  grid-template-columns: minmax(70px, 1fr) 18px minmax(86px, 1.12fr) 18px minmax(96px, 1.18fr) 18px minmax(92px, 1.14fr) 18px minmax(76px, 1fr);
}

.ha-pipeline__row--down {
  grid-template-columns: minmax(70px, 1fr) 18px minmax(82px, 1.08fr) 18px minmax(92px, 1.16fr) 18px minmax(78px, 1fr) 18px minmax(84px, 1.08fr) 18px minmax(76px, 1fr);
}

.ha-pipeline__node {
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 46px;
  padding: 12px 6px 5px;
  border: 1px solid rgba(161, 226, 238, 0.18);
  border-radius: 8px;
  background: rgba(8, 24, 38, 0.3);
  color: rgba(255, 255, 255, 0.88);
  font-size: 7.6px;
  font-weight: 750;
  line-height: 1.16;
  text-align: center;
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.04),
    0 0 10px rgba(112, 214, 232, 0.06);
}

.ha-pipeline__node > span:not(.ha-pipeline__drop) {
  display: block;
  margin-top: 1px;
  color: rgba(208, 229, 236, 0.68);
  font-size: 5.4px;
  font-weight: 600;
}

.ha-pipeline__node--register {
  border-color: rgba(143, 229, 255, 0.28);
  background: rgba(35, 109, 127, 0.42);
}

.ha-pipeline__node--state {
  border-color: rgba(246, 203, 131, 0.3);
  background: rgba(115, 82, 35, 0.35);
}

.ha-pipeline__node--dispatch {
  border-color: rgba(246, 151, 151, 0.3);
  background: rgba(117, 48, 55, 0.34);
}

.ha-pipeline__link {
  position: relative;
  overflow: hidden;
  min-width: 16px;
  height: 2px;
  background: rgba(185, 229, 239, 0.68);
  box-shadow: 0 0 8px rgba(115, 217, 235, 0.3);
}

.ha-pipeline__link::before {
  position: absolute;
  left: 50%;
  top: 50%;
  width: 12px;
  height: 4px;
  content: "";
  border-radius: 999px;
  background: rgba(230, 255, 255, 0.9);
  box-shadow:
    0 0 7px rgba(145, 235, 248, 0.9),
    0 0 14px rgba(92, 206, 230, 0.52);
  transform: translate(-50%, -50%);
  animation: pipeline-glow-right 1.45s linear infinite;
}

.ha-pipeline__link::after {
  position: absolute;
  right: -1px;
  top: 50%;
  width: 5px;
  height: 5px;
  content: "";
  border-top: 2px solid rgba(185, 229, 239, 0.84);
  border-right: 2px solid rgba(185, 229, 239, 0.84);
  filter: drop-shadow(0 0 4px rgba(115, 217, 235, 0.42));
  transform: translateY(-50%) rotate(45deg);
}

.ha-pipeline__ready {
  align-self: center;
  padding: 2px 11px;
  border: 1px dashed rgba(185, 229, 239, 0.34);
  border-radius: 999px;
  color: rgba(208, 229, 236, 0.66);
  font-size: 6.2px;
  font-weight: 650;
  line-height: 1.15;
}

.ha-pipeline__note {
  align-self: flex-end;
  max-width: 520px;
  padding: 5px 10px;
  border: 1px solid rgba(145, 224, 176, 0.22);
  border-radius: 999px;
  background: rgba(42, 102, 68, 0.16);
  color: rgba(208, 229, 236, 0.68);
  font-size: 6px;
  font-weight: 650;
  line-height: 1.28;
}

.architecture-flow {
  position: absolute;
  right: 34px;
  bottom: 34px;
  left: 34px;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 12px;
  min-height: 104px;
  border-radius: 16px;
  background: rgba(255, 255, 255, 0.07);
  border: 1px solid rgba(255, 255, 255, 0.12);
  color: rgba(255, 255, 255, 0.88);
  font-size: 15px;
  font-weight: 700;
}

.architecture-flow span {
  padding: 9px 13px;
  border-radius: 999px;
  background: rgba(8, 24, 38, 0.32);
  white-space: nowrap;
}

.architecture-flow b {
  color: rgba(183, 237, 255, 0.78);
  font-size: 20px;
}

.architecture-panel-enter-active,
.architecture-panel-leave-active {
  transition:
    opacity 420ms ease,
    transform 420ms ease,
    filter 420ms ease;
}

.architecture-panel-enter-from,
.architecture-panel-leave-to {
  opacity: 0;
  filter: blur(8px);
  transform: translateX(34px);
}

.architecture-mode-enter-active,
.architecture-mode-leave-active {
  transition:
    opacity 560ms cubic-bezier(0.2, 0.8, 0.2, 1),
    transform 560ms cubic-bezier(0.2, 0.8, 0.2, 1),
    filter 560ms cubic-bezier(0.2, 0.8, 0.2, 1);
}

.architecture-mode-enter-from {
  opacity: 0;
  filter: blur(10px);
  transform: translateX(-220px) scale(0.28);
  transform-origin: 6% 48%;
}

.architecture-mode-leave-to {
  opacity: 0.24;
  filter: blur(10px);
  transform: translateX(-430px) scale(0.16);
  transform-origin: 6% 48%;
}

/* Light theme typography colors */
.project-architecture {
  color: #0f172a;
}

.project-architecture__header h1 {
  color: #0f2033 !important;
  font-family: 'Noto Sans SC', 'PingFang SC', 'Microsoft YaHei', sans-serif;
  font-weight: 780;
  text-shadow: 0 10px 34px rgba(96, 165, 250, 0.18);
}

.project-architecture__header p {
  color: rgba(51, 65, 85, 0.76) !important;
  font-weight: 650;
}

.architecture-node,
.architecture-card,
.architecture-detail-card,
.audio-pipeline,
.mcp-pipeline,
.ha-pipeline,
.architecture-flow {
  color: rgba(15, 32, 51, 0.9) !important;
}

.architecture-node__icon,
.architecture-card__icon,
.architecture-rail__icon {
  color: rgba(2, 132, 199, 0.84) !important;
}

.architecture-node__index,
.architecture-card__index {
  color: rgba(2, 132, 199, 0.24) !important;
}

.architecture-node h2,
.architecture-card h2,
.architecture-detail-card h2,
.audio-pipeline__node strong,
.audio-pipeline__subnode,
.audio-pipeline__down-node,
.mcp-pipeline__node,
.ha-pipeline__node,
.architecture-flow span {
  color: rgba(15, 32, 51, 0.94) !important;
}

.architecture-node p,
.architecture-card p,
.architecture-detail-card p,
.audio-pipeline__node span,
.audio-pipeline__subnode span,
.mcp-pipeline__node > span:not(.mcp-pipeline__drop),
.ha-pipeline__node > span:not(.ha-pipeline__drop),
.architecture-flow b {
  color: rgba(51, 65, 85, 0.76) !important;
}

.architecture-detail-card__eyebrow,
.audio-pipeline__section-title,
.mcp-pipeline__section-title,
.ha-pipeline__section-title,
.mcp-pipeline__ready,
.ha-pipeline__ready,
.ha-pipeline__note {
  color: rgba(2, 132, 199, 0.76) !important;
}

.architecture-morph--detail .architecture-node--active {
  color: rgba(15, 32, 51, 0.94) !important;
}

.architecture-morph--detail .architecture-node--active .architecture-node__icon,
.architecture-node--active .architecture-node__icon {
  color: rgba(2, 132, 199, 0.96) !important;
}

.architecture-detail-card__tags span {
  border-color: rgba(14, 165, 233, 0.2) !important;
  background: rgba(255, 255, 255, 0.52) !important;
  color: rgba(2, 103, 152, 0.78) !important;
}

.audio-pipeline__node[data-layer]::before,
.audio-pipeline__down-node[data-layer]::before,
.mcp-pipeline__node[data-layer]::before,
.ha-pipeline__node[data-layer]::before {
  color: rgba(2, 132, 199, 0.68) !important;
}
</style>
