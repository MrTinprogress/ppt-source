<template>
  <div class="ability-light-stage">
    <div class="ability-light-inner">
      <div class="ability-light-heading">
        <h1>综合能力展示</h1>
        <p>
          学生会经历让我形成了稳定的组织、沟通与推进能力：能把任务拆清楚、把进度对齐好、把问题及时汇报出来，并在协作中推动事情落地。
        </p>
      </div>

      <div class="ability-light-content">
        <section
          class="ability-light-card ability-light-card--primary"
          :class="$clicks === 1 ? 'ability-light-card--active' : ($clicks === 2 ? 'ability-light-card--idle' : '')"
        >
          <div class="ability-light-card-title">学生会经历</div>
          <h2>电气工程学院学生会主席</h2>
          <p class="ability-light-summary">
            学生会主席经历不仅是组织活动，更重要的是让我反复练习了“把事情推进落地”的过程。
            在学术讲座、文艺晚会、体育赛事和创新活动中，我负责目标拆解、人员分工、进度跟进、资源协调和现场处理。
          </p>
          <ul class="ability-light-list">
            <li>任务拆解：把复杂目标拆成清晰步骤，明确谁做、何时做、做到什么程度。</li>
            <li>沟通汇报：在关键节点同步进度和风险，减少信息不对称。</li>
            <li>过程沉淀：整理材料、复盘问题、保留记录，让工作可追踪、可交接。</li>
          </ul>
        </section>

        <section
          class="ability-light-card ability-light-card--secondary"
          :class="$clicks === 2 ? 'ability-light-card--active' : ($clicks === 1 ? 'ability-light-card--idle' : '')"
        >
          <div class="ability-light-card-title">荣誉证明</div>
          <ul class="ability-light-honor-list">
            <li class="ability-light-honor-highlight">河南省普通高等学校优秀学生干部（2021）</li>
            <li>郑州大学优秀学生干部（2018、2019）</li>
            <li>郑州大学优秀学生会干部（2021）</li>
          </ul>
        </section>
      </div>
    </div>
  </div>
</template>
