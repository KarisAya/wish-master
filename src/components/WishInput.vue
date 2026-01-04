<script setup>
import { ref, computed } from 'vue';

// 定义组件事件
const emit = defineEmits(['submit']);

// 愿望输入
const wishInput = ref('');
const isSubmitting = ref(false);
const maxLength = 50;

// 更改为更有“欲望感”的示例
const exampleWishes = [
  '想要永远不用工作',
  '希望变身亿万富翁',
  '想让大家都听我的'
];

// 处理提交
function handleSubmit() {
  if (!wishInput.value.trim() || isSubmitting.value) return;
  if (wishInput.value.length > maxLength) return;
  
  isSubmitting.value = true;
  emit('submit', wishInput.value);
  
  // 重置状态
  setTimeout(() => {
    isSubmitting.value = false;
  }, 500);
}

// 填充示例愿望
function fillExampleWish(wish) {
  wishInput.value = wish;
}

// 计算剩余字数
const remainingChars = computed(() => {
  return maxLength - wishInput.value.length;
});
</script>

<template>
  <div class="wish-input-container">
    <h2 class="input-title">契约内容</h2>
    
    <div class="input-wrapper">
      <input
        v-model="wishInput"
        type="text"
        class="wish-input"
        placeholder="在此写下你渴望之物..."
        :maxlength="maxLength"
        @keyup.enter="handleSubmit"
      />
      <span class="char-counter" :class="{ 'warning': remainingChars < 10 }">
        {{ remainingChars }}
      </span>
    </div>
    
    <button 
      @click="handleSubmit" 
      class="submit-button"
      :disabled="!wishInput.trim() || wishInput.length > maxLength || isSubmitting"
    >
      <span v-if="!isSubmitting">签订契约</span>
      <span v-else class="loading-dots">因果计算中<span>.</span><span>.</span><span>.</span></span>
    </button>
    
    <div class="examples-container">
      <p class="examples-title">常见欲望：</p>
      <div class="examples-list">
        <button 
          v-for="(wish, index) in exampleWishes" 
          :key="index"
          @click="fillExampleWish(wish)"
          class="example-item"
        >
          {{ wish }}
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.wish-input-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
  max-width: 500px;
  margin: 0 auto;
}

.input-title {
  font-size: 1.2rem;
  margin-bottom: 20px;
  color: #2c3e50;
  text-align: center;
  font-weight: 600;
  letter-spacing: 2px;
}

.input-wrapper {
  position: relative;
  width: 100%;
  margin-bottom: 20px;
}

.wish-input {
  width: 100%;
  padding: 14px 45px 14px 18px;
  font-size: 1.1rem;
  /* 黑色边框增加契约严肃感 */
  border: 2px solid #2c3e50;
  border-radius: 4px; 
  background-color: transparent;
  transition: all 0.3s;
}

.wish-input:focus {
  outline: none;
  box-shadow: 0 0 10px rgba(44, 62, 80, 0.2);
  border-color: #8e44ad; /* 聚焦时带点紫色 */
}

.char-counter {
  position: absolute;
  right: 12px;
  top: 50%;
  transform: translateY(-50%);
  font-size: 0.8rem;
  color: #999;
}

.char-counter.warning {
  color: #e74c3c;
}

.submit-button {
  background-color: #2c3e50;
  color: white;
  border: none;
  padding: 14px 32px;
  font-size: 1.1rem;
  border-radius: 4px;
  cursor: pointer;
  transition: all 0.3s;
  min-width: 160px;
  letter-spacing: 2px;
  font-weight: bold;
}

.submit-button:hover:not(:disabled) {
  background-color: #000;
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(0,0,0,0.2);
}

.submit-button:disabled {
  background-color: #bdc3c7;
  cursor: not-allowed;
}

.examples-container {
  margin-top: 30px;
  width: 100%;
}

.examples-title {
  font-size: 0.85rem;
  color: #7f8c8d;
  margin-bottom: 10px;
  text-align: center;
}

.examples-list {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 10px;
}

.example-item {
  background-color: transparent;
  border: 1px dashed #bdc3c7;
  border-radius: 4px;
  padding: 5px 12px;
  font-size: 0.85rem;
  color: #7f8c8d;
  cursor: pointer;
  transition: all 0.2s;
}

.example-item:hover {
  border-style: solid;
  border-color: #8e44ad;
  color: #8e44ad;
  background-color: rgba(142, 68, 173, 0.05);
}

/* 加载动画 */
.loading-dots span {
  animation: loadingDots 1.4s infinite;
  animation-fill-mode: both;
}

@keyframes loadingDots {
  0% { opacity: 0.2; }
  20% { opacity: 1; }
  100% { opacity: 0.2; }
}
</style>