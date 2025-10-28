<template>
  <view class="container">
    <view class="card">
      <view class="section-title">本地存储演示</view>
      <view class="info-text">
        该页面会读取图片选择页面保存的图片路径，以及系统信息页面保存的手机型号，并在下次打开时自动显示。
      </view>
      <view class="info-text">存储的手机型号：{{ cachedModel || '暂无数据，请先前往系统信息页面获取。' }}</view>
      <view class="info-text">存储的图片路径：{{ cachedImagePath || '暂无数据，请先前往图片选择页面选择。' }}</view>
      <view v-if="cachedImagePath" class="preview">
        <image class="preview-image" :src="cachedImagePath" mode="aspectFit"></image>
      </view>
      <button class="primary-button" type="default" @tap="loadFromStorage">
        重新读取本地缓存
      </button>
      <button class="primary-button" type="default" @tap="clearStorage">
        清空缓存数据
      </button>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      cachedModel: '',
      cachedImagePath: ''
    };
  },
  onLoad() {
    this.loadFromStorage();
  },
  onShow() {
    this.loadFromStorage();
  },
  methods: {
    loadFromStorage() {
      const model = uni.getStorageSync('deviceModel');
      const imagePath = uni.getStorageSync('selectedImagePath');
      this.cachedModel = model || '';
      this.cachedImagePath = imagePath || '';
    },
    clearStorage() {
      uni.removeStorageSync('deviceModel');
      uni.removeStorageSync('selectedImagePath');
      this.cachedModel = '';
      this.cachedImagePath = '';
      uni.showToast({
        title: '缓存已清空',
        icon: 'none'
      });
    }
  }
};
</script>

<style scoped>
.preview {
  margin: 24rpx 0;
}

.preview-image {
  width: 100%;
  height: 400rpx;
  border-radius: 16rpx;
  background-color: #f0f0f0;
}
</style>
