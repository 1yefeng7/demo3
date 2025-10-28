<template>
  <view class="container">
    <view class="card">
      <view class="section-title">系统信息展示</view>
      <view class="info-text">以下为通过 <text style="font-weight: 600;">uni.getSystemInfo</text> 获取到的设备信息：</view>
      <view v-if="systemInfo">
        <view class="info-text">手机品牌：{{ systemInfo.brand }}</view>
        <view class="info-text">手机型号：{{ systemInfo.model }}</view>
        <view class="info-text">系统：{{ systemInfo.system }}</view>
        <view class="info-text">屏幕高度：{{ systemInfo.screenHeight }} px</view>
        <view class="info-text">屏幕宽度：{{ systemInfo.screenWidth }} px</view>
        <view class="info-text">平台：{{ systemInfo.platform }}</view>
        <view class="info-text">语言：{{ systemInfo.language }}</view>
      </view>
      <view v-else class="info-text">正在获取系统信息...</view>
      <button class="primary-button" type="default" @tap="fetchSystemInfo">
        重新获取系统信息
      </button>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      systemInfo: null
    };
  },
  onLoad() {
    this.fetchSystemInfo();
  },
  methods: {
    fetchSystemInfo() {
      uni.getSystemInfo({
        success: res => {
          this.systemInfo = res;
          // 将手机型号保存到本地缓存，供其他页面读取
          uni.setStorage({
            key: 'deviceModel',
            data: res.model
          });
          uni.setStorage({
            key: 'systemInfo',
            data: res
          });
        },
        fail: () => {
          uni.showToast({
            title: '获取系统信息失败',
            icon: 'none'
          });
        }
      });
    }
  }
};
</script>

<style scoped>
</style>
