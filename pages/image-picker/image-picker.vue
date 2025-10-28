<template>
  <view class="container">
    <view class="card">
      <view class="section-title">图片选择功能</view>
      <view class="info-text">点击下方按钮可从相册选择或调用相机拍摄一张图片。</view>
      <button class="primary-button" type="default" @tap="chooseImage">
        选择/拍摄图片
      </button>
      <view v-if="imagePath" class="preview">
        <image class="preview-image" :src="imagePath" mode="aspectFit"></image>
        <view class="info-text">已选择图片路径：{{ imagePath }}</view>
      </view>
      <view v-else class="info-text">暂未选择图片。</view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      imagePath: ''
    };
  },
  onLoad() {
    const cached = uni.getStorageSync('selectedImagePath');
    if (cached) {
      this.imagePath = cached;
    }
  },
  methods: {
    chooseImage() {
      uni.chooseImage({
        count: 1,
        sizeType: ['original', 'compressed'],
        sourceType: ['album', 'camera'],
        success: res => {
          const path = res.tempFilePaths[0];
          this.imagePath = path;
          uni.setStorage({
            key: 'selectedImagePath',
            data: path
          });
          uni.showToast({
            title: '图片选择成功',
            icon: 'success'
          });
        },
        fail: () => {
          uni.showToast({
            title: '未能选择图片',
            icon: 'none'
          });
        }
      });
    }
  }
};
</script>

<style scoped>
.preview {
  margin-top: 24rpx;
}

.preview-image {
  width: 100%;
  height: 400rpx;
  border-radius: 16rpx;
  background-color: #f0f0f0;
}
</style>
