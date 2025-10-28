<template>
  <view class="container">
    <view class="card">
      <view class="section-title">作业功能列表</view>
      <view class="info-text">请选择需要体验的功能页面：</view>
      <view class="nav-list">
        <button class="primary-button" type="default" @tap="goTo('pages/system-info/system-info')">
          系统信息展示
        </button>
        <button class="primary-button" type="default" @tap="goTo('pages/network-status/network-status')">
          网络状态监听
        </button>
        <button class="primary-button" type="default" @tap="goTo('pages/image-picker/image-picker')">
          图片选择功能
        </button>
        <button class="primary-button" type="default" @tap="goTo('pages/storage/storage')">
          本地存储演示
        </button>
        <button class="primary-button" type="default" @tap="goTo('pages/clipboard/clipboard')">
          剪贴板功能
        </button>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  methods: {
    goTo(url) {
      uni.navigateTo({
        url: `/${url}`
      });
    }
  }
};
</script>

<style scoped>
.nav-list {
  display: flex;
  flex-direction: column;
}
</style>
