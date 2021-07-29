<style lang="less" scoped>
    .event{
        width: 200px;
        height: 200px;
        border: 1px solid black;
    }
</style>
<template>
    <div class="event">
        <div class="back" @click="back">返回</div>
        <ul @click.stop="ev">
            <li>chlidrenOne</li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
        </ul>
        <p @click="p">chlidrenP</p>
    </div>
</template>
<script>
export default {
    data(){
        return{

        }
    },
    methods:{
        back(){
            this.$router.history.go(-1)
        },
        ev(e){
            console.log(222);
            // console.log(e);
        },
        p(){
            console.log("ppp");
        }
    }
}
</script>