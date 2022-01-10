<template>
    <div>
        <el-row type="flex" justify="center">
            <el-col :span="12"> 
                <p v-html="resmsg"></p><br>
                <br>
                <p>结局</p>
                <p v-html="picture"></p>
                <el-button @click="again" type="danger" plain >如果能重来</el-button>
            </el-col>
        </el-row>
    </div>
</template>

<script>
export default {
    name: 'Result',

    data() {
        return {
            resmsg:"",
            picture:"",
        };
    },

    methods: {
        again(){
            this.$root.$children[0].afresh();
        }
    },
};
</script>

<style >

</style>