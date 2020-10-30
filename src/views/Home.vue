<template>
  <div class="home">
    <div class="container">
      <div class="search-holder">
        <img src="~@/assets/icons/icon_calender.svg" @click='calendarVisible = !calendarVisible' alt="calender" width="18px">
        <input type="text" class="search" v-model="search" @click="range = {start: null,end: null}">
        <p class="date" v-if="range.start">{{$momemt(range.start).format('YYYY/MM/DD')}} - {{$momemt(range.end).format('YYYY/MM/DD')}}</p>
        <div class="img">
          <img src="~@/assets/icons/icon_search.svg" alt="search" width="18px">
        </div>
      </div>
      <DatePicker class="calendar" v-if="calendarVisible" v-model="range" is-range />
      <div class="result">
        <p> Result: <span>{{result}}</span>mail(s)</p>
        <hr>
      </div>
      <v-data-table
          hide-default-footer
          :hide-default-header="result ===  0"
          :headers="headers"
          :items="items"
          :items-per-page="10"
          :search="search"
          class="elevation-1"
          mobile-breakpoint="0"
      >
        <template v-slot:item.subject="{ item }" >
          <p>{{ item.subject }}</p>
        </template>

        <template v-slot:item.date="{ item }">
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 13.93083 15" width="18" v-if="item.files">
            <title>icon_clip</title>
            <path class="a"
                  d="M6.799,3.6254A2.30522,2.30522,0,1,0,3.56718,6.85622l4.304,4.304a.5222.5222,0,0,0,.7385-.7385l-4.304-4.304c-.53586-.53586-.87743-1.33808-.23084-1.98466.64553-.64659,1.4488-.304,1.98466.23189L11.032,9.3364c1.90632,1.90841,2.38159,2.78793,1.24615,3.92441-1.149,1.148-2.367.86385-4.20121-.96935L2.367,6.57941C1.1741,5.38653.33845,3.43842,1.90633,1.87159c1.86141-1.86141,3.98708-.03134,4.59293.57555l5.11038,5.11142a.5222.5222,0,0,0,.7385-.7385L7.23776,1.70864C5.18625-.34288,2.86-.56223,1.16678,1.13308c-1.711,1.71-1.5261,4.196.4617,6.18484l5.711,5.711C7.96726,13.6567,9.31161,15,10.85756,15a3.01214,3.01214,0,0,0,2.16014-1.00173c2.07554-2.07658.15564-3.99857-1.24616-5.40141Z"/>
          </svg>
          <p class="date">{{ item.date }}</p>
          <img src="~@/assets/icons/icon_arrow02.svg" class="arrow" alt="search" width="4px">
        </template>

        <template v-slot:item.to="{ item }">
          <div class="to">
            <p>{{ item.to[0] }} <span v-if="item.to.length > 1">, ...</span></p>
            <p v-if="item.to.length > 1" class="toMatch">+{{ item.to.length - 1 }}</p></div>
          <img src="~@/assets/icons/icon_mail_sp.svg" class="mail">
        </template>

        <template v-slot:no-results>
          <img id='logo' alt="Vue logo" src="../assets/logo.png">
        </template>
      </v-data-table>
    </div>
  </div>
</template>

<script>
import Calendar from 'v-calendar/lib/components/calendar.umd'
import DatePicker from 'v-calendar/lib/components/date-picker.umd'
import moment from 'moment'

export default {
  name: 'Home',
  components: {
    Calendar,
    DatePicker
  },
  data() {
    return {
      search: '',
      range: {
        start: null,
        end: null
      },
      calendarVisible: false,
      date: new Date(),
      result: 0,
      headers: [
        {text: 'From', value: 'fromm'},
        {text: 'To', value: 'to'},
        {text: 'Subject', value: 'subject'},
        {text: 'Date', value: 'date'}
      ],
      itemsTemp:[
        {
          fromm: 'aaa@exampple.com',
          to:['zzz.zzz@exampple.com'],
          subject:'[ HR-888 ] Notice of official announcement',
          date:'0:20',
          datafull: moment().startOf('day').add(20, 'minutes')
        },
        {
          fromm: 'bbb@exampple.com',
          to:['yyy@exampple.com'],
          subject:'[web:333] "Web Contact"',
          date:'0:10',
          datafull: moment().startOf('day').add(10, 'minutes'),
        },
        {
          fromm: 'ccc@exampple.com',
          to:['xxx@exampple.com', 'mmm@exampple.com'],
          subject:'Happy New Year! Greetings for the New Year.',
          date:'0:00',
          datafull:  moment().startOf('day'),
          files: [
            {
              text:'123'
            }
          ]
        },
        {
          fromm: 'ddd.dddd@exampple.com',
          to:['vvv.vvv@exampple.com', 'nnn@exampple.com'],
          subject:'[ HR-888 ] Notice of official announcement',
          date:'Jan 01',
          datafull:  moment('20200101', 'YYYYMMDD')
        },
        {
          fromm: 'eee@exampple.com',
          to:['sss@exampple.com','uuu@exampple.com','kkk@exampple.com'],
          subject:'[HR-887(Revised: Office Expansion Project Team)] Notice of off...',
          date:'Jan 01',
          datafull:  moment('20200101', 'YYYYMMDD')
        },
        {
          fromm: 'fff.ffffexampple.com',
          to:['qqq.qqq@exampple.com'],
          subject:'［dev］ Postfix 3.1.12 / 3.2.9 / 3.3.4 / 3.4.5',
          date:'Jan 01',
          datafull:  moment('20200101', 'YYYYMMDD')
        },
        {
          fromm: 'ggg@exampple.com',
          to:['ppp@exampple.com'],
          subject:'Re: [Github] Brush-up on loading animation',
          date:'Jan 01',
          datafull:  moment('20200101', 'YYYYMMDD')
        },
        {
          fromm: 'hhh.hhh@exampple.com',
          to:['ooo.ooo@exampple.com'],
          subject:'Workplace Summary for sample, Inc.: Jun 2 - Jun 9',
          date:'Jan 01',
          datafull:  moment('20200101', 'YYYYMMDD'),
          files: [
            {
              text:'123'
            }
          ]
        },
        {
          fromm: 'iii@exampple.com',
          to:['nnn@exampple.com'],
          subject:'I love you',
          date:'2019/12/31',
          datafull: moment('2019/12/31'),
          files: [
            {
              text:'123'
            }
          ]
        },
        {
          fromm: 'Pablo-Diego-...',
          to:['Pablo-Diego-José-Francisc...'],
          subject:'[info:888] ABC EQUIPMENT COMPANY',
          date:'2019/12/31',
          datafull: moment('2019/12/31')
        },
      ]
    }
  },
  computed: {
    items() {
      let th = this;
      return this.itemsTemp.filter(item => {
        if (th.range.start) {
          let start    = moment(th.range.start).format('DD/MMMM/YYYY'),
              end      = moment(th.range.end).format('DD/MMMM/YYYY'),
              itemDate = moment(item.datafull).format('DD/MMMM/YYYY')
          return th.$momemt(start).isSame(th.$momemt(itemDate)) || th.$momemt(end).isSame(th.$momemt(itemDate)) || th.$momemt(start).isBefore(th.$momemt(itemDate)) && th.$momemt(end).isAfter(th.$momemt(itemDate))
        } else {
          return true
        }
      });
    }
  },
  mounted() {
    this.result = document.querySelectorAll('.v-data-table__wrapper tbody tr:not(.v-data-table__empty-wrapper)').length
  },
  updated() {
    this.result = document.querySelectorAll('.v-data-table__wrapper tbody tr:not(.v-data-table__empty-wrapper)').length
  }
}
</script>

<style lang="scss">
  .home {
    .mdi-arrow-up::before {
      background: url("~@/assets/icons/icon_arrow01.svg") no-repeat center center / contain;
      width: 11px;
      height: 11px;
      content: '';
    }
    .container {
      .calendar {
        position: absolute;
        z-index: 2;
        top: 75px;
      }
      .search-holder {
        position: relative;
        margin-top: 25px;
        margin-bottom: 50px;
        display: flex;
        border: 1px solid #ccc;
        padding-left: 20px;
        z-index: 1;
        border-radius: 10px;
        overflow: hidden;
        input {
          outline: none;
          margin-right: 10px;
          margin-left: 10px;
        }
        .date {
          width: 100%;
          height: 100%;
          display: flex;
          align-items: center;
          box-sizing: border-box;
          padding-left: 30px;
          position: absolute;
          font-size: 12.5px;
          z-index: -1;
          color: rgb(51, 51, 51);
        }
        .img {
          background: rgb(245,245,245);
          padding: 5px 10px;
          border-left: 1px solid #ccc;
        }
      }
      .subject {
        display: flex;
        justify-content: space-between;
      }
      .elevation-1 {
        width: 100%;
        box-shadow: none!important;
        tr {
          &.v-data-table__empty-wrapper {
            td {
              border-bottom: 0;
            }
          }
          td {
            border-bottom: thin solid rgba(0, 0, 0, 0.12);
            .to {
              display: flex;
              justify-content: space-between;
              .toMatch {
                width: 25px;
                line-height: 20px;
                background: rgb(136, 136,136);
                border-radius: 5px;
                color: white!important;
                text-align: center;
                display: flex;
                justify-content: center;
              }
            }
            p {
              display: flex;
              justify-content: space-between;
              &.date {
                font-weight: bold;
              }
            }
            .a {
              fill: #666;
            }
            svg {
              position: absolute;
              right: 12.5%;
              width: 14px;
            }
          }
          &:hover {
            td {
              color:blue;
              p {
                color: currentColor;
                &.date {
                  color: #000000;
                }
              }
              .a {
                fill: blue;
              }
            }
          }
        }
      }
      .result {
        width: 100%;
        p {
          font-size: 17px;
          font-weight: bold;
          color: rgba(0, 0, 0, 0.6);
          span {
            font-size: 22.5px;
          }
        }
      }
      .form {
        display: flex;
        justify-content: space-between;
        background: rgb(245, 245, 245);
        padding-top: 10px;
        p {
          margin-top: 5px;
        }
      }
      #logo {
        display: flex;
        justify-content: center;
        align-items: center;
        margin: 0 auto;
        margin-top: 10%;
      }
      .emails {
        display: flex;
        justify-content: space-between;
        padding-top: 10px;
      }
      .arrow, .mail {
        display: none;
      }

    }

  }

</style>
