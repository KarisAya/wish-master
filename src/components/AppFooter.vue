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
    <div class="hidden-protocol" @click="toggleSupport" title="建立连接">
      [ <span class="protocol-icon">⚡</span> 支持/连接 <span class="protocol-icon">⚡</span>]
    </div>

    <div class="disclaimer">
      所有的愿望都已在暗中标好了代价。本系统基于逻辑推演，不承担任何因果责任。<br>
      智慧来源：DeepSeek-V4-flash 
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
            <a href="https://vipclub.weibo.com/vmember/gfopend?F=profile&vuid=7402396589" target="_blank"
              class="option-card highlight">
              <div class="card-icon">🌀</div>
              <div class="card-content">
                <div class="card-title">潜入内部圈子</div>
                <div class="card-desc">加入微博专属社群，与更多有趣的灵魂闲聊，或许能发现系统的后门 w</div>
                <div class="card-meta">ACCESS: YEARLY PASS</div>
              </div>
            </a>

            <div class="option-card donation-complex">
              <a href="https://weibo.com/7402396589/QlQNWszJ0" target="_blank" class="donation-link-part">
                <div class="card-icon">☕</div>
                <div class="card-content">
                  <div class="card-title">
                    投喂单次补给
                    <span class="link-arrow">↗</span>
                  </div>
                  <div class="card-desc">点击前往微博打赏，或向下查看二维码 w</div>
                  <div class="card-meta">DONATION: OPEN</div>
                </div>
              </a>

              <div class="donation-divider"></div>

              <div class="donation-qr-part">
                <img src="/sponsor.png" alt="Sponsor QR" class="mini-qr">
                <span class="qr-hint">WeChat Scan / 微信扫码</span>
              </div>
            </div>

            <a href="https://weibo.com/u/7402396589" target="_blank" class="option-card">
              <div class="card-icon">👁️</div>
              <div class="card-content">
                <div class="card-title">成为观测者</div>
                <div class="card-desc">关注本身就是一种量子纠缠。你的注视能让这个不稳定的系统更加“存在”。</div>
                <div class="card-meta">STATUS: FOLLOW</div>
              </div>
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

.creepy-note {
  display: block;
  margin-top: 4px;
  font-size: 10px;
  color: #bdc3c7;
  font-style: italic;
  transform: scale(0.95);
  transition: all 0.5s ease;
}

.system-log:hover .creepy-note {
  color: #8e44ad;
  text-shadow: 0 0 5px rgba(142, 68, 173, 0.3);
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

/* 覆盖默认的 option-card 布局，改为垂直排列 */
.option-card.donation-complex {
  display: flex;
  flex-direction: column;
  padding: 0;
  /* 清除默认内边距，由内部控制 */
  gap: 0;
  cursor: default;
  /* 外层不显示手型，手型给链接部分 */
  overflow: hidden;
  /* 保证圆角 */
  background: #fff;
  transition: box-shadow 0.3s ease;
}

/* 鼠标放上去时，整体稍微浮起一点点 */
.donation-complex:hover {
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.08);
  border-color: #bdc3c7;
  transform: translateY(-2px);
}

/* 上半部分：链接区域 */
.donation-link-part {
  display: flex;
  align-items: flex-start;
  padding: 12px;
  text-decoration: none;
  width: 100%;
  transition: background-color 0.2s ease;
}

/* 链接区域的 Hover 效果 */
.donation-link-part:hover {
  background-color: #f8f9fa;
}

.donation-link-part:hover .card-title {
  color: #8e44ad;
}

.link-arrow {
  font-size: 10px;
  margin-left: 4px;
  opacity: 0.5;
}

/* 分割线：虚线，内敛的关键 */
.donation-divider {
  width: 90%;
  height: 1px;
  border-top: 1px dashed #eee;
  margin: 0 auto;
}

/* 下半部分：二维码区域 */
.donation-qr-part {
  padding: 12px;
  display: flex;
  flex-direction: column;
  /* 垂直排列图片和文字 */
  align-items: center;
  background-color: #fff;
}

/* 二维码图片：小巧精致 */
.mini-qr {
  width: 100px;
  /* 控制在 100px，非常内敛 */
  height: 100px;
  object-fit: contain;
  border-radius: 6px;
  margin-bottom: 6px;
  opacity: 0.9;
  transition: all 0.3s ease;
}

/* 鼠标悬停二维码时，稍微清晰一点，暗示可交互 */
.donation-qr-part:hover .mini-qr {
  opacity: 1;
  transform: scale(1.05);
}

.qr-hint {
  font-size: 9px;
  color: #bdc3c7;
  font-family: 'Courier New', monospace;
  letter-spacing: 1px;
  transform: scale(0.9);
  /* 字体再小一点 */
}
</style>