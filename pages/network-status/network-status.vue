<template>
  <view class="container">
    <view class="card">
      <view class="section-title">网络状态监听</view>
      <view class="info-text">当前网络类型：{{ networkTypeLabel }}</view>
      <view class="info-text">是否已连接：{{ isConnected ? '是' : '否' }}</view>
      <button class="primary-button" type="default" @tap="initNetworkStatus">
        手动刷新网络状态
      </button>
      <view class="tips">
        <view class="info-text">提示：切换手机的网络状态（如打开飞行模式、切换 Wi-Fi/4G）时，将会自动更新并弹出提示。</view>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      networkType: 'unknown',
      isConnected: false
    };
  },
  computed: {
    networkTypeLabel() {
      const map = {
        wifi: 'Wi-Fi',
        '2g': '2G',
        '3g': '3G',
        '4g': '4G',
        '5g': '5G',
        none: '无网络',
        unknown: '未知'
      };
      return map[this.networkType] || this.networkType;
    }
  },
  onLoad() {
    this.handleNetworkChange = this.handleNetworkChange.bind(this);
    this.initNetworkStatus();
    uni.onNetworkStatusChange(this.handleNetworkChange);
  },
  onUnload() {
    if (this.handleNetworkChange) {
      uni.offNetworkStatusChange(this.handleNetworkChange);
    }
  },
  methods: {
    initNetworkStatus() {
      uni.getNetworkType({
        success: res => {
          this.networkType = res.networkType;
          this.isConnected = res.networkType !== 'none';
        },
        fail: () => {
          uni.showToast({
            title: '获取网络状态失败',
            icon: 'none'
          });
        }
      });
    },
    handleNetworkChange(res) {
      this.networkType = res.networkType;
      this.isConnected = res.isConnected;
      uni.showToast({
        title: `网络已切换为：${this.networkTypeLabel}`,
        icon: 'none'
      });
    }
  }
};
</script>

<style scoped>
.tips {
  margin-top: 24rpx;
  border-top: 1px dashed #e0e0e0;
  padding-top: 16rpx;
}
</style>
