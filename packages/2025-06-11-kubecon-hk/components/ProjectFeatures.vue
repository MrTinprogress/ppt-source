<template>
  <section class="project-features">
    <header class="project-features__header">
      <h1>项目实现功能</h1>
      <p>围绕端侧设备构建“感知 - 理解 - 执行 - 联动”的完整系统能力</p>
    </header>

    <div class="project-features__layers">
      <article
        class="project-feature-layer project-feature-layer--sense"
        :class="{ 'project-feature-layer--active': $clicks >= 1, 'project-feature-layer--pending': $clicks > 0 && $clicks < 1 }"
      >
        <div class="project-feature-layer__index">01</div>
        <div class="project-feature-layer__icon i-carbon:waveform" />
        <h2>感知层</h2>
        <p>负责端侧语音输入、前端处理、压缩传输与音频播放。</p>
        <ul>
          <li>语音采集处理及播放</li>
          <li>唤醒检测与对话音频流转</li>
        </ul>
        <div class="project-feature-layer__tags">
          <span>I2S</span><span>AFE</span><span>Opus</span><span>WebSocket</span>
        </div>
      </article>

      <article
        class="project-feature-layer project-feature-layer--mcp"
        :class="{ 'project-feature-layer--active': $clicks >= 2, 'project-feature-layer--pending': $clicks > 0 && $clicks < 2 }"
      >
        <div class="project-feature-layer__index">02</div>
        <div class="project-feature-layer__icon i-carbon:tool-kit" />
        <h2>理解与调度层</h2>
        <p>把 AI 的语义意图转换为结构化工具调用，并完成参数解析。</p>
        <ul>
          <li>MCP 工具拓展</li>
          <li>AI 调用硬件能力入口</li>
        </ul>
        <div class="project-feature-layer__tags">
          <span>MCP</span><span>JSON-RPC</span><span>Tool Schema</span><span>Thread</span>
        </div>
      </article>

      <article
        class="project-feature-layer project-feature-layer--execute"
        :class="{ 'project-feature-layer--active': $clicks >= 3, 'project-feature-layer--pending': $clicks > 0 && $clicks < 3 }"
      >
        <div class="project-feature-layer__index">03</div>
        <div class="project-feature-layer__icon i-carbon:chip" />
        <h2>执行与记忆层</h2>
        <p>将工具调用落到真实设备动作，并维护可恢复的本地状态。</p>
        <ul>
          <li>舵机硬件控制</li>
          <li>提醒与闹钟记忆系统</li>
        </ul>
        <div class="project-feature-layer__tags">
          <span>PWM</span><span>NVS Blob</span><span>Scheduler</span><span>State</span>
        </div>
      </article>

      <article
        class="project-feature-layer project-feature-layer--link"
        :class="{ 'project-feature-layer--active': $clicks >= 4, 'project-feature-layer--pending': $clicks > 0 && $clicks < 4 }"
      >
        <div class="project-feature-layer__index">04</div>
        <div class="project-feature-layer__icon i-carbon:network-4" />
        <h2>联动层</h2>
        <p>从单设备能力扩展到主动触发与智能家居生态联动。</p>
        <ul>
          <li>设备主动触发</li>
          <li>Home Assistant 联动</li>
        </ul>
        <div class="project-feature-layer__tags">
          <span>MQTT</span><span>Topic</span><span>Reconnect</span><span>Event</span>
        </div>
      </article>
    </div>

    <div class="project-features__formula">
      <span>端侧感知</span>
      <i></i>
      <span>AI 理解</span>
      <i></i>
      <span>工具调度</span>
      <i></i>
      <span>硬件执行</span>
      <i></i>
      <span>状态联动</span>
    </div>
  </section>
</template>

<style scoped>
.project-features {
  position: absolute;
  inset: 0;
  overflow: hidden;
  font-family: var(--deck-cn-serif);
}

.project-features__header {
  position: absolute;
  left: 6%;
  top: 8%;
}

.project-features__header h1 {
  margin: 0;
  color: #0f2033;
  font-family: 'Noto Sans SC', 'PingFang SC', 'Microsoft YaHei', sans-serif;
  font-size: 38px;
  font-weight: 780;
  letter-spacing: 0.015em;
  line-height: 1.12;
  text-shadow: 0 10px 34px rgba(96, 165, 250, 0.18);
}

.project-features__header p {
  margin: 13px 0 0;
  color: rgba(51, 65, 85, 0.76);
  font-size: 15px;
  font-weight: 650;
  letter-spacing: 0;
}

.project-features__layers {
  position: absolute;
  left: 50%;
  top: 27%;
  display: grid;
  grid-template-columns: repeat(4, 205px);
  gap: 20px;
  width: 880px;
  transform: translateX(-50%);
}

.project-feature-layer {
  position: relative;
  display: flex;
  flex-direction: column;
  min-height: 292px;
  overflow: visible;
  border: 1px solid rgba(14, 165, 233, 0.24);
  border-radius: 22px;
  padding: 20px 18px 18px;
  background:
    radial-gradient(circle at 76% 18%, rgba(125, 211, 252, 0.18), transparent 38%),
    linear-gradient(180deg, rgba(255, 255, 255, 0.7), rgba(240, 249, 255, 0.42));
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.84),
    0 18px 54px rgba(59, 130, 246, 0.14),
    0 0 0 1px rgba(255, 255, 255, 0.34);
  backdrop-filter: blur(18px) saturate(1.08);
  -webkit-backdrop-filter: blur(18px) saturate(1.08);
  transition:
    opacity 320ms ease,
    transform 320ms ease,
    border-color 320ms ease,
    box-shadow 320ms ease,
    background 320ms ease;
}

.project-feature-layer:not(:last-child)::after {
  position: absolute;
  top: 50%;
  right: -22px;
  z-index: 3;
  width: 22px;
  height: 2px;
  content: "";
  border-radius: 999px;
  background: rgba(14, 165, 233, 0.42);
  box-shadow: 0 0 14px rgba(14, 165, 233, 0.2);
}

.project-feature-layer:not(:last-child)::before {
  position: absolute;
  top: calc(50% - 4px);
  right: -22px;
  z-index: 4;
  width: 8px;
  height: 8px;
  content: "";
  border-top: 2px solid rgba(14, 165, 233, 0.5);
  border-right: 2px solid rgba(14, 165, 233, 0.5);
  transform: rotate(45deg);
}

.project-feature-layer__index {
  position: absolute;
  top: 17px;
  right: 18px;
  color: rgba(2, 132, 199, 0.22);
  font-family: 'Noto Sans SC', 'PingFang SC', 'Microsoft YaHei', sans-serif;
  font-size: 25px;
  font-weight: 800;
  line-height: 1;
}

.project-feature-layer__icon {
  color: rgba(2, 132, 199, 0.82);
  font-size: 38px;
}

.project-feature-layer h2 {
  margin: 20px 0 0;
  color: rgba(15, 32, 51, 0.94);
  font-family: 'Noto Sans SC', 'PingFang SC', 'Microsoft YaHei', sans-serif;
  font-size: 18px;
  font-weight: 780;
  line-height: 1.22;
}

.project-feature-layer p {
  min-height: 48px;
  margin: 11px 0 0;
  color: rgba(51, 65, 85, 0.78);
  font-size: 8.6px;
  font-weight: 650;
  line-height: 1.55;
}

.project-feature-layer ul {
  display: grid;
  gap: 7px;
  margin: 13px 0 0;
  padding: 0;
  list-style: none;
}

.project-feature-layer li {
  position: relative;
  padding-left: 12px;
  color: rgba(15, 32, 51, 0.86);
  font-size: 8.8px;
  font-weight: 700;
  line-height: 1.3;
}

.project-feature-layer li::before {
  position: absolute;
  top: 0.52em;
  left: 0;
  width: 5px;
  height: 5px;
  content: "";
  border-radius: 999px;
  background: rgba(14, 165, 233, 0.56);
}

.project-feature-layer__tags {
  display: flex;
  flex-wrap: wrap;
  gap: 5px;
  margin-top: auto;
  padding-top: 18px;
}

.project-feature-layer__tags span {
  border: 1px solid rgba(14, 165, 233, 0.18);
  border-radius: 999px;
  padding: 4px 6px;
  background: rgba(255, 255, 255, 0.34);
  color: rgba(2, 132, 199, 0.82);
  font-family: 'Noto Sans SC', 'PingFang SC', 'Microsoft YaHei', sans-serif;
  font-size: 5.8px;
  font-weight: 760;
  line-height: 1;
  white-space: nowrap;
}

.project-feature-layer--mcp {
  border-color: rgba(6, 182, 212, 0.24);
  background:
    radial-gradient(circle at 76% 18%, rgba(45, 212, 191, 0.18), transparent 38%),
    linear-gradient(180deg, rgba(255, 255, 255, 0.68), rgba(236, 254, 255, 0.4));
}

.project-feature-layer--execute {
  border-color: rgba(99, 102, 241, 0.22);
  background:
    radial-gradient(circle at 76% 18%, rgba(167, 139, 250, 0.16), transparent 38%),
    linear-gradient(180deg, rgba(255, 255, 255, 0.68), rgba(239, 246, 255, 0.4));
}

.project-feature-layer--link {
  border-color: rgba(14, 165, 233, 0.24);
}

.project-feature-layer--active {
  z-index: 2;
  border-color: rgba(14, 165, 233, 0.52);
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.9),
    0 22px 62px rgba(14, 165, 233, 0.2),
    0 0 0 1px rgba(14, 165, 233, 0.18);
  transform: translateY(-8px) scale(1.025);
}

.project-feature-layer--pending {
  opacity: 0.44;
  transform: scale(0.985);
}

.project-features__formula {
  position: absolute;
  left: 50%;
  bottom: 8%;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
  width: 790px;
  max-width: 88%;
  transform: translateX(-50%);
}

.project-features__formula span {
  border: 1px solid rgba(14, 165, 233, 0.22);
  border-radius: 999px;
  padding: 8px 15px;
  background:
    radial-gradient(circle at 80% 20%, rgba(125, 211, 252, 0.18), transparent 42%),
    rgba(255, 255, 255, 0.38);
  color: rgba(15, 32, 51, 0.9);
  font-family: 'Noto Sans SC', 'PingFang SC', 'Microsoft YaHei', sans-serif;
  font-size: 10.5px;
  font-weight: 760;
  line-height: 1;
  white-space: nowrap;
  box-shadow: 0 10px 28px rgba(59, 130, 246, 0.1);
  backdrop-filter: blur(14px) saturate(1.08);
}

.project-features__formula i {
  position: relative;
  display: block;
  width: 23px;
  height: 2px;
  border-radius: 999px;
  background: rgba(14, 165, 233, 0.42);
  box-shadow: 0 0 14px rgba(14, 165, 233, 0.2);
}

.project-features__formula i::after {
  position: absolute;
  top: 50%;
  right: -1px;
  width: 7px;
  height: 7px;
  content: "";
  border-top: 2px solid rgba(14, 165, 233, 0.52);
  border-right: 2px solid rgba(14, 165, 233, 0.52);
  transform: translateY(-50%) rotate(45deg);
}
</style>
