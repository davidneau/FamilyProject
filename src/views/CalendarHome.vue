<template>
  <div class="divCalendar">
    <div class="tableHeader">
    <v-btn style="background-color: aquamarine;" text icon @click="previousMonth"><v-icon>mdi-arrow-left-bold</v-icon></v-btn>
    <h1 style="margin-left: 10px; margin-right: 10px;;"><center>{{switchMonth(this.today.getMonth()+1) + ' ' + this.today.getFullYear()}}</center></h1>
    <v-btn style="background-color: aquamarine;" text icon @click="nextMonth"><v-icon>mdi-arrow-right-bold</v-icon></v-btn>
    </div>
    <table cellpadding="0" cellspacing="0">
      <tr>
        <th>Lundi</th>
        <th>Mardi</th>
        <th>Mercredi</th>
        <th>Jeudi</th>
        <th>Vendredi</th>
        <th>Samedi</th>
        <th>Dimanche</th>
      </tr>
      <tr class="row">
        <td :class="myClass(1)" @click="createEvent">{{getNum(1)['num']}}</td>
        <td :class="myClass(2)" @click="createEvent">{{getNum(2)['num']}}</td>
        <td :class="myClass(3)" @click="createEvent">{{getNum(3)['num']}}</td>
        <td :class="myClass(4)" @click="createEvent">{{getNum(4)['num']}}</td>
        <td :class="myClass(5)" @click="createEvent">{{getNum(5)['num']}}</td>
        <td :class="myClass(6)" @click="createEvent">{{getNum(6)['num']}}</td>
        <td :class="myClass(7)" @click="createEvent">{{getNum(7)['num']}}</td>
      </tr>
      <tr class="row">
        <td :class="myClass(8)" @click="createEvent">{{getNum(8)['num']}}</td>
        <td :class="myClass(9)" @click="createEvent">{{getNum(9)['num']}}</td>
        <td :class="myClass(10)" @click="createEvent">{{getNum(10)['num']}}</td>
        <td :class="myClass(11)" @click="createEvent">{{getNum(11)['num']}}</td>
        <td :class="myClass(12)" @click="createEvent">{{getNum(12)['num']}}</td>
        <td :class="myClass(13)" @click="createEvent">{{getNum(13)['num']}}</td>
        <td :class="myClass(14)" @click="createEvent">{{getNum(14)['num']}}</td>
      </tr>
      <tr class="row">
        <td :class="myClass(15)" @click="createEvent">{{getNum(15)['num']}}</td>
        <td :class="myClass(16)" @click="createEvent">{{getNum(16)['num']}}</td>
        <td :class="myClass(17)" @click="createEvent">{{getNum(17)['num']}}</td>
        <td :class="myClass(18)" @click="createEvent">{{getNum(18)['num']}}</td>
        <td :class="myClass(19)" @click="createEvent">{{getNum(19)['num']}}</td>
        <td :class="myClass(20)" @click="createEvent">{{getNum(20)['num']}}</td>
        <td :class="myClass(21)" @click="createEvent">{{getNum(21)['num']}}</td>
      </tr>
      <tr class="row">
        <td :class="myClass(22)" @click="createEvent">{{getNum(22)['num']}}</td>
        <td :class="myClass(23)" @click="createEvent">{{getNum(23)['num']}}</td>
        <td :class="myClass(24)" @click="createEvent">{{getNum(24)['num']}}</td>
        <td :class="myClass(25)" @click="createEvent">{{getNum(25)['num']}}</td>
        <td :class="myClass(26)" @click="createEvent">{{getNum(26)['num']}}</td>
        <td :class="myClass(27)" @click="createEvent">{{getNum(27)['num']}}</td>
        <td :class="myClass(28)" @click="createEvent">{{getNum(28)['num']}}</td>
      </tr>
      <tr class="row">
        <td :class="myClass(29)" @click="createEvent">{{getNum(29)['num']}}</td>
        <td :class="myClass(30)" id="{{getNum(30)}}" @click="createEvent">{{getNum(30)['num']}}</td>
        <td :class="myClass(31)" @click="createEvent">{{getNum(31)['num']}}</td>
        <td :class="myClass(32)" @click="createEvent">{{getNum(32)['num']}}</td>
        <td :class="myClass(33)" @click="createEvent">{{getNum(33)['num']}}</td>
        <td :class="myClass(34)" @click="createEvent">{{getNum(34)['num']}}</td>
        <td :class="myClass(35)" @click="createEvent">{{getNum(35)['num']}}</td>
      </tr>
      <tr class="row">
        <td :class="myClass(36)" @click="createEvent">{{getNum(36)['num']}}</td>
        <td :class="myClass(37)" @click="createEvent">{{getNum(37)['num']}}</td>
        <td :class="myClass(38)" @click="createEvent">{{getNum(38)['num']}}</td>
        <td :class="myClass(39)" @click="createEvent">{{getNum(39)['num']}}</td>
        <td :class="myClass(40)" @click="createEvent">{{getNum(40)['num']}}</td>
        <td :class="myClass(41)" @click="createEvent">{{getNum(41)['num']}}</td>
        <td :class="myClass(42)" @click="createEvent">{{getNum(42)['num']}}</td>
      </tr>
    </table>
  </div>
</template>

<script>
import { defineComponent } from 'vue';


export default defineComponent({
  name: 'CalendarHome',
  data(){
      return {
        today: "",
        mondayLastMonth: "",
        numberDaysLastMonth: 0,
        numberDaysCurrentMonth: 0,
        nums: {'1': 0},
      }
    },
  methods: {
    getNum(nb) {
      let final_num = this.mondayLastMonth + nb - 1
      let num = 0
      let month = ''
      if (this.mondayLastMonth == 1){
        //cas spécial où le mois commence par un lundi
        if (final_num <= this.numberDaysCurrentMonth) {
          num = final_num
          month = "currentMonth"
        }
        else {
          final_num -= this.numberDaysCurrentMonth
          num = final_num
          month = "nextMonth"
        }    
      }
      else{
        if (final_num <= this.numberDaysLastMonth) {
          num = final_num
          month = "previousMonth"
        }
        else if (final_num > this.numberDaysLastMonth && final_num <= this.numberDaysLastMonth + this.numberDaysCurrentMonth) {
          final_num -= this.numberDaysLastMonth
          num = final_num
          month = "currentMonth"
        }
        else {
          num = (final_num - this.numberDaysLastMonth) % this.numberDaysCurrentMonth
          month = 'nextMonth'
        }
      }
      let result = {'num' : num, 'month' : month}
      return result
    },
    createEvent(...args) {
      console.log(args)
    },
    myClass(numero){
      numero = this.getNum(numero)
      const today = new Date()
      if (this.today.getFullYear() == today.getFullYear() && this.today.getMonth() == today.getMonth() && numero['num'] == today.getDate() && numero['month'] == "currentMonth"){
        console.log(this.today)
        return "today"
      }
      if (numero['month'] == 'previousMonth' || numero['month'] == 'nextMonth') {
        return "grise"
      }
    },
    previousMonth(){
      console.log("previous month")
      const otherDay = new Date(this.today.getFullYear(), this.today.getMonth() - 1, 1)
      this.today = otherDay
      this.numberDaysCurrentMonth = new Date(this.today.getFullYear(), this.today.getMonth()+1, 0).getDate()
      this.numberDaysLastMonth = new Date(this.today.getFullYear(), this.today.getMonth(), 0).getDate()
      this.mondayLastMonth = new Date(this.today.getFullYear(), this.today.getMonth(), 1)
      const tmpDate = new Date(this.today.getFullYear(), this.today.getMonth(), 1)
      this.mondayLastMonth.setDate(tmpDate.getDate() - ((tmpDate.getDay() + 6) % 7))
      this.mondayLastMonth = this.mondayLastMonth.getDate()
    },
    nextMonth(){
      console.log("next month")
      const otherDay = new Date(this.today.getFullYear(), this.today.getMonth() + 1, 1)
      this.today = otherDay
      this.numberDaysCurrentMonth = new Date(this.today.getFullYear(), this.today.getMonth()+1, 0).getDate()
      this.numberDaysLastMonth = new Date(this.today.getFullYear(), this.today.getMonth(), 0).getDate()
      this.mondayLastMonth = new Date(this.today.getFullYear(), this.today.getMonth(), 1)
      const tmpDate = new Date(this.today.getFullYear(), this.today.getMonth(), 1)
      this.mondayLastMonth.setDate(tmpDate.getDate() - ((tmpDate.getDay() + 6) % 7))
      this.mondayLastMonth = this.mondayLastMonth.getDate()
      console.log('finish next month')
    },
    switchMonth(month){
      switch(month){
        case 1:
          return 'Janvier';
        case 2:
          return 'Février';
        case 3:
          return 'Mars';
        case 4:
          return 'Avril';
        case 5:
          return 'Mai';
        case 6:
          return 'Juin';
        case 7:
          return 'Juillet';
        case 8:
          return 'Août';
        case 9:
          return 'Septembre';
        case 10:
          return 'Octobre';
        case 11:
          return 'Novembre';
        case 12:
          return 'Décembre';
        default:
          return 'Error';
      }
    }
  },
  beforeMount() {
    console.log('beforemount')
    this.today = new Date()
    this.numberDaysCurrentMonth = new Date(this.today.getFullYear(), this.today.getMonth()+1, 0).getDate()
    this.numberDaysLastMonth = new Date(this.today.getFullYear(), this.today.getMonth(), 0).getDate()
    this.mondayLastMonth = new Date()
    const tmpDate = new Date(this.today.getFullYear(), this.today.getMonth(), 1)
    this.mondayLastMonth.setDate(tmpDate.getDate() - ((tmpDate.getDay() + 6) % 7))
    this.mondayLastMonth = this.mondayLastMonth.getDate()
  }
});
</script>

<style>
  .grise {
    background-color: rgb(134, 134, 134);
  }
  .today {
    background-color: #2EC9FF;
    color: azure;
  }
  td {
    text-align: center;
    border: solid 1.5px;
    width: 14%;
  }
  th {
    border: solid 1px;
  }
  .row {
    height: 128px
  }
  table {
    margin-top: 30px;
    width: 100%
  }
  .divCalendar {
    background-color: aqua;
    border: solid 2px;
    border-radius: 15px;
    margin-left: 2%;
    margin-right: 2%;
    padding-bottom: 20px;
    margin-top: 20px;
    padding-left: 20px;
    padding-right: 20px;
    width: 96%;
  }
  h1{
    text-align: center;
  }
  .tableHeader{
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
    margin-top: 10px;;
  }
</style>
