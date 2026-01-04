<script setup>
import { ref, reactive } from 'vue';
import { useRouter } from 'vue-router';
import HeaderLogo from '../components/HeaderLogo.vue';
import WishInput from '../components/WishInput.vue';
import StepFlow from '../components/StepFlow.vue';
import WishResultCard from '../components/WishResultCard.vue'; // 暂时复用组件，建议后续改名
import AppFooter from '../components/AppFooter.vue';

// 路由
const router = useRouter();

// 状态管理
// 0: 输入愿望, 1: 审查愿望, 2: 正在构建现实(钻漏洞), 3: 展示结果
const currentStep = ref(0); 
const wishText = ref('');
const isLoading = ref(false);
const error = ref(null);

// 愿望实现结果数据
const wishResult = reactive({
  confirmed_wish: '',
  realization_scenario: '', // 存储LLM生成的反转剧情
});

/**
 * 处理愿望提交逻辑
 */
async function handleWishSubmit(wish) {
  currentStep.value = 1; // 进入“审查与构建”状态
  isLoading.value = true;
  
  try {
    const response = await fetch('/api/validateWish', {
      method: 'POST',
      body: JSON.stringify({ wish })
    });
    const data = await response.json();

    if (data.result.category === 'block') {
      router.push('/error'); // 违规处理
      return;
    }

    // 直接拿到了结果！
    wishResult.confirmed_wish = data.result.confirmed_wish;
    wishResult.realization_scenario = data.result.scenario;
    
    currentStep.value = 3; // 直接跳到展示结果
  } catch (err) {
    error.value = "因果律崩溃了w";
  } finally {
    isLoading.value = false;
  }
}

/**
 * 重新开始许愿
 */
function handleRestart() {
  currentStep.value = 0;
  wishText.value = '';
  error.value = null;
  wishResult.confirmed_wish = '';
  wishResult.realization_scenario = '';
}

// --- API 调用函数 ---

async function validateWish(wish) {
  const response = await fetch('/api/validateWish', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ wish })
  });
  if (!response.ok) throw new Error(`验证失败: ${response.status}`);
  return await response.json();
}

async function generateWishRealization(wish) {
  // 注意：这里建议后端接口也统一命名为 generateWish 
  const response = await fetch('/api/generateWish', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ wish })
  });
  
  if (!response.ok) throw new Error(`愿望实现失败: ${response.status}`);
  return await response.json();
}
</script>

<template>
  <div class="home-container">
    <HeaderLogo />
    
    <div v-if="error" class="error-message">
      {{ error }}
    </div>
    
    <div v-if="currentStep === 0" class="input-section">
      <WishInput @submit="handleWishSubmit" />
    </div>
    
    <div v-else-if="currentStep < 3" class="processing-section">
      <StepFlow :current-step="currentStep" />
    </div>
    
    <div v-else class="result-section">
      <WishResultCard 
        :sign-data="wishResult" 
        @restart="handleRestart"
      />
    </div>
    
    <AppFooter />
  </div>
</template>

<style scoped>
.home-container {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

.error-message {
  background-color: #fff3e0;
  color: #e65100;
  padding: 12px 16px;
  border-radius: 8px;
  margin: 16px 0;
  border: 1px solid #ffe0b2;
  text-align: center;
}

.input-section, .processing-section, .result-section {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  padding: 10px 0;
  margin-top: -10px;
}
</style>