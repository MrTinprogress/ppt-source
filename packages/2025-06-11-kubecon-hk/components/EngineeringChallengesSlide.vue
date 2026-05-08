<script setup lang="ts">
import { useSlideContext } from '@slidev/client'

const { $clicks } = useSlideContext()

const challenges = [
  {
    index: '01',
    title: '唤醒词识别率下降',
    skill: '性能 profiling',
    design: '双核钉核',
    icon: 'i-carbon:voice-activate',
    tone: 'cyan',
    symptom: '识别率 95% → 60%，需要重复唤醒两三次',
    tool: 'vTaskGetRunTimeStats / vTaskList',
    root: 'audio_input 跑在 Core 0，被 WiFi 高优先级任务抢占',
    fix: '显式钉 Core 1，隔离网络抢占',
  },
  {
    index: '02',
    title: 'HA 偶尔控制不动舵机',
    skill: '静默错误排查',
    design: 'MQTT 重订阅',
    icon: 'i-carbon:home',
    tone: 'blue',
    symptom: '滑块拖动后舵机不动，日志无任何错误',
    tool: 'OnMessage 日志 / mosquitto_sub',
    root: 'CleanSession 清掉订阅，重连后 topic 未恢复',
    fix: 'OnConnected 后遍历 Feature 重订阅',
  },
  {
    index: '03',
    title: '设备运行几小时后重启',
    skill: '内存追踪',
    design: '长期稳定性',
    icon: 'i-carbon:chart-line-data',
    tone: 'emerald',
    symptom: '运行 3-4 小时后 Guru Meditation Error',
    tool: 'min_heap 趋势 / Stack Check / monitor 反汇编',
    root: 'WebSocket 重连反复 new，对象未释放导致碎片累积',
    fix: 'unique_ptr / RAII 管理重连资源',
  },
  {
    index: '04',
    title: '设备整体卡死无响应',
    skill: '死锁定位',
    design: 'mutex 持锁原则',
    icon: 'i-carbon:locked',
    tone: 'violet',
    symptom: '按键、串口均无响应，但没有崩溃信息',
    tool: 'vTaskList / Task Watchdog',
    root: '持锁执行 Lambda，内部再次 Schedule 抢同一把锁',
    fix: '取数据 → 解锁 → 再执行回调',
  },
]

const methodSteps = [
  {
    title: '量化现象',
    desc: '把“不灵敏、失效、卡死”转成识别率、延迟、任务状态和内存趋势。',
    icon: 'i-carbon:analytics',
  },
  {
    title: '验证链路',
    desc: '从设备、broker、任务状态多点打点，确认问题到底断在哪一层。',
    icon: 'i-carbon:flow',
  },
  {
    title: '定位机制',
    desc: '追到调度、订阅、内存生命周期、锁竞争这些系统机制。',
    icon: 'i-carbon:chip',
  },
  {
    title: '沉淀原则',
    desc: '把一次 bug 修复转成钉核、重订阅、RAII、持锁最小化。',
    icon: 'i-carbon:idea',
  },
]
</script>

<template>
  <section class="engineering-challenges">
    <header class="engineering-challenges__header">
      <h1>真实遇到的工程挑战</h1>
      <p>从问题定位到系统理解：调试能力是嵌入式开发的核心能力</p>
    </header>

    <div class="engineering-challenges__frame">
      <div class="engineering-challenges__summary">
        <span>4 类核心调试场景</span>
        <strong>性能 · 静默 bug · 内存 · 并发</strong>
      </div>

      <div class="engineering-challenges__grid" :class="{ 'engineering-challenges__grid--summary': $clicks >= 5 }">
        <article
          v-for="(challenge, i) in challenges"
          :key="challenge.title"
          class="challenge-card"
          :class="[
            `challenge-card--${challenge.tone}`,
            {
              'challenge-card--focused': $clicks === i + 1,
              'challenge-card--muted': $clicks > 0 && $clicks !== i + 1,
            },
          ]"
        >
          <div class="challenge-card__head">
            <div class="challenge-card__icon" :class="challenge.icon" />
            <div>
              <div class="challenge-card__index">Case {{ challenge.index }}</div>
              <h2>{{ challenge.title }}</h2>
            </div>
          </div>

          <div class="challenge-card__tags">
            <span>{{ challenge.skill }}</span>
            <span>{{ challenge.design }}</span>
          </div>

          <div class="challenge-card__body">
            <div class="challenge-card__row">
              <b>现象</b>
              <p>{{ challenge.symptom }}</p>
            </div>
            <div class="challenge-card__row">
              <b>工具</b>
              <p>{{ challenge.tool }}</p>
            </div>
            <div class="challenge-card__row">
              <b>根因</b>
              <p>{{ challenge.root }}</p>
            </div>
            <div class="challenge-card__row challenge-card__row--fix">
              <b>解决</b>
              <p>{{ challenge.fix }}</p>
            </div>
          </div>
        </article>
      </div>

      <Transition name="method-summary">
        <div v-if="$clicks >= 5" class="method-summary">
          <div class="method-summary__eyebrow">Debug Method</div>
          <h2>从 4 个真实 bug 中沉淀出的调试路径</h2>
          <div class="method-summary__flow">
            <article v-for="(step, index) in methodSteps" :key="step.title" class="method-summary__step">
              <div class="method-summary__icon" :class="step.icon" />
              <div>
                <div class="method-summary__index">0{{ index + 1 }}</div>
                <h3>{{ step.title }}</h3>
                <p>{{ step.desc }}</p>
              </div>
            </article>
          </div>
        </div>
      </Transition>
    </div>
  </section>
</template>

<style scoped>
.engineering-challenges {
  position: absolute;
  inset: 0;
  overflow: hidden;
  font-family: var(--deck-cn-serif);
  color: #0f2033;
}

.engineering-challenges__header {
  position: absolute;
  left: 6%;
  top: 7.2%;
  right: 6%;
}

.engineering-challenges__header h1 {
  margin: 0;
  color: #0f2033;
  font-family: 'Noto Sans SC', 'PingFang SC', 'Microsoft YaHei', sans-serif;
  font-size: 35px;
  font-weight: 820;
  letter-spacing: 0;
  line-height: 1.12;
  text-shadow: 0 10px 34px rgba(96, 165, 250, 0.18);
}

.engineering-challenges__header p {
  max-width: 860px;
  margin: 12px 0 0;
  color: rgba(51, 65, 85, 0.72);
  font-size: 14px;
  font-weight: 650;
  line-height: 1.55;
}

.engineering-challenges__frame {
  position: absolute;
  left: 6%;
  right: 6%;
  top: 22.2%;
  bottom: 5.8%;
  overflow: hidden;
  border: 1px solid rgba(125, 211, 252, 0.34);
  border-radius: 26px;
  background:
    radial-gradient(circle at 20% 18%, rgba(34, 211, 238, 0.15), transparent 30%),
    radial-gradient(circle at 80% 82%, rgba(167, 139, 250, 0.13), transparent 33%),
    linear-gradient(135deg, rgba(255, 255, 255, 0.84), rgba(239, 249, 255, 0.56));
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.9),
    0 24px 70px rgba(59, 130, 246, 0.14),
    0 0 0 1px rgba(255, 255, 255, 0.46);
  backdrop-filter: blur(20px) saturate(1.12);
}

.engineering-challenges__summary {
  position: absolute;
  left: 4.4%;
  top: 4.6%;
  display: flex;
  align-items: center;
  gap: 12px;
}

.engineering-challenges__summary span {
  border: 1px solid rgba(14, 165, 233, 0.22);
  border-radius: 999px;
  padding: 5px 12px;
  background: rgba(255, 255, 255, 0.6);
  color: rgba(2, 132, 199, 0.78);
  font-size: 8px;
  font-weight: 820;
}

.engineering-challenges__summary strong {
  color: rgba(51, 65, 85, 0.78);
  font-size: 11px;
  font-weight: 760;
}

.engineering-challenges__grid {
  position: absolute;
  left: 4.4%;
  right: 4.4%;
  top: 12.8%;
  bottom: 4.2%;
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  grid-template-rows: repeat(2, minmax(0, 1fr));
  gap: 12px;
  transition:
    opacity 520ms ease,
    filter 520ms ease,
    transform 520ms ease;
}

.engineering-challenges__grid--summary {
  opacity: 0.16;
  filter: blur(2px) saturate(0.65);
  transform: scale(0.985);
}

.challenge-card {
  position: relative;
  overflow: hidden;
  border: 1px solid rgba(14, 165, 233, 0.26);
  border-radius: 20px;
  padding: 13px 17px 12px;
  background:
    radial-gradient(circle at 84% 10%, var(--card-glow), transparent 42%),
    linear-gradient(180deg, rgba(255, 255, 255, 0.86), rgba(241, 249, 255, 0.64));
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.88),
    0 16px 42px rgba(59, 130, 246, 0.11);
  backdrop-filter: blur(16px) saturate(1.08);
  transition:
    opacity 520ms ease,
    filter 520ms ease,
    transform 520ms ease,
    box-shadow 520ms ease,
    border-color 520ms ease;
}

.challenge-card::after {
  position: absolute;
  right: -14%;
  bottom: -24%;
  width: 48%;
  height: 58%;
  content: "";
  background: radial-gradient(circle, var(--card-glow), transparent 68%);
  opacity: 0.68;
}

.challenge-card--focused {
  z-index: 3;
  border-color: color-mix(in srgb, var(--card-color) 58%, rgba(14, 165, 233, 0.28));
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.96),
    0 22px 56px rgba(59, 130, 246, 0.16),
    0 0 0 2px color-mix(in srgb, var(--card-color) 20%, transparent),
    0 0 34px var(--card-shadow);
  filter: saturate(1.14) contrast(1.02);
  transform: translateY(-2px);
}

.challenge-card--muted {
  opacity: 0.38;
  filter: saturate(0.65);
}

.challenge-card__head {
  position: relative;
  z-index: 1;
  display: grid;
  grid-template-columns: 30px minmax(0, 1fr);
  gap: 10px;
  align-items: center;
}

.challenge-card__icon {
  color: var(--card-color);
  font-size: 24px;
  filter: drop-shadow(0 8px 18px var(--card-shadow));
}

.challenge-card__index {
  color: rgba(2, 132, 199, 0.68);
  font-family: 'Inter', 'Noto Sans SC', sans-serif;
  font-size: 8px;
  font-weight: 820;
  letter-spacing: 0.08em;
  line-height: 1;
  text-transform: uppercase;
}

.challenge-card h2 {
  margin: 5px 0 0;
  color: #0f2033;
  font-size: 15.4px;
  font-weight: 820;
  line-height: 1.2;
}

.challenge-card__tags {
  position: relative;
  z-index: 1;
  display: flex;
  flex-wrap: wrap;
  gap: 5px;
  margin-top: 8px;
}

.challenge-card__tags span {
  display: inline-flex;
  align-items: center;
  min-height: 17px;
  border: 1px solid rgba(14, 165, 233, 0.2);
  border-radius: 999px;
  padding: 3px 7px;
  background: rgba(255, 255, 255, 0.58);
  color: rgba(51, 65, 85, 0.76);
  font-size: 6.6px;
  font-weight: 760;
  line-height: 1;
}

.challenge-card__body {
  position: relative;
  z-index: 1;
  display: grid;
  gap: 4px;
  margin-top: 9px;
}

.challenge-card__row {
  display: grid;
  grid-template-columns: 31px minmax(0, 1fr);
  gap: 7px;
  align-items: start;
}

.challenge-card__row b {
  color: rgba(2, 132, 199, 0.78);
  font-size: 7.4px;
  font-weight: 840;
  line-height: 1.4;
}

.challenge-card__row p {
  margin: 0;
  color: rgba(51, 65, 85, 0.78);
  font-size: 7.4px;
  font-weight: 680;
  line-height: 1.36;
}

.challenge-card__row--fix p {
  color: rgba(15, 32, 51, 0.86);
  font-weight: 780;
}

.challenge-card--cyan {
  --card-color: #0891b2;
  --card-glow: rgba(34, 211, 238, 0.2);
  --card-shadow: rgba(34, 211, 238, 0.3);
}

.challenge-card--blue {
  --card-color: #2563eb;
  --card-glow: rgba(59, 130, 246, 0.18);
  --card-shadow: rgba(59, 130, 246, 0.28);
}

.challenge-card--emerald {
  --card-color: #059669;
  --card-glow: rgba(52, 211, 153, 0.18);
  --card-shadow: rgba(52, 211, 153, 0.26);
}

.challenge-card--violet {
  --card-color: #6d28d9;
  --card-glow: rgba(196, 181, 253, 0.2);
  --card-shadow: rgba(196, 181, 253, 0.28);
}

.method-summary {
  position: absolute;
  left: 6.2%;
  right: 6.2%;
  top: 50%;
  z-index: 10;
  border: 1px solid rgba(14, 165, 233, 0.32);
  border-radius: 24px;
  padding: 24px 26px 26px;
  background:
    radial-gradient(circle at 18% 10%, rgba(34, 211, 238, 0.2), transparent 30%),
    radial-gradient(circle at 86% 84%, rgba(167, 139, 250, 0.17), transparent 34%),
    linear-gradient(180deg, rgba(255, 255, 255, 0.94), rgba(235, 248, 255, 0.82));
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.96),
    0 24px 64px rgba(59, 130, 246, 0.18),
    0 0 40px rgba(14, 165, 233, 0.12);
  transform: translateY(-50%);
  backdrop-filter: blur(20px) saturate(1.14);
}

.method-summary__eyebrow {
  color: rgba(2, 132, 199, 0.76);
  font-family: 'Inter', 'Noto Sans SC', sans-serif;
  font-size: 8px;
  font-weight: 840;
  letter-spacing: 0.1em;
  text-transform: uppercase;
}

.method-summary h2 {
  margin: 8px 0 0;
  color: #0f2033;
  font-size: 24px;
  font-weight: 840;
  line-height: 1.18;
}

.method-summary__flow {
  display: grid;
  grid-template-columns: repeat(4, minmax(0, 1fr));
  gap: 11px;
  margin-top: 20px;
}

.method-summary__step {
  position: relative;
  min-height: 126px;
  border: 1px solid rgba(14, 165, 233, 0.22);
  border-radius: 18px;
  padding: 16px 15px 14px;
  background:
    radial-gradient(circle at 80% 10%, rgba(56, 189, 248, 0.14), transparent 42%),
    linear-gradient(180deg, rgba(255, 255, 255, 0.72), rgba(241, 249, 255, 0.52));
}

.method-summary__step::after {
  position: absolute;
  top: 50%;
  right: -12px;
  width: 12px;
  height: 2px;
  content: "";
  background: linear-gradient(90deg, rgba(14, 165, 233, 0.42), rgba(14, 165, 233, 0));
}

.method-summary__step:last-child::after {
  display: none;
}

.method-summary__icon {
  color: #0284c7;
  font-size: 23px;
  filter: drop-shadow(0 8px 18px rgba(14, 165, 233, 0.25));
}

.method-summary__index {
  margin-top: 12px;
  color: rgba(2, 132, 199, 0.7);
  font-family: 'Inter', 'Noto Sans SC', sans-serif;
  font-size: 7px;
  font-weight: 840;
  letter-spacing: 0.08em;
}

.method-summary__step h3 {
  margin: 5px 0 0;
  color: #0f2033;
  font-size: 14px;
  font-weight: 840;
  line-height: 1.2;
}

.method-summary__step p {
  margin: 8px 0 0;
  color: rgba(51, 65, 85, 0.76);
  font-size: 7.4px;
  font-weight: 690;
  line-height: 1.45;
}

.method-summary-enter-active,
.method-summary-leave-active {
  transition:
    opacity 420ms ease,
    transform 420ms ease,
    filter 420ms ease;
}

.method-summary-enter-from,
.method-summary-leave-to {
  opacity: 0;
  filter: blur(6px);
  transform: translateY(-45%) scale(0.97);
}
</style>
