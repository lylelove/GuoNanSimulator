<template>
    <div id="common">
        <el-row type="flex" justify="center">
            <el-col :span="12" v-if="eventData">
                <p>{{eventData.event}}</p>
                    <br/>
                <el-button v-html="eventData.btn1" @click="handleChoice('btn1res')" type="success" plain ></el-button><br/><br/>
                <el-button v-html="eventData.btn2" @click="handleChoice('btn2res')" type="success" plain ></el-button>
            </el-col>
    </el-row>
    </div>
</template>

<script>
export default {
    name: 'Event',
    props: {
        eventData: {
            type: Object,
            required: true
        }
    },
    methods: {
        handleChoice(choiceKey) {
            this.$emit('player-choice', choiceKey);
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