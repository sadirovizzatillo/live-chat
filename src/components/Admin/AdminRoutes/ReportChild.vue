<template>
    <div class="reportchild">
        <h2>Operator bo'yicha hisobot</h2>
        <hr>
        <div class="reportchild-operator">
            <div class="reportchild-operator__wrapper">
                <img :src="reportImage" alt="report operator image" width="120" height="120">
                <div class="reportchild-operator__info">
                    <h3>{{ reportOperator.name }}</h3>
                    <p>{{ reportOperator.email }}</p>
                </div>
            </div>
            <button class="reportchild-operator__upload">
                <img :src="reportUpload" alt="upload image" width="52" height="52">
            </button>
        </div>
        <div class="choose-report__date">
            <p class="choose-report__date-title">Hisobotni ma'lum bir oraliqda olish uchun tanlang</p>
            <select class="date-select" name="date-report" id="date-report">
                <option value="kunlik">Kunlik</option>
                <option value="haftalik">Haftalik</option>
                <option value="oylik">Oylik</option>
            </select>
        </div>
        <div class="report-date__info">
            <BaseCard title="Suhbatlar soni" :count="reportOperator.talking" />
            <BaseCard title="Xabarlar soni" :count="reportOperator.messages" />
            <BaseCard title="O'rtacha aktivlik" :count="reportOperator.active" />
        </div>


        <div id="chart">
            <apexchart type="area" height="350" :options="chartOptions" :series="series"></apexchart>
        </div>
    </div>
</template>

<script>
    import BaseCard from '../BaseCard.vue'
    import EventServices from '../../../../services/EventServices'
    import ReportOperatorImage from '../../../assets/images/reportImage.png'
    import ReportUpload from '../../../assets/images/upload.png'
    export default {
        name:"ReportChild",
        props:['id'],
        components:{
            BaseCard,

        },
        data(){
            return {
                series: [{
                    name: 'series1',
                    data: [31, 40, 28, 51, 42, 109, 100]
                }],
                chartOptions: {
                    chart: {
                        height: 350,
                        type: 'area'
                    },
                    dataLabels: {
                        enabled: false
                    },
                    stroke: {
                        curve: 'smooth'
                    },
                    xaxis: {
                        type: 'datetime',
                        categories: ["2018-09-19T00:00:00.000Z", "2018-09-19T01:30:00.000Z", "2018-09-19T02:30:00.000Z", "2018-09-19T03:30:00.000Z", "2018-09-19T04:30:00.000Z", "2018-09-19T05:30:00.000Z", "2018-09-19T06:30:00.000Z"]
                    },
                    tooltip: {
                        x: {
                            format: 'dd/MM/yy HH:mm'
                        },
                    },
                },

                reportOperator:[],
                reportImage:ReportOperatorImage,
                reportUpload:ReportUpload
            }
        },
        created(){
            EventServices.getOperatorId(this.id)
            .then(operator => {
                this.reportOperator = operator.data
            })
        }
    }
</script>

<style scoped>
    .reportchild{
        max-width: 800px;
        margin: 0 auto;
    }
    .reportchild h2{
        color: #2262C6;
        text-align: left;
        font-weight: bold;
        font-size: 26px;
        line-height: 36px;
        margin: 0;
    }
    hr{
        opacity: 0.5;
    }
    .reportchild-operator{
        display: flex;
        justify-content: space-between;
        margin-bottom: 12px;
    }
    .reportchild-operator__wrapper{
        display: flex;
        align-items: center;
        margin-right: 30px;
    }
    .reportchild-operator__info{
        margin-left: 60px;
    }
    .apexcharts-toolbar{
        display: none;
    }
    .reportchild-operator__info h3{
        font-size: 26px;
        line-height: 36px;
        margin: 0;
        margin-bottom: 10px;
    }
    .reportchild-operator__upload{
        border: none;
        background-color: inherit;
        cursor: pointer;
    }
    .reportchild-operator__info p{
        margin: 0;
    }
    .date-select{
        padding: 10px 0;
        padding-right: 60px;
        padding-left: 20px;
        border: none;
        background: #FFFFFF;
        border-radius: 8px;
        border: 1px solid #BFBFC4;
        opacity: 0.5;
        outline: none;
    }
    option{
        font-weight: bold;
        font-size: 14px;
        line-height: 18px;
    }
    .choose-report__date-title{
        margin: 0;
        color: #989898;
        font-weight: normal;
        font-size: 23px;
        line-height: 27px;
        margin-right: 12px;
    }
    .choose-report__date{
        display: flex;
        justify-content: space-between;
        margin-bottom: 27px;
    }
    .report-date__info{
        display: grid;
        grid-template-columns: 1fr 1fr 1fr;
        gap: 40px;
        justify-content: space-between;
        margin-bottom: 45px;
    }
    .reportchild-operator__info p{
        font-weight: bold;
    }
    @media screen and (max-width:1050px) {
        .report-date__info{
            grid-template-columns: 1fr 1fr;
        }
    }
    @media screen and (max-width:865px) {
        .reportchild-operator__info h3{
            font-size: 22px;
            line-height: 30px;
        }
        .date-select{
            padding: 12px 0;
            padding-right: 33px;
            padding-left: 11px;
        }
        .reportchild-operator__info{
            margin-left: 48px;
        }

    }
    @media screen and (max-width:830px) {
        .reportchild h2{
            font-size: 30px;
            line-height: 42px;
        }

    }
    @media screen and (max-width:670px) {
        .reportchild-operator__info{
            margin-left: 30px;
        }
    }
    @media screen and (max-width:570px) {
        .report-date__info{
            grid-template-columns: 1fr;
            justify-items: center;
        }
        .reportchild-operator__wrapper h3{
            font-size: 18px;
            line-height: 20px;
        }
        .reportchild h2{
            font-size: 24px;
            line-height: 32px;
        }
        .reportchild{
            padding: 20px;
        }
        .choose-report__date{
            flex-direction: column;
            align-items: center;
            text-align: center;
        }
        .choose-report__date p{
            margin-bottom: 16px;
        }
        .choose-report__date-title{
            font-size: 18px;
            line-height: 22px;
        }
        .reportchild-operator__wrapper img{
            width: 80px;
            height: 80px;
        }
        .reportchild-operator__info{
            margin-left: 15px;
        }
        .reportchild-operator__info p{
            font-size: 15px;
            line-height: 19px;
        }
    }
</style>