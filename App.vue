<script>
export default {
  onLaunch() {
    console.log('App Launch');
  },
  onShow() {
    console.log('App Show');
  },
  onHide() {
    console.log('App Hide');
  }
};
</script>

<style>
/* 全局页面背景与字体 */
page {
  background-color: #f7f7f7;
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  color: #333;
}

.container {
  padding: 24rpx 32rpx;
}

.section-title {
  font-size: 32rpx;
  font-weight: 600;
  margin-bottom: 16rpx;
}

.card {
  background-color: #fff;
  border-radius: 16rpx;
  padding: 24rpx;
  box-shadow: 0 8rpx 24rpx rgba(0, 0, 0, 0.08);
}

.primary-button {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 20rpx 32rpx;
  margin: 12rpx 0;
  border-radius: 999rpx;
  background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
  color: #fff;
  font-size: 28rpx;
}

.primary-button:active {
  opacity: 0.85;
}

.info-text {
  font-size: 28rpx;
  line-height: 1.6;
  margin-bottom: 8rpx;
  word-break: break-all;
}
</style>
