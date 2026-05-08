<template>
  <section class="engineering-takeaways">
    <header class="engineering-takeaways__header">
      <h1>综合能力与工程能力总结</h1>
      <p>通过学生会经历与端侧 AI 家居项目，我形成了“能组织推进，也能工程落地”的复合型能力。</p>
    </header>

    <div class="engineering-takeaways__frame">
      <article class="ability-core">
        <div class="ability-core__eyebrow">Personal Value</div>
        <h2>我的特点不是只完成一个功能，而是能把任务拆清楚、把进度对齐好、把问题及时汇报出来，并把想法转化成可落地、可维护的工程系统。</h2>
      </article>

      <div class="ability-grid">
        <article v-for="item in abilities" :key="item.title" class="ability-card" :class="`ability-card--${item.tone}`">
          <div class="ability-card__icon" :class="item.icon" />
          <div class="ability-card__index">{{ item.index }}</div>
          <h2>{{ item.title }}</h2>
          <p>{{ item.desc }}</p>
          <div class="ability-card__tags">
            <span v-for="tag in item.tags" :key="tag">{{ tag }}</span>
          </div>
        </article>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
const abilities = [
  {
    index: '01',
    title: '任务拆解与从 0 到 1 落地能力',
    desc: '不是在现有项目中做局部修改，而是从需求拆解、技术选型、系统搭建到功能闭环独立推进，把端侧 AI 家居控制系统完整落地。',
    tags: ['需求拆解', '技术选型', '独立落地'],
    icon: 'i-carbon:assembly-cluster',
    tone: 'cyan',
  },
  {
    index: '02',
    title: '沟通对齐与协作推进能力',
    desc: '在学生会和项目推进中形成了稳定的沟通习惯，能主动同步进度、暴露风险、及时汇报问题，减少信息差，保证任务按节点推进。',
    tags: ['进度同步', '风险暴露', '及时汇报'],
    icon: 'i-carbon:collaborate',
    tone: 'blue',
  },
  {
    index: '03',
    title: '底层理解与问题定位能力',
    desc: '遇到问题时不只停留在功能表象，能继续深入任务调度、音频链路、MQTT 会话、内存管理和并发锁机制，用工具逐层定位真实根因。',
    tags: ['任务调度', '链路排查', '根因定位'],
    icon: 'i-carbon:debug',
    tone: 'emerald',
  },
  {
    index: '04',
    title: '工程复盘与长期维护能力',
    desc: '不把 bug 修复停留在“当前能跑”，而是进一步沉淀成钉核、重订阅、RAII、持锁最小化等设计原则，让系统后续更稳定、更可维护。',
    tags: ['工程复盘', '设计原则', '长期维护'],
    icon: 'i-carbon:idea',
    tone: 'violet',
  },
]
</script>

<style scoped>
.engineering-takeaways {
  position: absolute;
  inset: 0;
  overflow: hidden;
  font-family: var(--deck-cn-serif);
  color: #0f2033;
}

.engineering-takeaways__header {
  position: absolute;
  left: 6%;
  top: 7.2%;
  right: 6%;
}

.engineering-takeaways__header h1 {
  margin: 0;
  color: #0f2033;
  font-family: 'Noto Sans SC', 'PingFang SC', 'Microsoft YaHei', sans-serif;
  font-size: 35px;
  font-weight: 820;
  letter-spacing: 0;
  line-height: 1.12;
  text-shadow: 0 10px 34px rgba(96, 165, 250, 0.18);
}

.engineering-takeaways__header p {
  max-width: 960px;
  margin: 12px 0 0;
  color: rgba(51, 65, 85, 0.72);
  font-size: 14px;
  font-weight: 650;
  line-height: 1.55;
}

.engineering-takeaways__frame {
  position: absolute;
  left: 6%;
  right: 6%;
  top: 23%;
  bottom: 7.2%;
  overflow: hidden;
  border: 1px solid rgba(125, 211, 252, 0.34);
  border-radius: 26px;
  background:
    radial-gradient(circle at 26% 18%, rgba(34, 211, 238, 0.16), transparent 30%),
    radial-gradient(circle at 78% 76%, rgba(167, 139, 250, 0.13), transparent 33%),
    linear-gradient(135deg, rgba(255, 255, 255, 0.84), rgba(239, 249, 255, 0.56));
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.9),
    0 24px 70px rgba(59, 130, 246, 0.14),
    0 0 0 1px rgba(255, 255, 255, 0.46);
  backdrop-filter: blur(20px) saturate(1.12);
}

.ability-core {
  position: absolute;
  left: 3.2%;
  right: 3.2%;
  top: 6%;
  border: 1px solid rgba(14, 165, 233, 0.28);
  border-radius: 22px;
  padding: 15px 23px;
  background:
    radial-gradient(circle at 86% 18%, rgba(34, 211, 238, 0.16), transparent 36%),
    linear-gradient(180deg, rgba(255, 255, 255, 0.9), rgba(235, 248, 255, 0.68));
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.94),
    0 18px 52px rgba(59, 130, 246, 0.12);
}

.ability-core__eyebrow {
  color: rgba(2, 132, 199, 0.74);
  font-family: 'Inter', 'Noto Sans SC', sans-serif;
  font-size: 8px;
  font-weight: 840;
  letter-spacing: 0.1em;
  text-transform: uppercase;
}

.ability-core h2 {
  max-width: 1040px;
  margin: 8px 0 0;
  color: #0f2033;
  font-size: 15.6px;
  font-weight: 820;
  line-height: 1.36;
}

.ability-grid {
  position: absolute;
  left: 3.2%;
  right: 3.2%;
  top: 36.5%;
  bottom: 6.5%;
  display: grid;
  grid-template-columns: repeat(4, minmax(0, 1fr));
  gap: 9px;
}

.ability-card {
  position: relative;
  min-height: 0;
  overflow: hidden;
  border: 1px solid rgba(14, 165, 233, 0.25);
  border-radius: 20px;
  padding: 17px 16px 15px;
  background:
    radial-gradient(circle at 82% 12%, var(--ability-glow), transparent 42%),
    linear-gradient(180deg, rgba(255, 255, 255, 0.88), rgba(241, 249, 255, 0.62));
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.9),
    0 16px 42px rgba(59, 130, 246, 0.1);
  backdrop-filter: blur(16px) saturate(1.08);
}

.ability-card__icon {
  color: var(--ability-color);
  font-size: 25px;
  filter: drop-shadow(0 8px 18px var(--ability-shadow));
}

.ability-card__index {
  margin-top: 13px;
  color: rgba(2, 132, 199, 0.72);
  font-family: 'Inter', 'Noto Sans SC', sans-serif;
  font-size: 8px;
  font-weight: 840;
  letter-spacing: 0.08em;
}

.ability-card h2 {
  margin: 6px 0 0;
  color: #0f2033;
  font-size: 13.2px;
  font-weight: 840;
  line-height: 1.24;
}

.ability-card p {
  margin: 9px 0 0;
  color: rgba(51, 65, 85, 0.75);
  font-size: 7.4px;
  font-weight: 690;
  line-height: 1.48;
}

.ability-card__tags {
  display: flex;
  flex-wrap: wrap;
  gap: 5px;
  margin-top: 11px;
}

.ability-card__tags span {
  border: 1px solid rgba(14, 165, 233, 0.2);
  border-radius: 999px;
  padding: 3px 7px;
  background: rgba(255, 255, 255, 0.58);
  color: rgba(51, 65, 85, 0.72);
  font-size: 6.6px;
  font-weight: 760;
  line-height: 1;
}

.ability-card--cyan {
  --ability-color: #0891b2;
  --ability-glow: rgba(34, 211, 238, 0.2);
  --ability-shadow: rgba(34, 211, 238, 0.3);
}

.ability-card--blue {
  --ability-color: #2563eb;
  --ability-glow: rgba(59, 130, 246, 0.18);
  --ability-shadow: rgba(59, 130, 246, 0.28);
}

.ability-card--emerald {
  --ability-color: #059669;
  --ability-glow: rgba(52, 211, 153, 0.18);
  --ability-shadow: rgba(52, 211, 153, 0.26);
}

.ability-card--violet {
  --ability-color: #6d28d9;
  --ability-glow: rgba(196, 181, 253, 0.2);
  --ability-shadow: rgba(196, 181, 253, 0.28);
}
</style>
