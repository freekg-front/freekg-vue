<template>
    <div :style="styleDiv">
      <!--<Nav></Nav>-->
      <el-button v-on:click="toIntroduce" :style="styleIntroduce" type="text">介绍</el-button>
      <div class="search-width">
        <h1 style="text-align: center;font-family: 'my">中文诗歌知识图谱</h1>
        <el-input placeholder="请输入查询内容"  v-model="input">
          <el-button slot="append" icon="el-icon-search" v-on:click="answerSearch"></el-button>
        </el-input>
        <br/>
      </div>
      <div class="index-btn-container">
        <div class="index-btn">
          <!--<el-button v-on:click="toPoetcatalog" style="background-color: #42A5F5;color: white" class="btn">诗人目录</el-button>-->
          <el-button v-on:click="toPoetrelation" type="text" class="btn">诗人关系图谱</el-button>
          <el-button v-on:click="toPoetway"  type="text" class="btn">诗人轨迹</el-button>
          <el-button v-on:click="toPoetcard" type="text" class="btn">诗人卡片</el-button>
          <el-button v-on:click="toPoemcard" type="text" class="btn">诗歌卡片</el-button>
          <el-button v-on:click="toSearchall" type="text" class="btn">智能查询</el-button>
        </div>
      </div>

    </div>
</template>

<script>
//  import Nav from '../components/nav.vue'
  import ElButton from "../../node_modules/element-ui/packages/button/src/button.vue";

export default {
//    components: { Nav },
  components: {ElButton},
  data () {
      return {
        input:'',
        styleInput:{
          width:'400px',
          height:'200px',
          left:'50%',
          top:'50%',
          position:'relative',
          marginLeft:'-200px',
          marginTop:'-150px'
        },
        styleDiv:{
          width:document.documentElement.clientWidth+'px',
          height:document.documentElement.clientHeight+'px'
        },
        styleIntroduce:{
          position: 'fixed',
          top: '20px',
          right: '20px',
          height: '150px',
          width: '150px',
          fontSize:'30px',
          fontFamily: 'my',
          color: 'black',
//          color: '#c23531',
          backgroundImage: "url(" + require('../../static/image/2.png') + ")",
            backgroundSize:'150px 150px',
            backgroundPosition:'center'
        }
      }
    },
    methods: {
      answerSearch(){
        this.$api.get('/datasource/unknownquery?name='+this.input, null, json=> {
//          console.log(json);
          if (json[0].born) {//判断单个实体的类型，是古诗还是诗人
            window.location.assign("#/poetinfo/"+json[0].name+'?uri='+json[0].ob);
          } else {
            window.location.assign("#/poeminfo/"+json[0].name+'?uri='+json[0].o);
          }
        });
      },
      toPoetcatalog(){
        window.location.assign("#/poetcatalog/");
      },
      toPoetrelation(){
        window.location.assign("#/poetrelation/");
      },
      toPoetway(){
        window.location.assign("#/poetway/");
      },
      toPoetcard(){
        window.location.assign("#/poetcard/");
      },
      toPoemcard(){
        window.location.assign("#/poemcard/");
      },
      toSearchall(){
        window.location.assign("#/searchall/");
      },
      toIntroduce(){
        window.location.assign("#/introduce/");
      }
    }
  }
</script>
