<template>
  <section class="education-background">
    <h1 class="education-background__title">个人背景介绍</h1>

    <div class="education-background__meta">
      <div class="education-background__meta-card">
        <span>年龄：</span><strong>26岁</strong>
      </div>
      <div class="education-background__meta-card">
        <span>籍贯：</span><strong>河北保定</strong>
      </div>
      <div
        class="education-background__meta-card"
        :class="{
          'education-background__meta-card--active': $clicks >= 1,
        }"
      >
        <span>政治面貌：</span><strong>中国共产党党员</strong>
      </div>
    </div>

    <div class="education-background__cards">
      <article
        class="education-background__card"
        :class="{
          'education-background__card--active': $clicks >= 2,
        }"
      >
        <div class="education-background__copy">
          <div class="education-background__line">
            <div class="education-background__school">郑州大学</div>
            <div class="education-background__program">轨道交通信号与控制（自动化方向）</div>
          </div>
          <div class="education-background__tags">
            <span>2018.09 - 2022.06</span>
            <span>211</span>
          </div>
          <p class="education-background__courses">
            <strong>主修课程：</strong>电磁场，数字电子技术，模拟电子技术，电机与拖动，计算机网络，单片机原理，自动控制理论，电力电子技术
          </p>
        </div>

        <div class="education-background__logo-wrap">
          <img class="education-background__logo" src="/schools/zzu-logo.svg" alt="郑州大学校徽">
        </div>
      </article>

      <article
        class="education-background__card education-background__card--secondary"
        :class="{
          'education-background__card--active': $clicks >= 3,
        }"
      >
        <div class="education-background__copy">
          <div class="education-background__line">
            <div class="education-background__school">南安普敦大学</div>
            <div class="education-background__program">物联网</div>
          </div>
          <div class="education-background__tags">
            <span>2024.09 - 2025.11</span>
            <span>QS世界排名前100</span>
          </div>
          <p class="education-background__courses">
            <strong>主修课程：</strong>嵌入式物联网系统基础，物联网网络，嵌入式处理器，密码学，移动应用构建
          </p>
        </div>

        <div class="education-background__logo-wrap">
          <img class="education-background__logo" src="/schools/uos-no-text-from-pdf.svg" alt="南安普敦大学校徽">
        </div>
      </article>
    </div>
  </section>
</template>

<style scoped>
.education-background {
  position: absolute;
  inset: 0;
  overflow: hidden;
  font-family: var(--deck-cn-serif);
}

.education-background__title {
  position: absolute;
  top: 40px;
  left: 72px;
  margin: 0;
  color: #0f2033;
  font-family: 'Noto Sans SC', 'PingFang SC', 'Microsoft YaHei', sans-serif;
  font-size: 38px;
  font-weight: 760;
  letter-spacing: 0.02em;
  line-height: 1.16;
  text-align: left;
  text-shadow: 0 10px 34px rgba(96, 165, 250, 0.18);
}

.education-background__meta {
  position: absolute;
  left: 72px;
  right: auto;
  top: 104px;
  display: grid;
  grid-template-columns: 116px 150px 222px;
  gap: 12px;
}

.education-background__meta-card {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  border: 1px solid rgba(14, 165, 233, 0.22);
  border-radius: 999px;
  padding: 9px 14px;
  background:
    radial-gradient(circle at 82% 18%, rgba(125, 211, 252, 0.12), transparent 40%),
    linear-gradient(180deg, rgba(255, 255, 255, 0.64), rgba(240, 249, 255, 0.38));
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.76),
    0 12px 32px rgba(59, 130, 246, 0.1);
  backdrop-filter: blur(14px) saturate(1.08);
  -webkit-backdrop-filter: blur(14px) saturate(1.08);
  transition: opacity 280ms ease, transform 280ms ease, border-color 280ms ease, box-shadow 280ms ease, background 280ms ease;
}

.education-background__meta-card--active {
  border-color: rgba(125, 211, 252, 0.3);
  background:
    radial-gradient(circle at 76% 16%, rgba(56, 189, 248, 0.34), transparent 48%),
    radial-gradient(circle at 50% 70%, rgba(186, 230, 253, 0.32), transparent 56%),
    linear-gradient(180deg, rgba(255, 255, 255, 0.8), rgba(224, 242, 254, 0.5));
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.86),
    inset 0 0 18px rgba(125, 211, 252, 0.22),
    0 14px 34px rgba(14, 165, 233, 0.2),
    0 0 28px rgba(56, 189, 248, 0.34);
  transform: translateY(-3px) scale(1.035);
}

.education-background__meta-card span {
  display: inline;
  color: rgba(2, 132, 199, 0.72);
  font-size: 12px;
  font-weight: 700;
  line-height: 1;
}

.education-background__meta-card strong {
  display: inline;
  margin-top: 0;
  color: rgba(15, 32, 51, 0.92);
  font-family: 'Noto Sans SC', 'PingFang SC', 'Microsoft YaHei', sans-serif;
  font-size: 13px;
  font-weight: 760;
  line-height: 1;
  white-space: nowrap;
}

.education-background__cards {
  position: absolute;
  left: 72px;
  top: 158px;
  display: grid;
  gap: 14px;
  width: 840px;
}

.education-background__card {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: space-between;
  min-height: 148px;
  overflow: hidden;
  border: 1px solid rgba(14, 165, 233, 0.24);
  border-radius: 22px;
  padding: 18px 30px;
  background:
    radial-gradient(circle at 78% 18%, rgba(125, 211, 252, 0.14), transparent 36%),
    linear-gradient(180deg, rgba(255, 255, 255, 0.64), rgba(240, 249, 255, 0.38));
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.78),
    0 16px 44px rgba(59, 130, 246, 0.12),
    0 0 0 1px rgba(255, 255, 255, 0.32);
  backdrop-filter: blur(14px) saturate(1.08);
  -webkit-backdrop-filter: blur(14px) saturate(1.08);
  transition: opacity 300ms ease, transform 300ms ease, border-color 300ms ease, box-shadow 300ms ease, background 300ms ease;
}

.education-background__card--active {
  border-color: rgba(125, 211, 252, 0.34);
  background:
    radial-gradient(circle at 78% 18%, rgba(56, 189, 248, 0.3), transparent 42%),
    radial-gradient(circle at 42% 80%, rgba(186, 230, 253, 0.28), transparent 58%),
    linear-gradient(180deg, rgba(255, 255, 255, 0.78), rgba(224, 242, 254, 0.5));
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.88),
    inset 0 0 34px rgba(125, 211, 252, 0.2),
    0 22px 54px rgba(14, 165, 233, 0.18),
    0 0 42px rgba(56, 189, 248, 0.32);
  transform: translateY(-3px) scale(1.008);
}

.education-background__card::after {
  position: absolute;
  right: -18%;
  bottom: -34%;
  width: 58%;
  height: 70%;
  content: "";
  background: radial-gradient(circle, rgba(14, 165, 233, 0.16), rgba(14, 165, 233, 0));
}

.education-background__card--secondary {
  border-color: rgba(6, 182, 212, 0.24);
  background:
    radial-gradient(circle at 78% 18%, rgba(45, 212, 191, 0.13), transparent 36%),
    linear-gradient(180deg, rgba(255, 255, 255, 0.62), rgba(236, 254, 255, 0.36));
}

.education-background__copy {
  position: relative;
  z-index: 1;
  min-width: 0;
  max-width: 650px;
}

.education-background__line {
  display: flex;
  align-items: baseline;
  gap: 22px;
  min-width: 0;
}

.education-background__school {
  flex: 0 0 auto;
  color: #0f2033;
  font-family: 'Noto Sans SC', 'PingFang SC', 'Microsoft YaHei', sans-serif;
  font-size: 27px;
  font-weight: 760;
  letter-spacing: 0.01em;
  line-height: 1.18;
}

.education-background__program {
  flex: 1 1 auto;
  min-width: 0;
  margin-top: 0;
  color: rgba(51, 65, 85, 0.78);
  font-size: 14px;
  font-weight: 650;
  line-height: 1.5;
}

.education-background__tags {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  margin-top: 12px;
}

.education-background__tags span {
  border: 1px solid rgba(14, 165, 233, 0.2);
  border-radius: 999px;
  padding: 5px 12px;
  background: rgba(255, 255, 255, 0.34);
  color: rgba(15, 32, 51, 0.82);
  font-size: 12px;
  font-weight: 650;
  line-height: 1;
}

.education-background__courses {
  max-width: 640px;
  margin: 12px 0 0;
  color: rgba(51, 65, 85, 0.76);
  font-size: 11px;
  font-weight: 600;
  line-height: 1.52;
}

.education-background__courses strong {
  color: rgba(2, 132, 199, 0.76);
  font-weight: 760;
}

.education-background__logo-wrap {
  position: relative;
  z-index: 1;
  display: flex;
  flex: 0 0 auto;
  align-items: center;
  justify-content: center;
  width: 82px;
  height: 82px;
  border: 1px solid rgba(14, 165, 233, 0.16);
  border-radius: 999px;
  background: rgba(255, 255, 255, 0.68);
  box-shadow: 0 14px 30px rgba(59, 130, 246, 0.12);
  backdrop-filter: blur(10px) saturate(1.06);
  -webkit-backdrop-filter: blur(10px) saturate(1.06);
  overflow: hidden;
}

.education-background__logo {
  width: 100%;
  height: 100%;
  object-fit: contain;
  padding: 11px;
}
</style>
