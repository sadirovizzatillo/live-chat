<template>
    <div class="main-page">
        <AdminTop @menuBtn="buttonClick"/>
        <div class="main-page__bottom">
            <AdminNav :clicked="this.clicked"/>
            <router-view class="routes"></router-view>
        </div>
    </div>
</template>

<script>
    import AdminNav from '../components/Admin/AdminNav.vue'
    import AdminTop from '../components/Admin/AdminTop.vue'
    export default {
        name:"Home",
        components:{
            AdminNav,
            AdminTop
        },
        data(){
            return{
                clicked:false
            }
        },
        methods:{
            buttonClick(){
                this.clicked = !this.clicked
            }
        }
    }
</script>

<style scoped>
    .container{
        max-width: 1320px;
        padding-left: 20px;
        padding-right: 20px;
        margin: 0 auto;
    }
    .main-page{
        display: flex;
        flex-direction: column;
    }
    .main-page__bottom{
        display: flex;
    }
    .routes{
        flex-grow: 1;
        padding: 30px;
    }
    @media screen and (max-width:820px) {
        .routes{
            padding: 20px;
        }
    }
    @media screen and (max-width:520px) {
        .routes{
            padding-top: 100px;
        }
    }
</style>