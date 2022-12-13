<template>
    <div class="sidebar" :class="{ 'sidebar-mini': isSidebarMini }">
        <div class="sidebar-item tooltip" v-for="(item, index) in sidebarItems" :key="index"
            @mouseover="isAction = !isAction" @click="sidebarItemActive = index"
            :class="{ 'sidebar-item--active': sidebarItemActive == index }">
            <img :src="item.icon" alt="" />
            <span v-show="!isSidebarMini">{{ item.name }}</span>
            <span class="tooltiptext" v-if="isSidebarMini">{{ item.name }}</span>
        </div>

        <div class="sidebar-item sidebar-footer" @click="isSidebarMini = !isSidebarMini"
            :class="{ 'sidebar-mini': isSidebarMini , 'expand-btn' : isSidebarMini}">
            <img class="btn-navigation" src="../assets/Icons/ic_toggle.svg" alt=""
                :class="{ 'rotage-icon': isSidebarMini }" />
            <span class="sidebar-header__title" style="color: black" v-show="!isSidebarMini">Thu gọn</span>
        </div>
    </div>
</template>
  
<script setup>
import { ref } from "vue";
const isAction = false
const isSidebarMini = ref(false)
const sidebarItemActive = ref(7)
const sidebarItems = [
    {
        icon: require("@/assets/Icons/ic_dashboard_default.svg"),
        name: "Tổng quan",
        iconAction: require("@/assets/Icons/ic_dashboard.svg"),
    },
    {
        icon: require("@/assets/Icons/ic_movement_default.svg"),
        name: "Thi đua",
        iconAction: require("@/assets/Icons/ic_movement.svg"),
    },
    {
        icon: require("@/assets/Icons/ic_reward_default.svg"),
        name: "Khen thưởng",
        iconAction: require("@/assets/Icons/ic_reward.svg"),
    },
    {
        icon: require("@/assets/Icons/ic_decision_menu_default.svg"),
        name: "Quyết định",
        iconAction: require("@/assets/Icons/ic_decision_menu.svg"),
    },
    {
        icon: require("@/assets/Icons/ic_profile_default.svg"),
        name: "Hồ sơ",
        iconAction: require("@/assets/Icons/ic_profile.svg"),
    },
    {
        icon: require("@/assets/Icons/ic_search_default.svg"),
        name: "Tra cứu",
        iconAction: require("@/assets/Icons/ic_search.svg"),
    },
    {
        icon: require("@/assets/Icons/ic_report_default.svg"),
        iconAction: require("@/assets/Icons/ic_report.svg"),
        name: "Báo cáo",
    },
    {
        icon: require("@/assets/Icons/ic_category_default.svg"),
        iconAction: require("@/assets/Icons/ic_category.svg"),
        name: "Danh mục",
    },
    {
        icon: require("@/assets/Icons/ic_setting_default.svg"),
        iconAction: require("@/assets/Icons/ic_setting.svg"),
        name: "Thiết lập",
    },
    {
        icon: require("@/assets/Icons/ic_guide_default.svg"),
        iconAction: require("@/assets/Icons/ic_guide.svg"),
        name: "Hướng dẫn",
    },
];

</script>
  
<style scoped>
@import url(../styles/sidebar.css);
</style>
  