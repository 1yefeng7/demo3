<template>
  <view class="container">
    <view class="card">
      <view class="section-title">剪贴板功能</view>
      <view class="info-text">当前手机型号：{{ deviceModel || '未获取到设备型号' }}</view>
      <button class="primary-button" type="default" @tap="copyModel">
        复制手机型号到剪贴板
      </button>
      <view class="info-text tips">
        如果型号为空，请先前往“系统信息展示”页面获取最新信息。
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      deviceModel: ''
    };
  },
  onLoad() {
    this.loadModel();
  },
  onShow() {
    this.loadModel();
  },
  methods: {
    loadModel() {
      const model = uni.getStorageSync('deviceModel');
      if (model) {
        this.deviceModel = model;
      } else {
        uni.getSystemInfo({
          success: res => {
            this.deviceModel = res.model;
            uni.setStorage({
              key: 'deviceModel',
              data: res.model
            });
          }
        });
      }
    },
    copyModel() {
      if (!this.deviceModel) {
        uni.showToast({
          title: '暂无可复制的型号',
          icon: 'none'
        });
        return;
      }
      uni.setClipboardData({
        data: this.deviceModel,
        success: () => {
          uni.showToast({
            title: '已复制到剪贴板',
            icon: 'success'
          });
        }
      });
    }
  }
};
</script>

<style scoped>
.tips {
  margin-top: 16rpx;
  color: #666;
}
</style>
