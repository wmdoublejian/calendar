<template>
  <div class="home">
      <div class="year">
        <div @click="prevYear">
          <<
        </div>
        <div @click="prevMonth">
          <
        </div>
        <div>
          {{dateObj.year}}年{{dateObj.month+1}}月
        </div>
        <div @click="nextMonth">
          >
        </div>
        <div @click="nextYear">
          >>
        </div>
      </div>
      <div class="week">
        <div>
          一
        </div>
        <div>
          二
        </div>
        <div>
          三
        </div>
        <div>
          四
        </div>
        <div>
          五
        </div>
        <div>
          六
        </div>
        <div>
          日
        </div>
      </div>
      <div class="date">
        <div v-for="item in daysList">
          {{item}}
        </div>
      </div>
  </div>
</template>
<script>
  export default {
    data(){
      return {
        dateObj:{},
        daysList:[]
      }
    },
    methods:{
      renderDate(year,month){
        this.daysList=[];
        let firstDayWeekDay=new Date(year,month,1).getDay();
        for(let i=0;i<firstDayWeekDay-1;i++){
          this.daysList.push('')
        }
        let curMonthDays=new Date(year,month+1,0).getDate();
        for(let i=0;i<curMonthDays;i++){
          this.daysList.push(i+1)
        }
      },
      prevYear(){
        this.dateObj.year-=1
        this.renderDate(this.dateObj.year,this.dateObj.month)
      },
      nextYear(){
        this.dateObj.year+=1
        this.renderDate(this.dateObj.year,this.dateObj.month)
      },
      prevMonth(){
        this.dateObj.month-=1;
        if(this.dateObj.month<0){
          this.dateObj.month=11;
          this.dateObj.year-=1;
        }
        this.renderDate(this.dateObj.year,this.dateObj.month)
      },
      nextMonth(){
        this.dateObj.month+=1;
        if(this.dateObj.month>11){
          this.dateObj.month=0;
          this.dateObj.year+=1;
        }
        this.renderDate(this.dateObj.year,this.dateObj.month)
      }
    },
    created(){
      let date= new Date();
      this.dateObj.year=date.getUTCFullYear();
      this.dateObj.month=date.getUTCMonth();
      this.renderDate(this.dateObj.year,this.dateObj.month)
    }
  }
</script>
<style lang="less">
  @fontSize:16px;
  .home{
    width:350px;
    margin: 100px auto 0;
    padding: 10px;
    background-color: #fff;
    .year{
      display: grid;
      grid-template-columns: 37.5px 37.5px 200px 37.5px 37.5px;
      div{
        text-align: center;
        cursor: pointer;
      }
    }
    .week{
      margin-top: 10px;
      display: flex;
      padding-bottom: 10px;
      border-bottom: 1px solid #eee;
      div{flex: 1;text-align: center}
    }
    .date{
      display: flex;
      flex-wrap: wrap;
      /*display: grid;*/
      /*grid-template-columns:50px 50px 50px 50px 50px 50px 50px;*/
      /*grid-template-rows:50px 50px 50px 50px 50px 50px;*/
      div{
        text-align: center;
        line-height: 50px;
        width: 50px;
        height: 50px;
      }
    }
  }
</style>
