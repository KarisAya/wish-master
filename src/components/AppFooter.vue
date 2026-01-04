<script setup>
// AppFooter.vue - 页面底部组件
</script>

<template>
  <footer class="app-footer">
    <div class="divider"></div>
    <div class="disclaimer">
      所有的愿望都已在暗中标好了代价。本系统基于逻辑推演，不承担任何因果责任。<br>
      智慧来源：DeepSeek-V3 
    </div>
    <div class="copyright">
      © 2026 完美许愿器 | 
      <a href="https://github.com/senzi/wish-master" target="_blank">
        GitHub Source
      </a>
    </div>
    <div class="warning-text">CAVEAT EMPTOR</div>
  </footer>
</template>

<style scoped>
.app-footer {
  margin-top: auto; /* 确保在内容不足时也沉在底部 */
  padding: 2rem 0;
  background-color: transparent;
  color: #7f8c8d;
  font-size: 12px;
  text-align: center;
  width: 100%;
}

.divider {
  height: 1px;
  /* 使用更暗淡的虚线，增加陈旧感 */
  border-top: 1px dashed #ddd;
  margin-bottom: 1.5rem;
  width: 100%;
}

.disclaimer {
  margin-bottom: 0.8rem;
  line-height: 1.8;
  font-style: italic;
}

.copyright {
  line-height: 1.5;
  letter-spacing: 1px;
}

.copyright a {
  color: #2c3e50;
  text-decoration: none;
  border-bottom: 1px solid #bdc3c7;
  transition: all 0.3s ease;
}

.copyright a:hover {
  color: #8e44ad;
  border-bottom-color: #8e44ad;
}

.warning-text {
  margin-top: 1rem;
  font-size: 10px;
  letter-spacing: 4px;
  color: #bdc3c7;
  font-weight: bold;
}

@media (max-width: 768px) {
  .app-footer {
    padding: 1.5rem 10px;
  }
}
</style>