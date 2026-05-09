<template>
  <section class="project-intro">
    <div
      class="project-intro__section-title"
      :class="$clicks === 0 ? 'project-intro__section-title--center' : ($clicks === 1 ? 'project-intro__section-title--back' : 'project-intro__section-title--gone')"
    >
      个人技术能力展示
    </div>

    <div
      class="project-intro__project-title"
      :class="$clicks < 1 ? 'project-intro__project-title--hidden' : ($clicks === 1 ? 'project-intro__project-title--center' : 'project-intro__project-title--top')"
    >
      AI 控制智能家居 · ESP32-S3 端侧项目
    </div>

    <div
      class="project-intro__content"
      :class="{ 'project-intro__content--visible': $clicks >= 2 }"
    >
      <article class="project-intro__summary">
        <p>
          围绕 ESP32-S3 端侧设备自研的一套 AI 家居控制框架，把“语音唤醒 → 模型对话 → 工具调用 → 硬件执行 → 状态回报”串成完整闭环。
        </p>
      </article>

      <article class="project-intro__video-card" @click.stop="playVideo">
        <video
          ref="videoRef"
          class="project-intro__video"
          src="/videos/demo.mp4"
          controls
          preload="metadata"
          playsinline
          @play="isPlaying = true"
          @pause="isPlaying = false"
          @ended="isPlaying = false"
          @click.stop
        />
        <button
          v-if="!isPlaying"
          class="project-intro__play"
          type="button"
          aria-label="播放演示视频"
          @click.stop="playVideo"
        >
          <span class="i-carbon:play-filled-alt" />
          <strong>点击播放演示</strong>
        </button>
      </article>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const videoRef = ref<HTMLVideoElement | null>(null)
const isPlaying = ref(false)

function playVideo() {
  const video = videoRef.value
  if (!video)
    return

  video.play()
    .then(() => {
      isPlaying.value = true
    })
    .catch(() => {
      isPlaying.value = false
    })
}
</script>

<style scoped>
.project-intro {
  position: absolute;
  inset: 0;
  overflow: hidden;
  color: #0f2033;
  font-family: var(--deck-cn-serif);
}

.project-intro__section-title,
.project-intro__project-title {
  position: absolute;
  left: 50%;
  width: max-content;
  max-width: none;
  white-space: nowrap;
  color: #0f2033;
  font-family: var(--deck-cn-serif);
  font-weight: 700;
  letter-spacing: 0;
  transform: translateX(-50%);
  transition: opacity 700ms ease-in-out, transform 700ms ease-in-out, filter 700ms ease-in-out;
}

.project-intro__section-title {
  font-size: 3.75rem;
  line-height: 1;
}

.project-intro__section-title--center {
  top: 50%;
  opacity: 1;
  transform: translate(-50%, -50%) scale(1);
}

.project-intro__section-title--back {
  top: 50%;
  opacity: 0.2;
  transform: translate(-50%, calc(-50% - 6rem)) scale(0.92);
}

.project-intro__section-title--gone {
  top: 50%;
  opacity: 0;
  filter: blur(4px);
  transform: translate(-50%, calc(-50% - 7rem)) scale(0.9);
}

.project-intro__project-title {
  font-size: 2.25rem;
  line-height: 1.18;
}

.project-intro__project-title--hidden {
  top: 52%;
  opacity: 0;
  transform: translate(-50%, 2.6rem) scale(0.96);
}

.project-intro__project-title--center {
  top: 50%;
  opacity: 1;
  transform: translate(-50%, -50%) scale(1);
}

.project-intro__project-title--top {
  top: 17.5%;
  opacity: 1;
  transform: translateX(-50%) scale(1);
}

.project-intro__content {
  position: absolute;
  left: 8%;
  right: 8%;
  top: 33%;
  bottom: 10%;
  display: grid;
  grid-template-columns: minmax(0, 0.82fr) minmax(0, 1.18fr);
  gap: 20px;
  opacity: 0;
  filter: blur(4px);
  transform: translateY(40px);
  transition: opacity 700ms ease-in-out, transform 700ms ease-in-out, filter 700ms ease-in-out;
}

.project-intro__content--visible {
  opacity: 1;
  filter: blur(0);
  transform: translateY(0);
}

.project-intro__summary,
.project-intro__video-card {
  position: relative;
  overflow: hidden;
  border: 1px solid rgba(14, 165, 233, 0.24);
  border-radius: 18px;
  background:
    radial-gradient(circle at 78% 18%, rgba(125, 211, 252, 0.2), transparent 38%),
    linear-gradient(180deg, rgba(255, 255, 255, 0.82), rgba(224, 242, 254, 0.54));
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.9),
    0 18px 48px rgba(59, 130, 246, 0.16),
    0 0 0 1px rgba(255, 255, 255, 0.34);
  backdrop-filter: blur(18px) saturate(1.08);
  -webkit-backdrop-filter: blur(18px) saturate(1.08);
}

.project-intro__summary {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 26px 28px;
}

.project-intro__summary p {
  display: block;
  width: 100%;
  margin: 0;
  color: rgba(15, 32, 51, 0.86);
  font-size: 16px;
  font-weight: 650;
  line-height: 1.82;
  text-align: center;
  overflow-wrap: anywhere;
}

.project-intro__video-card {
  cursor: pointer;
  min-height: 0;
}

.project-intro__video {
  width: 100%;
  height: 100%;
  min-height: 0;
  object-fit: contain;
  background: rgba(15, 32, 51, 0.08);
}

.project-intro__play {
  position: absolute;
  inset: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 10px;
  border: 0;
  color: #0f2033;
  background:
    radial-gradient(circle at 50% 42%, rgba(255, 255, 255, 0.78), transparent 30%),
    linear-gradient(180deg, rgba(224, 242, 254, 0.42), rgba(15, 23, 42, 0.08));
  font-family: 'Noto Sans SC', 'PingFang SC', 'Microsoft YaHei', sans-serif;
}

.project-intro__play span {
  color: rgba(2, 132, 199, 0.92);
  font-size: 44px;
  filter: drop-shadow(0 0 20px rgba(56, 189, 248, 0.38));
}

.project-intro__play strong {
  font-size: 15px;
  font-weight: 780;
  letter-spacing: 0.03em;
}
</style>
