<template>
  <div>
    <h1 class="overview-title">汇报的三个部分</h1>
    <span class="overview-subtitle">从个人背景、综合能力到技术能力展示</span>

    <div mt-4></div>

    <div flex justify-center>
      <div
        v-motion
        :initial="{ opacity: 0, y: 40 }"
        :enter="{ opacity: 1, y: 0, transition: { duration: 600 } }"
        grid
        grid-cols-3
        gap-4
        w-full
        class="text-sm"
      >
        <div
          border="2 solid yellow-800"
          bg="yellow-800/8"
          rounded-lg
          overflow-hidden
          transition-all
          duration-500
          min-h-78
          :class="$clicks === 1 ? 'scale-106 z-10 opacity-100' : ($clicks > 0 ? 'scale-100 opacity-55' : 'scale-100 opacity-100')"
          :style="$clicks === 1 ? 'box-shadow: 0 0 0 2px rgba(217,119,6,0.85), 0 24px 60px rgba(217,119,6,0.38);' : ''"
        >
          <div
            h-full
            bg="yellow-800/12"
            px-6
            py-6
            flex
            flex-col
            items-center
            justify-center
            gap-8
            text-center
          >
            <div i-carbon:education text-5xl opacity-90></div>
            <div class="overview-card-title">
              个人背景介绍
            </div>
          </div>
        </div>

        <div
          border="2 solid cyan-800"
          bg="cyan-800/8"
          rounded-lg
          overflow-hidden
          transition-all
          duration-500
          min-h-78
          :class="$clicks === 2 ? 'scale-106 z-10 opacity-100' : ($clicks > 0 ? 'scale-100 opacity-55' : 'scale-100 opacity-100')"
          :style="$clicks === 2 ? 'box-shadow: 0 0 0 2px rgba(8,145,178,0.9), 0 24px 60px rgba(8,145,178,0.4);' : ''"
        >
          <div
            h-full
            bg="cyan-800/12"
            px-6
            py-6
            flex
            flex-col
            items-center
            justify-center
            gap-8
            text-center
          >
            <div i-carbon:user-multiple text-5xl opacity-90></div>
            <div class="overview-card-title">
              个人荣誉与综合能力
            </div>
          </div>
        </div>

        <div
          border="2 solid blue-800"
          bg="blue-800/8"
          rounded-lg
          overflow-hidden
          transition-all
          duration-500
          min-h-78
          :class="$clicks === 3 ? 'scale-106 z-10 opacity-100' : ($clicks > 0 ? 'scale-100 opacity-55' : 'scale-100 opacity-100')"
          :style="$clicks === 3 ? 'box-shadow: 0 0 0 2px rgba(59,130,246,0.9), 0 24px 60px rgba(59,130,246,0.4);' : ''"
        >
          <div
            h-full
            bg="blue-800/12"
            px-6
            py-6
            flex
            flex-col
            items-center
            justify-center
            gap-8
            text-center
          >
            <div i-carbon:code text-5xl opacity-90></div>
            <div class="overview-card-title">
              个人技术能力展示
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.overview-title {
  margin: 0;
  color: #0f2033;
  font-family: 'Noto Sans SC', 'PingFang SC', 'Microsoft YaHei', sans-serif;
  font-size: 38px;
  font-weight: 760;
  letter-spacing: 0.02em;
  line-height: 1.16;
  text-shadow: 0 10px 34px rgba(96, 165, 250, 0.18);
}

.overview-subtitle {
  display: inline-block;
  margin-top: 12px;
  color: rgba(51, 65, 85, 0.74);
  font-family: var(--deck-cn-serif);
  font-size: 17px;
  font-weight: 650;
  line-height: 1.45;
}

.overview-card-title {
  color: rgba(15, 32, 51, 0.92);
  font-family: 'Noto Sans SC', 'PingFang SC', 'Microsoft YaHei', sans-serif;
  font-size: 24px;
  font-weight: 760;
  letter-spacing: 0.01em;
  line-height: 1.22;
}
</style>
