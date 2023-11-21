<template>
  <div class="viewTitle">
    <h1>ロケットを選ぼう🚀</h1>

    <!-- 撮影を開始するボタン -->
    <button @click="startCamera">撮影を開始する</button>

    <!-- カメラの映像表示 -->
    <video v-if="showCamera" ref="videoElement" autoplay></video>

    <!-- 撮影ボタン -->
    <button v-if="showCaptureButton" @click="captureImage">撮影</button>

    <!-- ロケット作成へボタン -->
    <button v-if="showCreateRocketButton" @click="createRocket">
      ロケット作成へ
    </button>
  </div>
</template>

<script lang="ts">
export default {
  data() {
    return {
      showCamera: false,
      showCaptureButton: false,
      showCreateRocketButton: false,
      cameraStream: null,
    };
  },
  methods: {
    // カメラを開始するメソッド
    startCamera() {
      this.showCamera = true;
      const videoElement = this.$refs.videoElement as HTMLVideoElement;

      // カメラのストリームを取得
      navigator.mediaDevices
        .getUserMedia({ video: true })
        .then((stream) => {
          videoElement.srcObject = stream;
          if (videoElement.srcObject !== null) {
            this.showCaptureButton = true;
          }
        })
        .catch((error) => {
          console.error("Error accessing camera:", error);
        });
    },

    // 画像を撮影するメソッド
    captureImage() {
      // ここに画像のキャプチャロジックを追加
      this.showCaptureButton = true;
      this.showCreateRocketButton = true;
    },

    // ロケットを作成するメソッド
    createRocket() {
      // ここにロケット作成のロジックを追加
      this.$router.push("/main/generaterocket");
    },
  },
};
</script>

<style src="../assets/main.css" scoped />
