<template>
<el-row class="full-screen-center">

<!--  <el-row :gutter="20" justify="start" align="center">-->
<!--    <h1>Cabbage Engine</h1>-->
<!--  </el-row>-->

<!--<el-row :gutter="20" type="flex" class="column" justify="start" align="center" style="margin-top: 12%;margin-left: 5%">-->
  <el-row :gutter="20" type="flex" class="column" justify="start" align="center" style="margin-top: 20vh;margin-left: 7vw;;width: 90vw;">
  <el-col :gutter="10">
    <el-button class="custom-button" type="primary" @click="goToSecondPage">继续游戏</el-button>
  </el-col>
  <el-col :gutter="10">
    <el-button class="custom-button" type="primary" @click="goToSecondPage">新建游戏</el-button>
  </el-col>
  <el-col :gutter="10">
    <el-button class="custom-button" type="primary" @click="uploadFile">加载游戏</el-button>
  </el-col>
  <el-col :gutter="10">
    <el-button class="custom-button" type="primary">游戏设置</el-button>
  </el-col>
  <el-col :gutter="10">
    <el-button class="custom-button" type="primary">退出游戏</el-button>
  </el-col>
<!--  <el-col :gutter="10">-->
<!--    <el-button class="decorate-button" type="primary"></el-button>-->
<!--  </el-col>-->
</el-row>

  <el-row type="flex" class="column" justify="end" align="center" style="margin-top: 5%;margin-right: 4%">
<!--  <el-col justify="center" align="end">-->
<!--&lt;!&ndash;    <el-button class="custom-button" type="primary" @click="dialogVisible = true" size="medium">公告</el-button>&ndash;&gt;-->
<!--  </el-col>-->
  <el-col justify="center" align="end">
    <el-text size="medium" class="custom-font" style="margin-top: 0px;"> version 0.3.0</el-text>
  </el-col>
  </el-row>

  <el-dialog
      v-model="dialogVisible"
      :modal="false"
      :close-on-click-modal="false"
      :close-on-press-escape="false"
      :show-close="false"
      draggable
      :z-index="998"
      class="my-custom-dialog"
      @before-close="handleClose">
      <el-tabs v-model="activeName" class="demo-tabs" @tab-click="handleClick">
      <el-tab-pane label="公告" name="first" class="broadTab">
        <img class="broadImg" src="../assets/imgs/broad.png"/>
      </el-tab-pane>
      <el-tab-pane label="致谢" name="second" class="regardsTab">
        <el-text size="medium" class="message-font">制作团队</el-text>
        <el-text size="medium" class="message-font">
          GraphZ（邹刘磊）、Gemini（朱金铭）、翼首草（黄炎）、什么…、
        </el-text>
        <el-text size="medium" class="message-font">特别鸣谢（核心技术/产品设计/视觉元素的朋友们</el-text>
        <el-text size="medium" class="message-font">
          猫猫猫、
          小薯条、与湫风起、
          AQ（徐安琦）、xxm123666（徐志明）、无邪の梦（吴学杰）、
          白吟（周聪）、Wlxkyh（林炎厚）、Zero（朱翎）、有个小小杜、及时行乐（高骜）、
          coldWeather66260（吴恒）、Willy Wonka（黄语莹）、Effort and luck、whiteThrush（顾晟尧）、
        </el-text>
        <el-text size="medium" class="message-font">鸣谢（参与讨论、参与测试、给出建议的朋友们）</el-text>
        <el-text size="medium" class="message-font">
          整理中......
        </el-text>
        <el-text size="medium" class="message-font">额外鸣谢（向60-526实验室的负责人及其团队致以最崇高的敬意）</el-text>
        <el-text size="medium" class="message-font">
          范洪辉教授、朱洪锦教授，以及历任与现任的实验室成员
        </el-text>
      </el-tab-pane>
    </el-tabs>
<!-- 
    <el-text size="medium" class="message-font">version 0.3.0</el-text>
    <el-text size="medium" class="message-font">version 0.3.0</el-text> -->
  </el-dialog>

</el-row>
</template>


<script>

import {useRouter} from 'vue-router';
import {ref} from 'vue';

export default {
  setup() {
    const router = useRouter();
    const activeName = ref('first')
    const dialogVisible = ref(true); // 定义响应式数据
    const fileInput = ref(null);
    const goToSecondPage = () => {
      router.push({name: 'MainPage'});
    };

    const createFileInput = () => {
      const input = document.createElement('input');
      input.type = 'file';
      input.style.display = 'none';
      input.addEventListener('change', handleFileChange);
      document.body.appendChild(input);
      return input;
    };

    const uploadFile = () => {
      if (!fileInput.value) {
        fileInput.value = createFileInput();
      }
      fileInput.value.click();
    };

    const handleFileChange = (event) => {
      const files = event.target.files;
      if (files.length > 0) {
        console.log(`选择的文件: ${files[0].name}`);
        // 在这里可以处理文件上传

      }
    };

    return {goToSecondPage, dialogVisible, activeName, uploadFile}; // 返回响应式数据和方法
  },
};

</script>


<style lang="scss">
.el-row {
  width: 100%;
  margin-bottom: 20px;
  left: 0%;
}
//.custom-button {
//  background-color: rgba(0, 0, 0, 0.0);
//  margin: 9px; /* 上下左右各10px的间距 */
//  background-image: url('button_background.png');
//  background-size: cover;
//  border-color: transparent;
//  color: white;
//  width: 15%; /* 设置对话框宽度为视口宽度的50% */
//  height: 135%; /* 设置对话框高度为视口高度的60% */
//  font-size: 20px;
//  display: flex; /* 使用 flexbox 布局 */
//  align-items: center; /* 垂直居中 */
//  justify-content: center; /* 水平居中 */
//}

.custom-button {
  background-color: rgba(0, 0, 0, 0.0);
  //margin: 0; /* 上下左右各10px的间距 */
  background-image: url('button_background.png');
  background-size: cover;
  border-color: transparent;
  color: white;
  width: 15vw; /* 使用 vw 使按钮宽度根据视口宽度自动调整 */
  height: 10vh; /* 使用 vh 使按钮高度根据视口高度自动调整 */
  font-size: 2vw; /* 字体大小根据视口宽度自动调整 */
  display: flex; /* 使用 flexbox 布局 */
  align-items: center; /* 垂直居中 */
  justify-content: center; /* 水平居中 */
}

@media (max-width: 768px) {
  .custom-button {
    width: 25vw; /* 调整宽度 */
    font-size: 3vw; /* 调整字体大小 */
  }
  .column {
    justify-content: flex-start; /* 小屏幕下左对齐 */
  }
}


.el-button {
  position: relative;
  z-index: 999;
}

.custom-font {
  font-family: 'Fantasy', sans-serif;
  color: rgba(192, 192, 192, 0.5);
}

//.full-screen-center {
//    display: flex; /* 使用 Flexbox */
//    justify-content: center; /* 水平居中 */
//    align-items: center; /* 垂直居中 */
//    height: 100vh; /* 容器高度设置为视口高度 */
//    margin: 0; /* 移除默认的外边距 */
//    padding: 5vh; /* 四周添加5%的间隔 */
//    background-image: url('background.png');
//    background-size: cover;
//    background-position: center center;
//    background-attachment: fixed; /* 保持背景固定 */
//}
.full-screen-center {
  display: flex; /* 使用 Flexbox */
  justify-content: center; /* 水平居中 */
  align-items: center; /* 垂直居中 */
  height: 100vh; /* 容器高度设置为视口高度 */
  margin: 0; /* 移除默认的外边距 */
  padding: 5vh; /* 四周添加5%的间隔 */
  background-image: url('background.png');
  background-size: contain; /* 保证背景图完整显示 */
  background-position: center center; /* 背景居中显示 */
  background-repeat: no-repeat; /* 禁止背景图重复 */
  background-attachment: fixed; /* 保持背景固定不滚动 */
}

.my-custom-dialog {
  width: 25%; /* 设置对话框宽度为视口宽度的50% */
  height: 60%; /* 设置对话框高度为视口高度的60% */
  position: fixed; /* 固定定位 */
  top: 5%; /* 距离顶部20%的位置 */
  left: 72%; /* 距离左侧25%的位置 */
  background-color: rgba(255, 255, 255, 0.6);
  border-color: transparent;

}

.message-font {
  font-family: 'Fantasy', sans-serif;
  color: rgba(98,157,93,1.0);
}

.el-dialog__title {
  color: rgba(98,157,93,1.0);
  background-color: rgba(0, 0, 0, 0);
  border-color: transparent;
}

.decorate-button {
  background-color: rgba(0, 0, 0, 0.0);
  margin: 6px; /* 上下左右各10px的间距 */
  background-image: url('small_button.png');
  background-size: cover;
  border-color: transparent;
  color: white;
  width: 15%; /* 设置对话框宽度为视口宽度的50% */
  height: 135%; /* 设置对话框高度为视口高度的60% */
}
.regardsTab{
  display: flex;
  flex-direction: column;
}
.broadImg{
  width: 50%;
  height: 50%;
}
.broadTab{
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>


