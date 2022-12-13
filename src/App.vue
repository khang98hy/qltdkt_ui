<script setup>
import TheHeaderVue from './components/TheHeader.vue';
import TheSidebarVue from './components/TheSidebar.vue';
import TheContentVue from './components/TheContent.vue';
import ModalAddVue from './components/ModalAdd.vue';
</script>

<template>
  
  <div class="block">
    <TheHeaderVue/>
    <div class="container">
      <TheSidebarVue/>
      <TheContentVue/>
    </div>
    <ModalAddVue/>
  </div>
</template>

<style scoped>
@import url(./styles/main.css);
.block{
  display: flex;
  flex-direction: column ;
}
.container {
  display: flex;
  flex: 1;
  width: 100vw;
  height: calc(100vh - 56px);
}

</style>