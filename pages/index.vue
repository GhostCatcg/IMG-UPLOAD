<template >
  <div id="goods-add">
    <el-form model="goodinfo" ref="goodinfo" label-width="100px" class="demo-ruleForm">
      <el-form-item label="名字">
        <el-input v-model="goodinfo.name"></el-input>
      </el-form-item>

      <el-form-item label="价格">
        <el-input v-model="goodinfo.price"></el-input>
      </el-form-item>

      <el-form-item label="描述">
        <el-input v-model="goodinfo.description"></el-input>
      </el-form-item>

      <el-form-item label="品牌">
        <el-input v-model="goodinfo.brand"></el-input>
      </el-form-item>

      <el-form-item label="标签">
        <el-input v-model="goodinfo.label" placeholder="每个标签使用 分开"></el-input>
      </el-form-item>

      <div class="img-upload">
        <el-upload
          action="#"
          :limit="5"
          ref="upload"
          :multiple="true"
          :auto-upload="false"
          :file-list="fileList"
          list-type="picture-card"
        >
          <el-button slot="trigger" size="small" type="primary">选取文件</el-button>
          <div slot="tip" class="el-upload__tip">上传图片大小不超过500kb</div>
        </el-upload>
      </div>

      <el-form-item>
        <el-button type="primary" @click="submitUpload">立即创建</el-button>
        <el-button @click="resetForm('goodinfo')">重置</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>


<script>
import axios from "axios";

export default {
  name: "goods-add",
  methods: {
    submitUpload() {
      // 获取到 上传的所有文件，它是一个数组
      const fileArray = this.$refs.upload.uploadFiles;
      // 实例化FormData对象
      const fd = new FormData();
      // 遍历文件数组，将所有文件存入fd中
      for (let i = 0; i < fileArray.length; i++) {
        // 在这里数组每一项的.raw才是你需要的文件，有疑惑的可以打印到控制台看一下就清楚了
        fd.append("avatar", fileArray[i].raw);
      }
      // 发送HTTP请求，发送数据
      axios({
        url: "/api/view/add-good",
        method: "post",
        data: fd
      }).then(res => {
        console.log(res.data);
      });
    }
  }
};
</script>