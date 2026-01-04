<script setup>
import { computed } from 'vue';

// 接收当前步骤作为prop
const props = defineProps({
  currentStep: {
    type: Number,
    required: true,
    // 现在 1 是审查，2 是生成场景，3 是准备展示
    validator: (value) => value >= 1 && value <= 3
  }
});

// 步骤文本：改成了更有“完美许愿器”风格的文案w
const steps = [
  { id: 1, text: '正在审查愿望契约...' },
  { id: 2, text: '正在寻找逻辑漏洞...' },
  { id: 3, text: '正在构建讽刺现实...' }
];

// 计算当前激活的步骤
const activeStep = computed(() => {
  return props.currentStep;
});
</script>

<template>
  <div class="step-flow">
    <div class="steps-container">
      <div 
        v-for="step in steps" 
        :key="step.id"
        class="step"
        :class="{ 
          'active': step.id === activeStep,
          'completed': step.id < activeStep
        }"
      >
        <div class="step-indicator">
          <div class="step-circle">
            <span v-if="step.id < activeStep" class="step-check">✓</span>
            <span v-else class="step-number">{{ step.id }}</span>
          </div>
          <div class="step-line" v-if="step.id < steps.length"></div>
        </div>
        <div class="step-content">
          <p class="step-text">{{ step.text }}</p>
          <div v-if="step.id === activeStep" class="step-animation">
            <span class="dot"></span>
            <span class="dot"></span>
            <span class="dot"></span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
/* 样式部分基本保持原样，但我调了一下颜色，让它看起来不那么“求签” */
.step-flow {
  width: 100%;
  max-width: 500px;
  margin: 0 auto;
}

.steps-container {
  display: flex;
  flex-direction: column;
  gap: 24px; /* 增加一点间距，显得更大气 */
}

.step {
  display: flex;
  align-items: flex-start;
}

.step-indicator {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-right: 16px;
}

.step-circle {
  width: 32px;
  height: 32px;
  border-radius: 50%;
  background-color: #f5f5f5;
  border: 2px solid #ddd;
  display: flex;
  justify-content: center;
  align-items: center;
  font-weight: bold;
  color: #999;
  transition: all 0.3s ease;
}

/* 激活和完成时使用更符合“契约”感的墨色或深青色 */
.step.active .step-circle {
  background-color: #2c3e50;
  border-color: #2c3e50;
  color: white;
}

.step.completed .step-circle {
  background-color: #42b883; /* 完成仍用绿色，表示安全通过 */
  border-color: #42b883;
  color: white;
}

.step-check {
  font-size: 14px;
}

.step-number {
  font-size: 14px;
}

.step-line {
  height: 24px;
  width: 2px;
  background-color: #ddd;
  margin-top: 4px;
  transition: background-color 0.3s ease;
}

.step.completed .step-line {
  background-color: #42b883;
}

.step-content {
  padding-top: 4px;
}

.step-text {
  margin: 0;
  font-size: 1rem;
  color: #999;
  transition: color 0.3s ease;
}

.step.active .step-text {
  color: #2c3e50;
  font-weight: 600;
}

.step.completed .step-text {
  color: #42b883;
}

.step-animation {
  display: flex;
  gap: 4px;
  margin-top: 8px;
}

.dot {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background-color: #2c3e50;
  animation: pulse 1.5s infinite ease-in-out;
}

.dot:nth-child(2) { animation-delay: 0.2s; }
.dot:nth-child(3) { animation-delay: 0.4s; }

@keyframes pulse {
  0%, 100% { transform: scale(0.8); opacity: 0.4; }
  50% { transform: scale(1.2); opacity: 1; }
}

@media (max-width: 768px) {
  .step-text { font-size: 0.95rem; }
}
</style>