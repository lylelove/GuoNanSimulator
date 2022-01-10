<template>
    <div id="common">
        <el-row type="flex" justify="center">
            <el-col :span="12">        
                <p>{{msg}}</p>
                    <br/>
                <el-button v-html="btn1" @click="f_btn1" type="success" plain ></el-button><br/><br/>
                <el-button  v-html="btn2" @click="f_btn2" type="success" plain ></el-button>
            </el-col>
    </el-row>


    </div>
</template>

<script>
export default {
    name: 'Event',

    data() {
        return {
            msg:"你是某国男性,简称国男，20岁,是学生，就读于某高校。今天你没有课， 你决定:",
            btn1:"待在宿舍",
            btn2:"出去逛逛",
        };
    },

    methods: {
        f_btn1(){
            this.$root.$children[0].btnfun1()
        },
        f_btn2(){
            this.$root.$children[0].btnfun2()
            console.log(123)
        }
    },
};
</script>

<style>
#common {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>