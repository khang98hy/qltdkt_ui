<template>
  <div class="header">
    <div class="header-left">
      <div class="home-icon"></div>
      <div class="logo-icon"></div>
      <span>MISA CeGov</span>
    </div>
    <div class="header-right">
      <div class="notifications-icon tooltip">
        <span class="tooltiptext">Thông báo</span>
      </div>
      <div class="help-icon tooltip">
        <span class="tooltiptext">Hướng dẫn</span>
      </div>
      <div class="documents-icon tooltip">
        <span class="tooltiptext">Văn bản quy định</span>
      </div>
      <div class="setting-icon tooltip">
        <span class="tooltiptext">Thiết đặt hệ thống</span>
      </div>
      <div class="avatar-icon"></div>
    </div>
  </div>
</template>

<script>

export default {
}
</script>

<style scoped>
.tooltip {
  position: relative;
  display: inline-block;
}

.tooltip .tooltiptext {
  visibility: hidden;
  width: 120px;
  background-color: black;
  color: #fff;
  text-align: center;
  border-radius: 6px;
  padding: 5px 0;
  /* Xác định vị trí tooltip */
  position: absolute;
  z-index: 1;
  top: 40px;
  left: 50%;
  margin-left: -60px;
}

.tooltip:hover .tooltiptext {
  visibility: visible;
}

.header {
  display: flex;
  height: 56px;
  width: 100%;
  background-color: var(--background-sidebar);
  border-bottom:2px solid #1b0c0121;
  justify-content: space-between;
}

.header-left {
  display: flex;
  align-items: center;
}

.header-right {
  display: flex;
  align-items: center;
}

.home-icon {
  background: url('../assets/Icons/sprites.svg') no-repeat -196px -4px;
  width: 16px;
  height: 16px;
  margin: 20px;
}

.logo-icon {
  width: 32px;
  height: 32px;
  background: url('../assets/Icons/logo.svg');
  background-size: 32px;
  margin-right: 12px;
}

.header-left>span {
  font-weight: 700;
  font-size: 20px;
}

.avatar-icon {
  height: 32px;
  width: 32px;
  background-image: url(../assets/Icons/getavatar.png);
  background-size: 32px;
  margin-right: 8px;
}

.avatar-icon:hover {
  cursor: pointer;
}

.setting-icon {
  background: url('../assets/Icons/sprites.svg') no-repeat -266px -170px;
  width: 24px;
  height: 24px;
  margin-right: 12px;
  position: relative;
}

.setting-icon:hover {
  cursor: pointer;
}

.documents-icon {
  background: url('../assets/Icons/ic_document.svg') no-repeat;
  width: 24px;
  height: 24px;
  margin-right: 12px;
  position: relative;
}

.documents-icon:hover {
  cursor: pointer;
}

.help-icon {
  background: url('../assets/Icons/sprites.svg') no-repeat -50px -50px;
  width: 24px;
  height: 24px;
  margin-right: 12px;
  position: relative;
}

.notifications-icon {
  background: url('../assets/Icons/sprites.svg') no-repeat -26px -50px;
  width: 24px;
  height: 24px;
  margin-right: 12px;
  position: relative;
}
</style>