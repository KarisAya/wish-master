<script setup>
// HeaderLogo组件 - 完美许愿器品牌标志
</script>

<template>
  <header class="header-logo">
    <h1 class="logo-text">完美许愿器</h1>
    <p class="logo-subtitle">" So tell me, what is it you truly desire? "</p>
  </header>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@1,400;1,700&display=swap');

.header-logo {
  text-align: center;
  padding: 30px 0 20px;
  margin-bottom: 15px;
}

.logo-text {
  font-size: 2.8rem;
  font-weight: 900;
  margin: 0;
  /* 换成了更深邃的紫黑渐变，有种魔法或契约的感觉 */
  background: linear-gradient(135deg, #2c3e50 0%, #000000 50%, #8e44ad 100%);
  -webkit-background-clip: text;
  background-clip: text;
  -webkit-text-fill-color: transparent;
  letter-spacing: 4px;
  filter: drop-shadow(0px 2px 2px rgba(0,0,0,0.1));
}

.logo-subtitle {
  font-size: 1.1rem;
  /* 使用衬线体并倾斜，增加那种优雅的恶魔质感 */
  font-family: 'Playfair Display', serif;
  font-style: italic;
  color: #555;
  margin: 12px 0 0;
  font-weight: 400;
  letter-spacing: 0.5px;
}

@media (max-width: 768px) {
  .logo-text {
    font-size: 2.2rem;
    letter-spacing: 2px;
  }
  
  .logo-subtitle {
    font-size: 0.95rem;
  }
}
</style>