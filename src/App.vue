<template>
  <div id="app" @click="hided()">
    <div :class="status == 'pop_show' ? 'blur' : ''">
      <div class="title">
        CSS滤镜与混合模式
      </div>

      <div class="content">
        <div class="left">
          <div class="small_title">滤镜</div>

          <div :class="actived == 'filter_about' ? 'actived' : ''" @click="toggle('filter_about')">滤镜简介</div>

          <div :class="actived == 'filter_effect' ? 'actived' : ''" @click="toggle('filter_effect')">滤镜效果</div>

          <div :class="actived == 'filter_base' ? 'actived' : ''" @click="toggle('filter_base')">基础应用</div>

          <div :class="actived == 'filter_senior' ? 'actived' : ''" @click="toggle('filter_senior')">高级应用</div>

          <div class="small_title">混合模式</div>

          <div :class="actived == 'mix_about' ? 'actived' : ''" @click="toggle('mix_about')">混合模式简介</div>

          <div :class="actived == 'mix_blend' ? 'actived' : ''" @click="toggle('mix_blend')">混合模式应用</div>
        </div>
        
        <div class="right">
          <div v-if="actived == 'filter_about'">
            <h1>filter属性的作用是定义元素的可视效果</h1>
            
            <h2>基础属性值介绍</h2>

            <div class="filter_list" v-for="item of filter_list" :key="item.value">
              <h3>{{ item.value }}</h3>
              <h3>{{ item.describe }}</h3>
            </div>
          </div>

          <div class="filter_effect" v-if="actived == 'filter_effect'">
            <div class="picture">
              <h3>原图</h3>
              <img src="../src/assets/pc1.jpg">
            </div>

            <div v-for="filter of filter_list" :key="filter.describe">
              <h3>{{ filter.describe }}</h3>
              <h3>{{ filter.css }}</h3>
              <img :style="filter.css" src="../src/assets/pc1.jpg">
            </div>
          </div>

          <div class="filter_base" v-if="actived == 'filter_base'">
            <h2>1. filter:blur 基础应用</h2>
            <h3>一般情况下有两种使用场景，一个是把图片模糊后，作为背景图使用</h3>

            <a href="#" @click.stop="showBackground">查看效果</a>

            <br>
            <br>

            <h3>还有一个是应用于弹窗，当弹窗出现时把弹窗背后的元素模糊，可以让视觉更聚焦</h3>

            <a href="#" @click.stop="showPop">查看效果</a>

            <br>
            <br>
            <br>
            <br>

            <h2>2. filter:grayscale 基础应用</h2>

            <h3>在日常开发中，图标点亮和置灰是很常见的需求，传统的处理方式就是需要准备两张图片来切换显示</h3>
            <h3>使用滤镜我们就可以做到图标点亮或置灰时只需要准备一张彩图，灰图的实现，我们可以使用滤镜来控制</h3>

            <div class="filter_grayscale">
              <img src="../src/assets/logo.png">
              <img class="grayscale" src="../src/assets/logo.png">
            </div>

            <br>
            <br>

            <h3>特殊情况下大型网站灰色调处理</h3>

            <br>
            <br>
            <br>
            <br>

            <h2>3. filter:brightness 基础应用</h2>

            <h3>图标希望从深色变成白色</h3>

            <div class="filter_brightness">
              <div>
                <img src="../src/assets/pc2.png">
                <span>删除</span>
              </div>

              <div>
                <img class="brightness" src="../src/assets/pc2.png">
                <span>删除</span>
              </div>
            </div>
          </div>

          <div v-if="actived == 'filter_senior'">
            <h2>1. filter: hue-rotate 色彩动画</h2>
            <h3>下面是一个360度色调无缝旋转动画，这个动画可以用在任何元素上，可以实现一个色彩的流动效果</h3>

            <div class="filter_hue_rotate"></div>

            <br>

            <a href="#" @click.stop="showText">查看示例</a>

            <br>
            <br>

            <div v-if="text_status" class="filter_hue_rotate_text">
              CSS滤镜与混合模式分享
            </div>


            <br>
            <br>

            <h2>2. 径向模糊</h2>
            <h3>平常我们实现的模糊效果，都是整体模糊，实际上css是可以实现径向模糊的</h3>

            <a href="#" @click.stop="showBlur">查看示例</a>

            <br>
            <br>

            <div class="filter_blur" v-if="blur_status">
              <div>
                <img class="radial_blur" src="../src/assets/pc1.jpg">
                <img src="../src/assets/pc1.jpg">
              </div>

              <img class="radial_picture" src="../src/assets/pc1.jpg">
            </div>

          </div>

          <div v-if="actived == 'mix_about'">
            <h1>混合模式相关属性如下</h1>

            <h2>background-blend-mode 用于混合元素背景图案、渐变和颜色</h2>

            <h2>mix-blend-mode 用于元素与元素之间的混合</h2>

            <h2>基础属性值介绍</h2>

            <div class="blend_list" v-for="item of blend_list" :key="item.value">
              <h3>{{ item.value }}</h3>
              <h3>{{ item.describe }}</h3>
            </div>
          </div>

          <div v-if="actived == 'mix_blend'">
            <h2>1. mix-blend-mode:difference 文字背景反色</h2>

            <h3>差值模式。查看每个通道中的颜色信息，比较底色和绘图色，用较亮的像素点的像素值减去较暗的像素点的像素值。</h3>
            <h3>例如底色是红色,RGB值是(255, 0, 0),还有一个蓝色，其RGB值是(0, 0, 255)，使用差值混合模式后得到的颜色就是(255 - 0, 0 - 0, 255 - 0) = RGB(255, 0 , 255)。所以与白色混合将使底色反相；与黑色混合则不产生变化</h3>

            <a href="#" @click.stop="showDiff">查看示例</a>

            <br>
            <br>

            <div v-if="diff_status" class="mix_blend_diff">
              <div></div>
              <div>CSS滤镜与混合模式分享</div>
            </div>

            <br>
            <br>
            <br>
            <br>

            <h2>2. background-blend-mode:darken/lighten 图标变色</h2>

            <h3>变亮/变暗模式。混合颜色结果取决于两个颜色的对比，darken/变暗 是哪个颜色深显示哪个颜色，lighten/变亮 是哪个颜色浅显示哪个颜色</h3>

            <br>
            <br>

            <div class="mix_lighten"></div>

            <br>
            <br>
            <br>
            <br>

            <h2>3. mix-blend-mode:screen 滤色模式简介</h2>

            <h3>滤色模式。计算公式 C = 255 - ((255 - A) * (255 - B) / 255)</h3>
            <h3>公式中的 C 表示最终混合的RGB色值(范围是0-255)，A和B表示用来混合的两个颜色的RGB色值(范围也是0-255)</h3>
            <h3>例如有一个红色，其RGB值是(255, 0, 0)，还有一个蓝色，其RGB值是(0, 0, 255)</h3>

            <ul>
              <li><h3>R = 255 - (255 - 255) * (255 - 0) / 255 = 255</h3></li>
              <li><h3>G = 255 - (255 - 0) * (255 - 0) / 255 = 0</h3></li>
              <li><h3>B = 255 - (255 - 0) * (255 - 255) / 255 = 255</h3></li>
            </ul>

            <h3>最终的色值是 RGB(255, 0, 255)</h3>

            <br>
            <br>

            <div class="mix_screen">
              <div>
                <div></div>
                <div></div>
              </div>

              <div></div>
            </div>

            <br>
            <br>

            <h3>开发中我们不用去记住具体公式，只需要了解到下面提到的更直观特性</h3>

            <ul>
              <li><h3>任何颜色和黑色进行滤色，还是显示原来的颜色</h3></li>
              <li><h3>任何颜色和白色进行滤色，得到的是白色</h3></li>
              <li><h3>任何颜色和其他颜色进行滤色后的颜色会更浅，有点类似漂白的效果</h3></li>
            </ul>

            <br>
            <br>
            <br>
            <br>

            <h2>4. 图片滤色</h2>

            <h3>滤色模式对于在图像中加入场景特效是非常好用的</h3>

            <h3>下面有一张底图</h3>

            <div class="mix_img">
              <img src="../src/assets/pc5.jpg">
            </div>

            <h3>然后，有以下一些特效图</h3>

            <div style="display: flex; gap: 20px" class="mix_img">
              <img src="../src/assets/pc6.jpg">
              <img src="../src/assets/pc7.jpg">
              <img src="../src/assets/pc8.jpg">
              <img src="../src/assets/pc9.jpg">
            </div>

            <h3>分别和上面的底图进行混合，可以看到如下图所示的混合效果</h3>

            <a href="#" @click.stop="showMixImage">查看示例</a>

            <br>
            <br>

            <div v-if="mix_image" style="display: flex; gap: 20px" class="mix_img">
              <div>
                <img src="../src/assets/pc5.jpg">
                <img src="../src/assets/pc6.jpg">
              </div>

              <div>
                <img src="../src/assets/pc5.jpg">
                <img src="../src/assets/pc7.jpg">
              </div>

              <div>
                <img src="../src/assets/pc5.jpg">
                <img src="../src/assets/pc8.jpg">
              </div>

              <div>
                <img src="../src/assets/pc5.jpg">
                <img src="../src/assets/pc9.jpg">
              </div>
            </div>

            <br>
            <br>
            <br>
            <br>

            <h2>5. 视频滤色</h2>

            <h3>滤色混合模式不仅可以作用于图像，还可以用于视频，同样的，只要我们把视频的底色做成黑色，就能很好得和图片背景融为一体</h3>

            <h3>以下是两个黑色背景的视频特效素材</h3>

            <div class="mix_video">
              <video width="200" autoplay="" preload="auto" loop="" webkit-playsinline="true" playsinline="true" x5-video-player-type="h5" x5-video-orientation="portraint" x5-video-player-fullscreen="true" src="../src/assets/video1.mp4"></video>
              <video width="200" autoplay="" preload="auto" loop="" webkit-playsinline="true" playsinline="true" x5-video-player-type="h5" x5-video-orientation="portraint" x5-video-player-fullscreen="true" src="../src/assets/video2.mp4"></video>
            </div>

            <h3>通过设置video元素滤色混合模式，可以得到下面所示的视频效果</h3>

            <a href="#" @click.stop="showMixVideo">查看示例</a>

            <br>
            <br>

            <div v-if="mix_video" class="mix_video">
              <div>
                <video width="200" autoplay muted loop preload src="../src/assets/video1.mp4"></video>
              </div>

              <div>
                <video width="200" autoplay muted loop preload src="../src/assets/video2.mp4"></video>
              </div>
            </div>

            <br>
            <br>

            <h3>变暗混合模式与滤色混合模式结合使用，还可以实现融入背景的视频文字效果</h3>

            <a href="#" @click.stop="showMixTextVideo">查看示例</a>

            <br>
            <br>

            <div v-if="mix_text_video" class="mix_text_video">
              <video autoplay muted loop preload src="../src/assets/video3.mp4"></video>
              <div>混合模式</div>

              <div>混合模式</div>
            </div>
          </div>

          <div v-if="status == 'bg_show'" class="bg">
            <img src="../src/assets/pc3.jpg">
          </div>
        </div>
      </div>

    </div>

    <div v-if="status == 'pop_show'" class="pop">
      我是一个弹窗
    </div>

  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      actived: 'filter_about',
      filter_list: [
        {
          value: 'filter: blur',
          describe: '模糊',
          css: 'filter: blur(5px);'
        },
        {
          value: 'filter: brightness',
          describe: '亮度',
          css: 'filter: brightness(1.4);'
        },
        {
          value: 'filter: contrast',
          describe: '对比度',
          css: 'filter: contrast(2);'
        },
        {
          value: 'filter: drop-shadow',
          describe: '投影',
          css: 'filter: drop-shadow(4px 4px 8px blue);'
        },
        {
          value: 'filter: grayscale',
          describe: '灰度',
          css: 'filter: grayscale(50%);'
        },
        {
          value: 'filter: hue-rotate',
          describe: '色调变化',
          css: 'filter: hue-rotate(90deg);'
        },
        {
          value: 'filter: invert',
          describe: '反向',
          css: 'filter: invert(75%);'
        },
        {
          value: 'filter: opacity',
          describe: '透明度',
          css: 'filter: opacity(25%);'
        },
        {
          value: 'filter: saturate',
          describe: '饱和度',
          css: 'filter: saturate(230%);'
        },
        {
          value: 'filter: sepia',
          describe: '褐色',
          css: 'filter: sepia(60%);'
        }
      ],
      blend_list: [
        {
          value: 'mix/background-blend-mode: multiply',
          describe: '正片叠底'
        },
        {
          value: 'mix/background-blend-mode: screen',
          describe: '滤色'
        },
        {
          value: 'mix/background-blend-mode: overlay',
          describe: '叠加'
        },
        {
          value: 'mix/background-blend-mode: darken',
          describe: '变暗'
        },
        {
          value: 'mix/background-blend-mode: lighten',
          describe: '变亮'
        },
        {
          value: 'mix/background-blend-mode: color-dodge',
          describe: '颜色减淡'
        },
        {
          value: 'mix-blend-mode: color-burn',
          describe: '颜色加深'
        },
        {
          value: 'mix-blend-mode: hard-light',
          describe: '强光'
        },
        {
          value: 'mix-blend-mode: soft-light',
          describe: '柔光'
        },
        {
          value: 'mix-blend-mode: difference',
          describe: '差值'
        },
        {
          value: 'mix-blend-mode: exclusion',
          describe: '排除'
        },
        {
          value: 'mix-blend-mode: hue',
          describe: '色调'
        },
        {
          value: 'mix/background-blend-mode: saturation',
          describe: '饱和度'
        },
        {
          value: 'mix/background-blend-mode: color',
          describe: '颜色'
        },
        {
          value: 'mix/background-blend-mode: luminosity',
          describe: '亮度'
        }
      ],
      status: null,
      blur_status: false,
      text_status: false,
      diff_status: false,
      mix_image: false,
      mix_video: false,
      mix_text_video: false
    }
  },

  methods: {
    toggle(title) {
      this.actived = title
    },
    hided() {
      this.status = null
    },
    showBackground() {
      this.status = 'bg_show'
    },
    showPop() {
      this.status = 'pop_show'
    },
    showText() {
      this.text_status = true
    },
    showBlur() {
      this.blur_status = true
    },
    showDiff() {
      this.diff_status = true
    },
    showMixImage() {
      this.mix_image = true
    },
    showMixVideo() {
      this.mix_video = true
    },
    showMixTextVideo() {
      this.mix_text_video = true
    }
  }
}

</script>


<style>

body {
  margin: 0;
}

#app {
  font-family: Arial, sans-serif;
  text-align: center;
  background-color: #A0B3D6;
  width: 100vw;
  height: 100vh;
  padding-top: 30px;
  box-sizing: border-box;
}

.blur {
  filter: blur(5px);
}

.title {
  height: 60px;
  line-height: 60px;
  margin: 0;
  text-align: center;
  font-size: 32px;
  background: #c1d5eb;
  font-family: 'kaiti','microsoft yahei';
  font-weight: bold;
  width: 100%;
}

.content {
  display: flex;
  height: calc(100vh - 130px);
}

.content .left {
  width: 350px;
  height: 100%;
  text-align: left;
  background-color: #FFF;
}

.content .right {
  width: 100%;
  height: 100%;
  overflow-y: scroll;
  background-color: #F0F3F9;
  text-align: left;
  padding: 50px;
  padding-bottom: 100px;
  box-sizing: border-box;
  position: relative;
}

.content .left div {
  height: 70px;
  line-height: 70px;
  font-size: 22px;
  color: #4c5161;
  cursor: pointer;
  padding-left: 50px;
  box-sizing: border-box;
}

.content .left .small_title {
  height: 40px;
  color: #9facba;
  font-family: Arial, sans-serif;
  font-size: 20px;
  padding-left: 30px;
  font-weight: bold;
  line-height: 60px;
}

.content .left .actived {
  background-color: #F0F3F9;
}

.content .left div:hover {
  background-color: #F0F3F9;
}

.content .left .small_title:hover {
  background-color: #fff;
}

.filter_list {
  display: flex;
  justify-content: space-between;
  width: 300px;
}

.blend_list {
  display: flex;
  justify-content: space-between;
  width: 500px;
}

.blend_list:nth-child(6),
.blend_list:nth-child(9),
.blend_list:nth-child(14) {
  color: rgb(253, 66, 66);
}

.filter_list:nth-child(3),
.filter_list:nth-child(4),
.filter_list:nth-child(7),
.filter_list:nth-child(8) {
  color: rgb(253, 66, 66);
}

.filter_effect img {
  width: 300px;
  object-fit: cover;
  margin-bottom: 20px;
}

.filter_effect .picture {
  position: fixed;
  top: 200px;
  left: 344px;
}

.filter_effect div:nth-child(n+2) {
  padding-left: 500px;
  box-sizing: border-box;
}

.filter_effect div:nth-child(n+2) h3:nth-child(2) {
  color: rgb(253, 66, 66);
}

.filter_base {
  position: relative;
  z-index: 1;
}

.filter_base .filter_grayscale,
.filter_base .filter_brightness {
  display: flex;
  width: 400px;
  justify-content: space-between;
}

.filter_base .filter_grayscale img {
  width: 100px;
}

.filter_brightness div {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 4px;
  width: 100px;
  height: 45px;
  border-radius: 5px;
  cursor: pointer;
}

.filter_brightness div:first-child {
  color: #4c5161;
  border: 1px solid #d0d0d5;
  background-color: #fff;
}

.filter_brightness div:first-child:hover {
  border: 1px solid #2486ff;
  background-color: #2486ff;
  color: #fff;
}

.filter_brightness div:first-child:hover img{
  filter: brightness(100);
}

.filter_brightness div:last-child {
  border: 1px solid #2486ff;
  background-color: #2486ff;
  color: #fff;
}

.filter_brightness div img {
  width: 30px;
}

.filter_hue_rotate,
.filter_hue_rotate_text {
  width: 800px;
  height: 100px;
  background: linear-gradient(to right, red, orange, yellow, green, cyan, blue, purple);
  animation: hue 6s linear infinite;
}

.filter_hue_rotate_text {
  -webkit-background-clip: text;
  color: transparent;
  font-size: 60px;
}

.filter_blur {
  display: flex;
  gap: 100px;
}

.filter_blur div{
  width: 300px;
  height: 200px;
  position: relative;
  overflow: hidden;
}

.filter_blur img {
  width: 300px;
  object-fit: cover;
}

.filter_blur .radial_blur {
  position: absolute;
  inset: 0;
  filter: blur(30px);
  mask-image: radial-gradient(transparent, transparent 30%, black 60%);
  transform: scale(1.2);
}

.mix_blend_diff {
  width: 700px;
  height: 100px;
  overflow: hidden;
  position: relative;
  background-color: #000;
}

.mix_blend_diff div:first-child {
  /* display: none; */
  position: absolute;
  width: 1000px;
  height: 1000px;
  top: -450px;
  left: -150px;
  margin: auto;
  background: linear-gradient(#fff 50%, #000 50%);
  animation: spin 5s linear infinite;
}

.mix_blend_diff div:last-child {
  color: #fff;
  font-size: 50px;
  line-height: 100px;
  text-align: center;
  position: relative;
  mix-blend-mode: difference;
  z-index: 10;
}

.mix_lighten {
  width: 100px;
  height: 100px;
  background-blend-mode: lighten;
  background: url('../src/assets/pc4.png');
  background-size: 100%;
  background-color: #000;
}

.mix_screen {
  display: flex;
  gap: 100px;
}

.mix_screen > div {
  width: 300px;
  height: 200px;
}

.mix_screen > div:first-child {
  position: relative;
  z-index: 1
}

.mix_screen > div:last-child {
  background-color: rgb(255, 0, 255);
}

.mix_screen > div:first-child div {
  width: 300px;
  height: 200px;
}

.mix_screen > div:first-child div:first-child {
  background-color: rgb(255, 0, 0);
}

.mix_screen > div:first-child div:last-child {
  position: absolute;
  inset: 0;
  background-color: rgb(0, 0, 255);
  mix-blend-mode: screen;
}

.mix_img img {
  width: 200px;
}

.mix_img div {
  position: relative;
}

.mix_video {
  display: flex;
  gap: 20px;
}

.mix_video div {
  background: url('../src/assets/pc5.jpg');
  background-size: cover;
}

.mix_video div video {
  mix-blend-mode: screen;
}

.mix_img div img:last-child {
  position: absolute;
  inset: 0;
  mix-blend-mode: screen;
}

.mix_text_video {
  width: 900px;
  height: 500px;
  position: relative;
}

.mix_text_video video {
  width: 100%;
  height: 100%;
  position: absolute;
  inset: 0;
}

.mix_text_video div {
  font-size: 200px;
  font-weight: 700;
  line-height: 500px;
  text-align: center;
  font-style: italic;
}

.mix_text_video div:nth-child(2) {
  width: 100%;
  height: 100%;
  background: white;
  mix-blend-mode: screen;
  color: #000;
}

.mix_text_video div:last-child {
  position: absolute;
  inset: 0;
  background: #F0F3F9;
  color: transparent;
  z-index: 100;
  mix-blend-mode: darken;
}

.grayscale {
  filter: grayscale(1);
}

.brightness {
  filter: brightness(100);
}

.bg {
  position: absolute;
  inset: 0;
}

.bg img{
  width: 100%;
  height: 100%;
  filter: blur(60px);
  z-index: -1;
}

.pop {
  text-align: center;
  line-height: 300px;
  width: 500px;
  height: 300px;
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%,-50%);
  border: 1px solid #A0B3D6;
  background-color: #c1d5eb;
  font-size: 22px;
  font-weight: bold;
}

@keyframes hue {
  from { filter: hue-rotate(0deg); }
  to { filter: hue-rotate(360deg); }
}

@keyframes spin {
    from { transform: rotate(0deg); }
    to   {  transform: rotate(360deg); }
}

</style>
