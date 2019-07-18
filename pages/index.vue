<template>
  <div>
    <input type="text" v-model="phonenumber">
    <input type="file" @change="uploadImg($event,'HF')" />
    <p @click="sumbit">发送</p>
  </div>
</template>
 
<script>
import axios from "axios";
export default {
  data(){
    return {
      phonenumber:""

    }
  },
  methods: {
    uploadImg: (e, type) => {
      let file = e.target.files[0];
      console.log(file);
      if (!/\.(gif|jpg|jpeg|png|GIF|JPG|PNG|JPEG)$/.test(file.name)) {
        this.alert(this.l.ST_TEXT5);
        return;
      }
      let param = new FormData(); //创建form对象
      param.append("file", file); //通过append向form对象添加数据
      console.log(param, param.get("file"));

      axios
        .post("http://localhost:3000/upload", param)
        .then(function(response) {
          console.log(response);
        })
        .catch(function(error) {
          console.log(error);
        });
    }
  }
};
</script>

<style>
p {
  padding: 0.2em 0.5em;
  border: 1px solid #432532;
  width: 2em;
  cursor: pointer;
  border-radius: 5px;
  background-color: #ccc;
}
p:hover{
  color:red;
}
</style>