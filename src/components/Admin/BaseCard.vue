<template>
    <div class="report-date__card">
        <h4 class="report-date__title">
            <slot name="title">{{ title }}</slot>
        </h4>
        <hr>
        <span class="report-date__count">
            <slot name="count">{{ count }}</slot>
        </span>
    </div>
</template>

<script>
    export default {
        name:'Base-card',
        props:['title', 'count']
    }
</script>

<style scoped>
    .report-date__card{
        border: 1px solid #8AB5CB;
        box-sizing: border-box;
        border-radius: 10px;
        max-width: 260px;
        text-align: center;
    }
    .report-date__title{
        margin: 0;
        padding: 8px 16px;
        font-weight: normal;
        font-size: 29px;
        line-height: 48px;
        color: #8AB5CB;
    }
    .report-date__count{
        font-weight: normal;
        font-size: 39px;
        line-height: 48px;
        color: #8AB5CB;
    }

    @media screen and (max-width:570px) {
        .report-date__card{
            max-width: 300px;
            width: 100%;
        }
    }

    @media screen and (max-width:520px) {
        .report-date__card{
            max-width: 200px;
        }
        .report-date__title{
            font-size: 20px;
            line-height: 30px;
        }
        .report-date__count{
            font-size: 20px;
            line-height: 30px;
        }
    }
</style>