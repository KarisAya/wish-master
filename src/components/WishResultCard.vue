<script setup>
import { ref, onMounted, nextTick } from 'vue';
import { animate } from 'animejs';

// 动态添加 DaisyUI CSS (保持你的原始逻辑)
onMounted(() => {
  if (!document.querySelector('link[href*="daisyui"]')) {
    const link = document.createElement('link');
    link.rel = 'stylesheet';
    link.href = 'https://cdn.bootcdn.net/ajax/libs/daisyui/4.12.23/full.min.css';
    document.head.appendChild(link);
  }
});

const props = defineProps({
  signData: {
    type: Object,
    required: true // 包含 confirmed_wish 和 realization_scenario
  }
});

const emit = defineEmits(['restart']);
const cardRef = ref(null);

function handleRestart() {
  emit('restart');
}

onMounted(async () => {
  await nextTick();
  if (cardRef.value) {
    animate(cardRef.value, {
      opacity: [0, 1],
      scale: [0.9, 1],
      duration: 1000,
      easing: 'easeOutElastic(1, .8)'
    });
  }
});
</script>

<template>
  <div class="result-card-container">
    <div ref="cardRef" class="card bg-base-100 shadow-xl">
      <div class="contract-header"></div>
      
      <div class="card-body">
        <div class="wish-section">
          <div class="label-tag">原定愿望</div>
          <h2 class="wish-title">「 {{ props.signData.confirmed_wish }} 」</h2>
        </div>

        <div class="divider">契约达成情况</div>
        
        <div class="realization-section">
          <div class="label-tag danger">实现场景 (逻辑检查通过)</div>
          <p class="scenario-text">
            {{ props.signData.realization_scenario }}
          </p>
          
          <div class="contract-seal">已达成</div>
        </div>

        <div class="disclaimer">
          警告：本系统遵循严格的逻辑演绎，任何利益受损均由许愿者逻辑不严密引起。<br>
          Powered by DeepSeek & 完美许愿器 v2.0
        </div>
      </div>
    </div>

    <div class="action-buttons">
      <button @click="handleRestart" class="btn btn-primary btn-wide shadow-lg">
        重新修正愿望 w
      </button>
    </div>
  </div>
</template>

<style scoped>
.result-card-container {
  max-width: 600px;
  margin: 0 auto;
  padding: 1rem;
  display: flex;
  flex-direction: column;
  gap: 2rem;
}

.card {
  background: #fff9f0 !important; /* 像旧纸张一样的颜色 */
  border: 2px solid #2c3e50;
  color: #2c3e50 !important;
  opacity: 0;
  position: relative;
  overflow: hidden;
}

.contract-header {
  height: 12px;
  background: repeating-linear-gradient(
    45deg,
    #2c3e50,
    #2c3e50 10px,
    #e74c3c 10px,
    #e74c3c 20px
  );
}

.label-tag {
  font-size: 0.75rem;
  font-weight: bold;
  text-transform: uppercase;
  color: #7f8c8d;
  margin-bottom: 0.5rem;
  letter-spacing: 1px;
}

.label-tag.danger {
  color: #e74c3c;
}

.wish-title {
  font-size: 1.4rem;
  font-weight: 800;
  text-align: center;
  padding: 1rem 0;
  font-style: italic;
}

.divider {
  font-size: 0.8rem;
  color: #bdc3c7;
  margin: 0.5rem 0;
}

.realization-section {
  position: relative;
  background: rgba(44, 62, 80, 0.03);
  padding: 1.5rem;
  border-radius: 8px;
  border: 1px dashed #bdc3c7;
  min-height: 150px;
}

.scenario-text {
  font-size: 1.1rem;
  line-height: 1.8;
  color: #2c3e50;
  z-index: 1;
  position: relative;
  white-space: pre-wrap;
}

/* 装饰性印章样式 */
.contract-seal {
  position: absolute;
  right: 10px;
  bottom: 10px;
  width: 80px;
  height: 80px;
  border: 3px solid rgba(231, 76, 60, 0.4);
  border-radius: 50%;
  color: rgba(231, 76, 60, 0.4);
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: bold;
  transform: rotate(-20deg);
  font-size: 1.2rem;
  pointer-events: none;
  user-select: none;
}

.disclaimer {
  font-size: 0.7rem;
  color: #95a5a6;
  text-align: center;
  margin-top: 1.5rem;
  padding-top: 1rem;
  border-top: 1px solid rgba(0,0,0,0.05);
}

.action-buttons {
  display: flex;
  justify-content: center;
}

.btn-primary {
  background-color: #2c3e50 !important;
  border-color: #2c3e50 !important;
  color: white !important;
}

@media (max-width: 640px) {
  .wish-title { font-size: 1.1rem; }
  .scenario-text { font-size: 1rem; }
}
</style>