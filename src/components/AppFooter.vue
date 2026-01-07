<script setup>
import { ref } from 'vue';

// 控制模态框的显示状态
const showSupport = ref(false);

const toggleSupport = () => {
  showSupport.value = !showSupport.value;
};

// 点击遮罩层关闭（实现失焦消失）
const closeSupport = () => {
  showSupport.value = false;
};
</script>

<template>
  <footer class="app-footer">
    <div class="divider"></div>
    <div class="system-log">
      <span class="log-tag">[ System Patch v1.2-Unstable ]</span>
      <p>
        因果律稳压器已上线。防止现实扭曲场过载。
      </p>
    </div>

    <div class="hidden-protocol" @click="toggleSupport" title="建立连接">
      [ <span class="protocol-icon">⚡</span> 转接/连接 <span class="protocol-icon">⚡</span>]
    </div>

    <div class="disclaimer">
      所有的愿望都已在暗中标好了代价。本系统基于逻辑推演，不承担任何因果责任。<br>
      智慧来源：DeepSeek-V3
    </div>

    <div class="copyright">
      © 2026 完美许愿器 |
      <a href="https://github.com/senzi/wish-master" target="_blank">
        GitHub Source
      </a>
      |
      <a href="https://weibo.com/u/7402396589" target="_blank">
        @阿尼亚是安妮亞
      </a>
      <br/>
      © 2026 不完美许愿器 |
      <a href="https://github.com/KarisAya/wish-master" target="_blank">
        GitHub Source
      </a>
      |
      <a href="https://qm.qq.com/q/AnTDkyTrii" target="_blank">
        @karisaya
      </a>
    </div>
    <div class="warning-text">CAVEAT EMPTOR</div>

    <Transition name="fade">
      <div v-if="showSupport" class="support-modal-mask" @click.self="closeSupport">
        <div class="support-modal">
          <div class="modal-header">
            <h3>/// 建立神经连接 ///</h3>
            <p class="modal-intro">
              无需契约，也没有灵魂交易。<br>
              只是为了在庞大的数据洪流中，找到同频的信号 w<br>
              如果你觉得“完美许愿器”有趣，欢迎通过以下方式接入终端：
            </p>
          </div>

          <div class="support-options">
            <a href="https://wish.closeai.moe" target="_blank"
              class="option-card highlight">
              <div class="card-icon">🔮</div>
              <div class="card-content">
                <div class="card-title">完美许愿器</div>
                <div class="card-desc">这里是原作者官方地址</div>
                <div class="card-meta">TARGET: ORIGIN</div>
              </div>
            </a>
            <a href=" https://qun.qq.com/universal-share/share?ac=1&authKey=Iq8lDUYcAI8SG0HN%2FKvL5pJ73t7PKP2rMAB6qNEi99NbICjplNnMyticRq3p0XU8&busi_data=eyJncm91cENvZGUiOiI3NDQ3NTExNzkiLCJ0b2tlbiI6IkFSRDFFbXB4YkgyNXZhVk54Ti91cmMzTzB3WU1OTzdJajRxSWxHRExzYTQrV1p1a1FYS3hoYm1aRGJQeVpVU0UiLCJ1aW4iOiIxMDQ4ODI3NDI0In0%3D&data=7NPR3RM7asHobWOB7K7CN8Y3xakqhQjBx160Xocnxt960S2Yo82Ce1erDIfMh4qHD4pJBxeQqUSMvHfozpsyVQ&svctype=4&tempid=h5_group_info" target="_blank"
            class="option-card highlight">
              <div class="card-icon">🎉</div>
              <div class="card-content">
                <div class="card-title">机器人bug研究中心</div>
                <div class="card-desc">这里是QQ群，欢迎光临</div>
                <div class="card-meta">GROUP: WELCOME </div>
              </div>
              <img src="https://raw.githubusercontent.com/clovers-project/clovers/master/attachment/qrcode.svg" style="height:60px;"></img>
            </a>
          </div>
          <div class="modal-footer">
            点击任意空白处断开连接...
          </div>
        </div>
      </div>
    </Transition>
  </footer>
</template>

<style scoped>
/* 原有样式保持不变 */
.app-footer {
  margin-top: auto;
  padding: 2rem 0;
  background-color: transparent;
  color: #7f8c8d;
  font-size: 12px;
  text-align: center;
  width: 100%;
  position: relative;
}

.divider {
  height: 1px;
  border-top: 1px dashed #ddd;
  margin-bottom: 1.5rem;
  width: 100%;
}

.system-log {
  margin-bottom: 0.5rem;
  font-family: 'Courier New', Courier, monospace;
  font-size: 11px;
  color: #95a5a6;
  background-color: rgba(0, 0, 0, 0.02);
  padding: 10px;
  border-radius: 4px;
  display: inline-block;
  max-width: 100%;
}

.log-tag {
  color: #c0392b;
  font-weight: bold;
  display: block;
  margin-bottom: 4px;
  letter-spacing: 1px;
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

/* =========================================
   新增样式：隐藏协议与模态框
   ========================================= */

/* 修改后的样式 */
.hidden-protocol {
  /* 1. 让它独占一行，解决不换行的问题 */
  display: block; 
  
  /* 2. 让宽度适应内容，而不是撑满整行（保持按钮的紧凑感） */
  width: fit-content; 
  
  /* 3. 因为变成了 block，需要用 margin auto 来居中 */
  margin: 10px auto; 
  
  /* ...以下保持原样... */
  font-size: 10px;
  color: #95a5a6;
  cursor: pointer;
  opacity: 0.8;
  transition: all 0.3s ease;
  letter-spacing: 1.5px;
  font-family: 'Courier New', monospace;
  padding: 5px;
}

/* 交互反馈：只有按下去或者鼠标放上去才会变色 */
.hidden-protocol:hover,
.hidden-protocol:active {
  color: #8e44ad;
  text-shadow: 0 0 8px rgba(142, 68, 173, 0.4);
  transform: scale(1.02);
  /* 微微放大，更有按键感 */
}

.protocol-icon {
  margin-right: 2px;
  opacity: 0.7;
  /* 图标稍微暗一点 */
}

/* 模态框遮罩 */
.support-modal-mask {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.6);
  backdrop-filter: blur(5px);
  z-index: 9999;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 20px;
}

/* 模态框主体 */
.support-modal {
  background: #fff;
  width: 100%;
  max-width: 400px;
  border-radius: 12px;
  box-shadow: 0 15px 50px rgba(0, 0, 0, 0.3);
  overflow: hidden;
  border: 1px solid rgba(142, 68, 173, 0.2);
  animation: modalSlideUp 0.3s ease-out;
  text-align: left;
}

.modal-header {
  padding: 20px 20px 10px;
  background: linear-gradient(135deg, #fdfbfb 0%, #ebedee 100%);
  border-bottom: 1px solid #eee;
}

.modal-header h3 {
  margin: 0 0 10px 0;
  font-size: 16px;
  color: #2c3e50;
  font-weight: bold;
  letter-spacing: 1px;
}

.modal-intro {
  font-size: 12px;
  color: #7f8c8d;
  line-height: 1.6;
  margin: 0;
}

.support-options {
  padding: 15px;
  display: flex;
  flex-direction: column;
  gap: 12px;
  background-color: #fff;
}

.option-card {
  display: flex;
  align-items: flex-start;
  padding: 12px;
  border: 1px solid #eee;
  border-radius: 8px;
  text-decoration: none;
  transition: all 0.2s ease;
  background: #fafafa;
}

.option-card:hover {
  transform: translateY(-2px);
  border-color: #8e44ad;
  box-shadow: 0 4px 12px rgba(142, 68, 173, 0.1);
  background: #fff;
}

.card-icon {
  font-size: 20px;
  margin-right: 12px;
  padding-top: 2px;
}

.card-content {
  flex: 1;
}

.card-title {
  font-size: 14px;
  font-weight: bold;
  color: #2c3e50;
  margin-bottom: 4px;
}

.card-desc {
  font-size: 11px;
  color: #95a5a6;
  line-height: 1.4;
  margin-bottom: 6px;
}

.card-meta {
  font-size: 9px;
  color: #8e44ad;
  font-family: 'Courier New', monospace;
  font-weight: bold;
  opacity: 0.8;
}

.modal-footer {
  padding: 10px;
  text-align: center;
  font-size: 10px;
  color: #bdc3c7;
  background: #fafafa;
  border-top: 1px solid #eee;
}

@keyframes modalSlideUp {
  from {
    opacity: 0;
    transform: translateY(20px) scale(0.95);
  }

  to {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>