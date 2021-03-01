<template>
  <div class="home">
    <div class="h">
      <div class="chatroom">
        <dl>
          <div v-for="(item, index) in ditems" :key="index">
            <dt>item.title</dt>
            <dd>item.content</dd>
          </div>
        </dl>
      </div>
    </div>

    <div class="bottom">
      <input type="text" placeholder="请输入..." v-model="info" />
      <button @click="chatSend">确 定</button>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import axios from "axios";

export default {
  name: 'Home',
  components: {
    
  },
  data() {
    return {
      info: '',
      ditems:[
        {title: '陈望', content: '故宫在哪里？'},
        {title: '明明', content: '故宫在北京'},
      ]
    };
  },
  methods:{
    chatSend(){
      console.log(this.info);
    },

    httpcall(){
      // axios.get('http://121.4.148.42:8000/hello/f')
      //   .then(res=>{
      //     this.msg = res.data;
      //   })
      //   .catch((error)=>{
      //     console.log(error);
      //   });

        // axios.get('http://121.4.148.42:8000/index/hello', {
        //   params: {
        //     ID: 12345
        //   }
        // }).then(res=>{
        //   this.msg = res.data;
        // })
        // .catch((error)=>{
        //   console.log(error);
        // });

        // axios.post('http://121.4.148.42:8000/index/hello/f', {
        //   ID: 12345
        // }).then(res=>{
        //   this.msg = res.data;
        // })
        // .catch((error)=>{
        //   console.log(error);
        // });

        // axios.get('http://121.4.148.42:8000/index.php/index/postTest', {
        //   params: {
        //     ID: 12345
        //   }
        // }).then(res=>{
        //   // this.msg = res.data;
        //   console.log(res.data);
        // })
        // .catch((error)=>{
        //   console.log(error);
        // });

        axios.post('http://121.4.148.42:8000/index.php/index/postTest', {
          ID: 12345,
          name: 'chen',
          info: {
            parent: 'f',
            age: 45
          }
        }).then(res=>{
          // this.msg = res.data;
          console.log(res.data);
        })
        .catch((error)=>{
          console.log(error);
        });
    },
    changeHandle(){
      const file = this.$refs.fileInt.files[0];
      console.log(file);
      const data = new FormData();
      data.append('file', file);
      axios.post('http://121.4.148.42:8000/index.php/upload/up', data, {
        headers: {
          'Content-Type': 'multipart/form-data',
        },
      }).then(
        res => {
          console.log(res);
        }
      ).catch(err=>{
        console.log(err);
      })
    },
    downFunc(){
      axios.post('http://121.4.148.42:8000/index.php/download/down', {
          ID: 12345,
        }).then(res=>{
          console.log(res.data);
        })
        .catch((error)=>{
          console.log(error);
        });
    },
  },
}
</script>

<style scoped>
.h{
  display: flex;
  justify-content: center;
}
.chatroom{
  border: 1px solid black;
  width: 500px;
  height: 300px;
  padding: 10px;
  background-color: aliceblue;
}
.bottom{
  display: flex;
  justify-content: center;
  margin-top: 10px;
}
.bottom button{
  margin-left: 10px;
}
</style>