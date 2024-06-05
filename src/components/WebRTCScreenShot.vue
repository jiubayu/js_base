<template>
    <div>
        <div class="screenShot">
            <video width="640px" height="480px" ref="myVideo"></video>
            <canvas width="640px"  height="480px" ref="mycanvas"></canvas>
        </div>
        <div >
            <a @click="changeToCamerra" class="btn">摄像头</a>
            <a @click="changeToDesktop" class="btn">桌面</a>
            <a @click="shot" class="btn">截图</a>
            <a @click="download" class="btn">下载</a>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'screenShot',
        data() {
            return {}
        },
        methods:{
            // 开始捕捉屏幕
            async changeToDesktop() {
                let stream = await window.navigator.mediaDevices.getDisplayMedia();
                // 将MediaStream输出到video标签
                this.$refs.myVideo.srcObject = stream;
                this.$refs.myVideo.play();
            },
            changeToCamerra() {
                window.navigator.getUserMedia({video: true}, (stream) => {
                    this.$refs.myVideo.srcObject = stream;
                    this.$refs.myVideo.play();
                })
            },
            shot() {
                let context = this.$refs.mycanvas.getContext('2d');
                context.drawImage(this.$refs.myVideo, 0,0,640,480,0,0,640,480)
            },
            download() {
                var dataImg = new Image();
                dataImg.src = this.$refs.mycanvas.toDataURL('image/png');
                document.body.appendChild(dataImg);
                var link = document.createElement('a');
                link.href = dataImg.src;
                link.download = 'screenshot',
                document.body.appendChild(link);
                link.click();
            }
        }
    }
</script>

<style lang="less" scoped>
.screenShot {
  display: flex;
  position: relative;
  border: 1px #ccc solid;
  width: 650px;
  height: 540px;
}
.btn{
    margin: 0 20px;
}
</style>