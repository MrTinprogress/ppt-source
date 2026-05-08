<template>
  <section class="tech-highlights">
    <header class="tech-highlights__header">
      <h1>技术亮点介绍</h1>
      <p>围绕端侧 AI 家居控制框架，把底层框架、音频智能、通信协议与状态存储组织成可维护的系统能力。</p>
    </header>

    <div class="tech-highlights__stage">
      <svg class="tech-highlights__links" viewBox="0 0 1000 560" preserveAspectRatio="none" aria-hidden="true">
        <line
          v-for="(link, index) in links"
          :key="index"
          :x1="link.x1"
          :y1="link.y1"
          :x2="link.x2"
          :y2="link.y2"
          :class="{ 'tech-highlights__link--active': $clicks >= index + 1 }"
        />
      </svg>

      <article class="tech-core">
        <div class="tech-core__eyebrow">System Core</div>
        <h2>ESP32-S3 端侧 AI 家居控制框架</h2>
        <p>感知、唤醒、对话、工具调用、硬件执行与状态回报的闭环系统。</p>
      </article>

      <article
        v-for="(item, index) in highlights"
        :key="item.title"
        class="tech-node"
        :class="[
          `tech-node--${item.tone}`,
          `tech-node--${item.position}`,
          {
            'tech-node--active': $clicks >= index + 1,
            'tech-node--current': $clicks === index + 1,
          },
        ]"
      >
        <div class="tech-node__top">
          <div class="tech-node__icon" :class="item.icon" />
          <div>
            <div class="tech-node__group">{{ item.group }}</div>
            <h2>{{ item.title }}</h2>
          </div>
        </div>
        <div class="tech-node__keywords">
          <span v-for="keyword in item.keywords" :key="keyword">{{ keyword }}</span>
        </div>
      </article>
    </div>

    <div class="tech-highlights__legend">
      <span>底层框架</span>
      <span>音频智能</span>
      <span>通信协议</span>
      <span>状态存储</span>
    </div>
  </section>
</template>

<script setup lang="ts">
import { useSlideContext } from '@slidev/client'

const { $clicks } = useSlideContext()

const links = [
  { x1: 500, y1: 278, x2: 208, y2: 96 },
  { x1: 500, y1: 278, x2: 500, y2: 86 },
  { x1: 500, y1: 278, x2: 792, y2: 96 },
  { x1: 500, y1: 278, x2: 166, y2: 278 },
  { x1: 500, y1: 278, x2: 834, y2: 278 },
  { x1: 500, y1: 278, x2: 208, y2: 462 },
  { x1: 500, y1: 278, x2: 500, y2: 480 },
  { x1: 500, y1: 278, x2: 792, y2: 462 },
]

const highlights = [
  {
    title: 'ESP-IDF 框架',
    group: '底层框架',
    icon: 'i-carbon:tree-view-alt',
    tone: 'blue',
    position: 'top-left',
    keywords: ['控制权', '组件化', '底层能力'],
  },
  {
    title: 'AFE 音频前端',
    group: '音频智能',
    icon: 'i-carbon:volume-up',
    tone: 'cyan',
    position: 'top',
    keywords: ['AEC', 'NS', 'VAD', 'WakeNet'],
  },
  {
    title: 'Opus 编码',
    group: '音频智能',
    icon: 'i-carbon:audio-console',
    tone: 'teal',
    position: 'top-right',
    keywords: ['低延迟', '高压缩比', '实时通信'],
  },
  {
    title: '本地唤醒词检测',
    group: '音频智能',
    icon: 'i-carbon:voice-activate',
    tone: 'purple',
    position: 'middle-left',
    keywords: ['零网络流量', '隐私保护', '低 CPU 占用'],
  },
  {
    title: 'WebSocket 通信',
    group: '通信协议',
    icon: 'i-carbon:network-4',
    tone: 'sky',
    position: 'middle-right',
    keywords: ['双向流式', '长连接', '低延迟'],
  },
  {
    title: '双核任务分配 + 优先级',
    group: '底层框架',
    icon: 'i-carbon:task-settings',
    tone: 'indigo',
    position: 'bottom-left',
    keywords: ['Core 0 网络', 'Core 1 音频', '优先级隔离'],
  },
  {
    title: 'NVS Blob 序列化',
    group: '状态存储',
    icon: 'i-carbon:data-structured',
    tone: 'emerald',
    position: 'bottom',
    keywords: ['Flash 可靠性', '原子提交', '结构化持久化'],
  },
  {
    title: 'MCP 协议范式',
    group: '通信协议',
    icon: 'i-carbon:tool-kit',
    tone: 'violet',
    position: 'bottom-right',
    keywords: ['工具描述', 'JSON-RPC', '异步执行'],
  },
]
</script>

<style scoped>
.tech-highlights {
  position: absolute;
  inset: 0;
  overflow: hidden;
  font-family: var(--deck-cn-serif);
  color: #0f2033;
}

.tech-highlights__header {
  position: absolute;
  left: 6%;
  top: 7.4%;
  right: 6%;
}

.tech-highlights__header h1 {
  margin: 0;
  color: #0f2033;
  font-family: 'Noto Sans SC', 'PingFang SC', 'Microsoft YaHei', sans-serif;
  font-size: 35px;
  font-weight: 820;
  letter-spacing: 0;
  line-height: 1.12;
  text-shadow: 0 10px 34px rgba(96, 165, 250, 0.18);
}

.tech-highlights__header p {
  max-width: 900px;
  margin: 12px 0 0;
  color: rgba(51, 65, 85, 0.72);
  font-size: 14px;
  font-weight: 650;
  line-height: 1.55;
}

.tech-highlights__stage {
  position: absolute;
  left: 6%;
  right: 6%;
  top: 23%;
  bottom: 7.2%;
  overflow: hidden;
  border: 1px solid rgba(125, 211, 252, 0.34);
  border-radius: 26px;
  background:
    radial-gradient(circle at 50% 46%, rgba(56, 189, 248, 0.16), transparent 24%),
    radial-gradient(circle at 24% 22%, rgba(34, 211, 238, 0.12), transparent 30%),
    radial-gradient(circle at 82% 74%, rgba(167, 139, 250, 0.12), transparent 34%),
    linear-gradient(135deg, rgba(255, 255, 255, 0.82), rgba(239, 249, 255, 0.54));
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.9),
    0 24px 70px rgba(59, 130, 246, 0.14),
    0 0 0 1px rgba(255, 255, 255, 0.46);
  backdrop-filter: blur(20px) saturate(1.12);
}

.tech-highlights__links {
  position: absolute;
  inset: 5.2% 4.8%;
  width: 90.4%;
  height: 89.6%;
  pointer-events: none;
}

.tech-highlights__links line {
  stroke: rgba(14, 165, 233, 0.1);
  stroke-width: 1.4;
  stroke-linecap: round;
  filter: drop-shadow(0 0 5px rgba(56, 189, 248, 0.08));
  transition:
    stroke 520ms ease,
    stroke-width 520ms ease,
    filter 520ms ease,
    opacity 520ms ease;
  opacity: 0.44;
}

.tech-highlights__links .tech-highlights__link--active {
  stroke: rgba(14, 165, 233, 0.48);
  stroke-width: 2.1;
  filter: drop-shadow(0 0 12px rgba(56, 189, 248, 0.42));
  opacity: 1;
}

.tech-core {
  position: absolute;
  left: 50%;
  top: 50%;
  z-index: 8;
  width: 286px;
  min-height: 118px;
  border: 1px solid rgba(14, 165, 233, 0.34);
  border-radius: 22px;
  padding: 20px 24px;
  background:
    radial-gradient(circle at 78% 16%, rgba(34, 211, 238, 0.2), transparent 38%),
    linear-gradient(180deg, rgba(255, 255, 255, 0.92), rgba(232, 247, 255, 0.72));
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.95),
    0 22px 56px rgba(14, 165, 233, 0.2),
    0 0 38px rgba(45, 212, 191, 0.12);
  text-align: center;
  transform: translate(-50%, -50%);
}

.tech-core__eyebrow {
  color: rgba(2, 132, 199, 0.76);
  font-family: 'Inter', 'Noto Sans SC', sans-serif;
  font-size: 9px;
  font-weight: 820;
  letter-spacing: 0.08em;
  text-transform: uppercase;
}

.tech-core h2 {
  margin: 9px 0 0;
  color: #0f2033;
  font-size: 16px;
  font-weight: 800;
  line-height: 1.24;
}

.tech-core p {
  margin: 9px 0 0;
  color: rgba(51, 65, 85, 0.76);
  font-size: 9.6px;
  font-weight: 680;
  line-height: 1.55;
}

.tech-node {
  position: absolute;
  z-index: 4;
  width: 206px;
  min-height: 104px;
  border: 1px solid rgba(14, 165, 233, 0.28);
  border-radius: 18px;
  padding: 13px 15px 12px;
  background:
    radial-gradient(circle at 80% 16%, var(--node-glow), transparent 40%),
    linear-gradient(180deg, rgba(255, 255, 255, 0.84), rgba(241, 249, 255, 0.6));
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.88),
    0 14px 42px rgba(59, 130, 246, 0.11);
  backdrop-filter: blur(16px) saturate(1.08);
  filter: saturate(0.72);
  opacity: 0.34;
  transition:
    opacity 520ms ease,
    filter 520ms ease,
    box-shadow 520ms ease,
    border-color 520ms ease,
    background 520ms ease;
}

.tech-node--active {
  border-color: color-mix(in srgb, var(--node-color) 52%, rgba(14, 165, 233, 0.26));
  opacity: 1;
  filter: saturate(1.16) contrast(1.02);
  background:
    radial-gradient(circle at 80% 16%, var(--node-glow), transparent 40%),
    linear-gradient(180deg, rgba(255, 255, 255, 0.94), rgba(232, 247, 255, 0.74));
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.94),
    0 18px 48px rgba(59, 130, 246, 0.14),
    0 0 26px var(--node-shadow);
}

.tech-node--current {
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.96),
    0 20px 54px rgba(59, 130, 246, 0.18),
    0 0 0 2px color-mix(in srgb, var(--node-color) 32%, transparent),
    0 0 34px var(--node-shadow);
}

.tech-node__top {
  display: grid;
  grid-template-columns: 26px minmax(0, 1fr);
  gap: 8px;
  align-items: center;
}

.tech-node__icon {
  color: var(--node-color);
  font-size: 22px;
  filter: drop-shadow(0 8px 18px var(--node-shadow));
  transition:
    opacity 520ms ease,
    transform 520ms ease,
    filter 520ms ease;
}

.tech-node--active .tech-node__icon {
  transform: translateY(-1px);
  filter: drop-shadow(0 10px 24px var(--node-shadow));
}

.tech-node__group {
  color: rgba(2, 132, 199, 0.7);
  font-family: 'Inter', 'Noto Sans SC', sans-serif;
  font-size: 7px;
  font-weight: 820;
  letter-spacing: 0.06em;
  line-height: 1;
}

.tech-node h2 {
  margin: 5px 0 0;
  color: #0f2033;
  font-size: 12px;
  font-weight: 820;
  line-height: 1.22;
}

.tech-node__keywords {
  display: flex;
  flex-wrap: wrap;
  gap: 4px;
  margin-top: 9px;
  opacity: 0.58;
  transition: opacity 520ms ease;
}

.tech-node--active .tech-node__keywords {
  opacity: 1;
}

.tech-node__keywords span {
  display: inline-flex;
  align-items: center;
  min-height: 17px;
  border: 1px solid rgba(14, 165, 233, 0.18);
  border-radius: 999px;
  padding: 3px 6px;
  background: rgba(255, 255, 255, 0.55);
  color: rgba(51, 65, 85, 0.78);
  font-size: 6.4px;
  font-weight: 720;
  line-height: 1;
}

.tech-node--top-left {
  left: 7.8%;
  top: 6.8%;
}

.tech-node--top {
  left: 50%;
  top: 5.8%;
  transform: translateX(-50%);
}

.tech-node--top-right {
  right: 7.8%;
  top: 6.8%;
}

.tech-node--middle-left {
  left: 4.2%;
  top: 50%;
  transform: translateY(-50%);
}

.tech-node--middle-right {
  right: 4.2%;
  top: 50%;
  transform: translateY(-50%);
}

.tech-node--bottom-left {
  left: 7.8%;
  bottom: 6.8%;
}

.tech-node--bottom {
  left: 50%;
  bottom: 5.8%;
  transform: translateX(-50%);
}

.tech-node--bottom-right {
  right: 7.8%;
  bottom: 6.8%;
}

.tech-node--blue {
  --node-color: #2563eb;
  --node-glow: rgba(59, 130, 246, 0.2);
  --node-shadow: rgba(59, 130, 246, 0.28);
}

.tech-node--cyan {
  --node-color: #0891b2;
  --node-glow: rgba(34, 211, 238, 0.2);
  --node-shadow: rgba(34, 211, 238, 0.28);
}

.tech-node--teal {
  --node-color: #0f766e;
  --node-glow: rgba(45, 212, 191, 0.18);
  --node-shadow: rgba(45, 212, 191, 0.26);
}

.tech-node--purple {
  --node-color: #7c3aed;
  --node-glow: rgba(167, 139, 250, 0.18);
  --node-shadow: rgba(167, 139, 250, 0.26);
}

.tech-node--sky {
  --node-color: #0284c7;
  --node-glow: rgba(125, 211, 252, 0.2);
  --node-shadow: rgba(125, 211, 252, 0.28);
}

.tech-node--indigo {
  --node-color: #4f46e5;
  --node-glow: rgba(129, 140, 248, 0.18);
  --node-shadow: rgba(129, 140, 248, 0.26);
}

.tech-node--emerald {
  --node-color: #059669;
  --node-glow: rgba(52, 211, 153, 0.18);
  --node-shadow: rgba(52, 211, 153, 0.26);
}

.tech-node--violet {
  --node-color: #6d28d9;
  --node-glow: rgba(196, 181, 253, 0.2);
  --node-shadow: rgba(196, 181, 253, 0.28);
}

.tech-highlights__legend {
  position: absolute;
  left: 50%;
  bottom: 5.4%;
  display: flex;
  gap: 10px;
  transform: translateX(-50%);
}

.tech-highlights__legend span {
  border: 1px solid rgba(14, 165, 233, 0.18);
  border-radius: 999px;
  padding: 4px 12px;
  background: rgba(255, 255, 255, 0.48);
  color: rgba(51, 65, 85, 0.66);
  font-size: 8px;
  font-weight: 760;
}
</style>
