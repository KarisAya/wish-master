<!-- src/views/WishResultCardPreview.vue -->
<template>
  <div class="preview-container">
    <WishResultCard 
      :signData="sampleData" 
      @restart="handleRestart" 
    />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import WishResultCard from '../components/WishResultCard.vue';

const sampleData = ref({
  confirmed_wish: "希望获得完美的人生体验",
  score: 10,
  realization_scenario: "经过精心规划和逻辑严谨的思考，愿望已成功实现"
});

function handleRestart() {
  console.log('重新开始');
}
</script>