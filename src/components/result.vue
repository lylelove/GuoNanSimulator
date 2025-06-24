<template>
    <div v-if="resultData">
        <el-row type="flex" justify="center">
            <el-col :span="12"> 
                <p v-html="resultData.res"></p><br>
                <br>
                <p>结局</p>
                <p v-html="resultData.pic"></p>
                <el-button @click="requestRestart" type="danger" plain >如果能重来</el-button>
            </el-col>
        </el-row>
    </div>
</template>

<script>
export default {
    name: 'Result',
    props: {
        resultData: {
            type: Object,
            required: false // Can be null if no result yet
        }
    },
    methods: {
        requestRestart(){
            this.$emit('restart-game');
        }
    },
};
</script>

<style >

</style>