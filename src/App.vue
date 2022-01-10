<template>
  <div id="app">
    <h1>国男大冒险</h1><div id="waline"></div>
    <event ref="event" :class="gameover == true ? 'none' : ''"></event>
    <result ref="result" :class="gameover == false ? 'none' : ''" ></result>
    <el-dialog title="关于" :visible.sync="dialogVisible2" >
      <div>本项目来源于<a href="https://github.com/Fengzi2333">fengzi2333</a>的<a href="https://github.com/Fengzi2333/GuoNanSimulator">GuoNanSimulator</a>项目。<br><br>经<a href="https://github.com/lylelove">lylelove</a>使用Vue重构。</div>
    </el-dialog>
    <el-button class="bottomright" icon="el-icon-info" @click="dialogVisible2 = true"  circle></el-button>
  </div>
</template>

<script>
import Event from './components/event.vue'
import Result from './components/result.vue';
export default {
  name: 'App',
  components: {
    Event,
    Result
  },
  data() {
    return {
      gameover:false,
      gameon:true,
      gamesence:0,
      dialogVisible2: false,
      event_list:[
        {
          id:"e1",
          event:"你是某国男性,简称国男，20岁,是学生，就读于某高校。今天你没有课， 你决定:",
          btn1:"待在宿舍",
          btn1res:"res1",
          btn2:"出去逛逛",
          btn2res:"e2",
        },{
          id:"e2",
          event:"出门应该带上哪些东西好呢，你看看手机、平板、kindle、switch...决定:",
          btn1:"全都带上",
          btn1res:"res2",
          btn2:"只带必要的",
          btn2res:"e3",
        },{
          id:"e3",
          event:"你只带了手机和蓝牙耳机。你在学校逛了一圈， 看了看时间该吃午饭了，于是你来到食堂，发现这里已经人满患，你选了一个看起来不太长的队伍走了过去：",
          btn1:"为了防止有人插队，<br>你紧紧跟着前一个人",
          btn1res:"res3",
          btn2:"和前一个人保持距离",
          btn2res:"e4",
          },
          {
            id:"e4",
            event:"你和前一个人保持着距离，但是队伍移动得很慢，你打算：",
            btn1:"玩手机打发时间",
            btn1res:"res4",
            btn2:"听歌就好",
            btn2res:"e5",
          },{
            id:"e5",
            event:"你跟着队伍打到了饭, 吃饭时耳机没电了，你草草收了起来，便一边吃饭一边玩手机。这时你注意到一个女生在偷你耳机，你：",
            btn1:"制止她",
            btn1res:"res5",
            btn2:"假装没看见",
            btn2res:"e6",
          },{
            id:"e6",
            event:"你继续吃饭，吃完饭回宿舍，刚吃饱的你不太想运动，但是电梯里已经站了几个女生,你决定：",
            btn1:"坐电梯",
            btn1res:"res6",
            btn2:"走楼梯",
            btn2res:"e7",
          },{
            id:"e7",
            event:"你爬楼梯回到宿舍,之后无惊无险的毕业，找了一家公司996,贷款买了车房，通过相亲结了婚，婚后一年有了个儿子，转眼儿子便到了上小学的年纪，你肩上的担子更重了。这天你破天荒的准时下班，你看时间还早，决定：",
            btn1:"回家休息",
            btn1res:"e10",
            btn2:"赚点外快",
            btn2res:"e8",
          },{
            id:"e8",
            event:"你在货推推平台注册了账户，平台推来一份可接单，你选择：",
            btn1:"接受",
            btn1res:"res7",
            btn2:"不接受",
            btn2res:"e9",
          },{
            id:"e9",
            event:"你在网约车平台注册了账户，平台推来一份可接单，你选择：",
            btn1:"接受",
            btn1res:"res8",
            btn2:"不接受",
            btn2res:"e10",
          },
          {
            id:"e10",
            event:"难得有这空闲时间，你打算回家休息。停车时发现你的停车位被一陌生车辆占用，你决定：",
            btn1:"想办法联系车主",
            btn1res:"e11",
            btn2:"换个车位",
            btn2res:"res9",
          },{
            id:"e11",
            event:"车主在雨刮器上留了联系方式，电话打通后，车主下来开车离开了。回到家，老婆在洗澡，你躺在沙发小憩。迷迷糊糊中老婆叫你去接儿子，你：",
            btn1:"去接",
            btn1res:"e12",
            btn2:"不去",
            btn2res:"res10",
          },{
            id:"e12",
            event:"你看了看时间，儿子差不多放学了，于是你将放学的儿子接回家。之后你和老婆响应国家号召生了二胎，并开始准备三胎。可是随着二儿子长大，他和大儿子之间的容貌差异越来越大，你看在眼里，决定：",
            btn1:"装不知道",
            btn1res:"res11",
            btn2:"去做亲子鉴定",
            btn2res:"e13",
          },{
            id:"e13",
            event:"心中的疑问越来越大，你悄悄带着两个孩子做了亲子鉴定，发现两个孩子都不是自己的。你和妻子为此吵了一架， 你决定离婚，同时为了眼不见心不烦，搬去和父母一起住。这天岳父敲门，说是为他女儿的事来赔礼，你决定：",
            btn1:"见面聊聊",
            btn1res:"res12",
            btn2:"不见",
            btn2res:"res13",
          },


      ],
      result_list:[
        {
          id:"res1",
          res:"你打算在宿舍享受一下颓废的生活，于是叫了一份外卖开始打游戏。几轮厮杀过后，看到你舍友问你为什么在食堂对着女生DIY，你感觉莫名其妙，一番网上冲浪后才知道，社交网络上到处都是你的负面消息，而你今天并没有出过宿舍。事后事件源头的女生表示事件纯属虚构，而你已经社会性死亡。<br><a href='https://weibo.com/6239620007/L6iAi5T2l'>来源</a><br>关键词：深圳大学 食堂",
          pic:"人在家中坐",
        },
        {
          id:"res2",
          res:"由于你的包太大，不小心碰到了一位学姐的屁股，她在社交网络上称你是色狼，你社会性死亡。<br><a href='https://weibo.com/2615417307/JuLwat2bs'>来源</a><br>关键词：清华老师回应学姐错告学弟",
          pic:"无过则勉",
        },
        {
          id:"res3",
          res:"你距离前面的女生太近，被她拍了下来，并且在社交网络上称你对她图谋不轨，你社会性死亡。<br><a href='https://weibo.com/p/231522cba6129f538ccfce7f46a63025fc45e6'>来源</a>",
          pic:"欲加之罪",
        },
        {
          id:"res4",
          res:"你忘了跟上前面的队伍，突然听到一个女生喊“你是不是插我队？！”接着一个玻璃瓶就碎在了你的后脑勺，虽然你最后制服了对方，但你也受伤住院。<br><br>关键词：广东医科大学 玻璃瓶",
          pic:"无妄之灾",
        },        {
          id:"res5",
          res:"你将小偷捉了现行，对方却表示“抛开事实不谈，你坐了我常坐的位子难道就没错吗”，然后砸了你的耳机扬长而去。<br><Br>关键词：华东理工大学 耳机",
          pic:"捉贼拿脏",
        },        {
          id:"res6",
          res:"电梯作为公共资源，当然可以用，你抱着这个想法走进电梯，却被电梯里的女生认为是抢占她们的资源，并对你网曝，后来学校禁止低楼层的男生使用电梯。<br><br>关键词：北京师范大学 电梯",
          pic:"高人一等",
        },        {
          id:"res7",
          res:"你选了第一份单，叫车的是一位女性，目的地不算远，你凭着记忆中的路线开了过去，没想到在快到目的地时，乘客突然跳车，随后身亡，你被拘留二百天。<br><br>关键词：货拉拉司机 周某春<br><a href='https://weibo.com/1806128454/L55Qeu5zh'>来源</a>",
          pic:"逃出生天",
        },        {
          id:"res8",
          res:"叫车的是一位丰满的女性，手一直插在裤兜里，目的地有点远，中间要走一段高速公路。上了高速以后，乘客从裤兜里掏出一把刀，对你连捅数刀，你重伤住院。<br><br>关键词：湖南一女子乘出租车拿刀刺司机<br><a href='https://weibo.com/2628314830/KxZ8Hcdje'>来源</a>",
          pic:"血光之灾",
        },        {
          id:"res9",
          res:"你换了个没人用的车位. 回到家，发现门前有一双不认识的男鞋，开门看到老婆正在和一名陌生男子一起为爱鼓掌。",
          pic:"同道之人",
        },        {
          id:"res10",
          res:"你难得有时间休息 ,迷迷糊糊地拒绝了，平时儿子不用接能回来，今天应该也可以。但是今天你儿子很晚都没回来，后来得知，你儿子被一名女子抱到楼上摔死。<br><br>关键词：男童被陌生女抱走后在附近小区坠亡<br><a href='https://weibo.com/5044281310/L44o2EDIJ'>来源</a>",
          pic:"切肤之痛",
        },        {
          id:"res11",
          res:"你对两个儿子的容貌差异视若无睹，视如己出，老婆对你很满意，不久，你们又生了第三胎。",
          pic:"难得糊涂",
        },        {
          id:"res12",
          res:"你打开门，没想到岳父带着刀，他趁你不防砍倒了你，又砍倒了你的父母，然后报警自首，之后你老婆出具谅解书，减轻了岳父的刑责，并带着你的家产改嫁了。<br><br>关键词：彭州 岳父 灭门<br><a herf='https://weibo.com/1887344341/L2LHwrUZ5'>来源</a>",
          pic:"鸡犬不留",
        },        {
          id:"res13",
          res:"你表示此事绝无回旋余地，对岳父闭门不见，他离去时你从窗户看到他带着刀，暗自庆幸。",
          pic:"未来可期<br><br><br>恭喜你已通关当前版本，本游戏中所有结局，除“同道中人”不确定是否有真实案例外，均根据真实事件改编，如有雷同，刻意为之。",
        },
      ]
      
    }
  },
  methods:{
    afresh(){
      this.gameover=false;
      this.gameon=true;
      this.gamesence=0;
      this.$refs.event.msg=this.event_list[0].event;
      this.$refs.event.btn1=this.event_list[0].btn1;
      this.$refs.event.btn2=this.event_list[0].btn2;
    },
    btnfun1(){
      this.gameon = false;
      for(var i=0;i<this.event_list.length;i++){
        if(this.gameon==false){
          if(this.event_list[this.gamesence].btn1res==this.event_list[i].id){
            this.gamesence = i;
            this.gameon = true;
            this.$refs.event.msg = this.event_list[this.gamesence].event;
            this.$refs.event.btn1=this.event_list[this.gamesence].btn1;
            this.$refs.event.btn2=this.event_list[this.gamesence].btn2;
          } 
        }

      }
      if(this.gameon==false){
        this.gameover=true;
        for(var j =0;j<this.result_list.length;j++){
          if(this.event_list[this.gamesence].btn1res==this.result_list[j].id){
            this.$refs.result.resmsg=this.result_list[j].res;
            this.$refs.result.picture = this.result_list[j].pic;
          } 
        }
      }
      
    },
    btnfun2(){
      this.gameon=false;
      for(var i =0;i<this.event_list.length;i++){
        if(this.gameon==false){
          if(this.event_list[this.gamesence].btn2res==this.event_list[i].id){
            this.gamesence=i;
            this.gameon=true;
            this.$refs.event.msg = this.event_list[this.gamesence].event;
            this.$refs.event.btn1=this.event_list[this.gamesence].btn1;
            this.$refs.event.btn2=this.event_list[this.gamesence].btn2;
          }
        }
      }
      if(this.gameon==false){
        this.gameover=true
        for(var j =0;j<this.result_list.length;j++){
          if(this.event_list[this.gamesence].btn2res==this.result_list[j].id){
            this.$refs.result.resmsg=this.result_list[j].res;
            this.$refs.result.picture = this.result_list[j].pic;
          } 
        }
      }
    },

  }

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.none{
  display: none;
}
.bottomleft{
  position: fixed;
  bottom: 0;
  left: 0;
}
.bottomright{
  position: fixed;
  bottom: 0;
  right: 0;
}
</style>
