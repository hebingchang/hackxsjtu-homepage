<template>
  <div class="fixed-bg">
    <div class="title"> {{ $t('views')[2] }} </div>

    <div class="schedule-wrapper">
    <div class="schedule-column" v-for="line in schedule">
      <div v-for="event in line">
          <div v-if="event[0] === 'event-lg'"
            class="event-lg"
          >
            {{ event[1] }}
            {{ event[2] }}
          </div>
          <div v-else-if="event[0].startsWith('event-')"
            class="event-sm"
          >
            <div class="bubble" :class="event[0].slice(6)">{{ event[1] }}</div>
            <div class="bubble-right">{{ event[2] }}</div>
          </div>
          <div v-else-if="event[0].startsWith('span')"
            class="time-span" :class="event[0].slice(5)"
          >
          </div>
      </div>
    </div>
    </div>

  </div>
</template>

<script>
export default {
  name: 'timeline',
  props: {
    scheduleStrings: {
      required: true,
      type: Array
    }
  },
  computed: {
    schedule () {
      let s = this.scheduleStrings
      let ret = []
      let ind = 0
      let _ind = 0
      while ((ind = s.indexOf('---', _ind)) !== -1) {
        ret.push(Array.from(s.slice(_ind, ind), str => str.split('|')))
        _ind = ind + 1
      }
      ret.push(Array.from(s.slice(_ind), str => str.split('|')))
      return ret
    }
  }
}
</script>

<style scoped>
  .title {
    font-size: 30px;
    padding-top: 70px;
    margin-bottom: 70px;
  }
  .time-span {
    height: 30px;
    width: 3px;
    margin-top: -3px;
  }

  .event-lg {
    font-size: 25px;
    margin: 20px;
  }
  .event-sm {
    text-align: left;
    margin-bottom: 3px; 
  }
  .bubble {
    font-size: 20px;
    display: inline-block;
    height: 60px;
    width: 60px;
    line-height: 60px;
    text-align: center;
    
    padding: 10px;

    border-radius: 50%;
    
    color: #fff;
    font-weight: 900;
    transition: transform .4s;
  }
  .bubble:hover {
    transform: scale(1.1);
  }
  .bubble-right {
    display: inline-block;
    margin-left: 10px;
    text-align: left;
    font-size: 18px;
    font-weight: 900;
  }

  /* horizontal in pc, vertical in mobile */
  @media screen and (min-width: 600px) {
    .schedule-wrapper {
      display: flex;
      margin-right: 30px; 
    }
    .schedule-column {
      flex-grow: 1;
    }
    .time-span {
      margin-left: 190px;
    }
    .bubble {
      margin-left: 150px;
    }
  }
  @media screen and (max-width: 600px) {
    .time-span {
      margin-left: 110px;
    }
    .bubble {
      margin-left: 70px;
    }
  }

  .time-span.prepare { background-color: #9ae; }
  .time-span.rest { background-color: #9d9; }
  .time-span.working { background-color: #f90; }
  .time-span.crazy { background-color: #c44; }

  .bubble.prepare { background-color: #9ae; box-shadow: 1px 1px 3px #456; }
  .bubble.rest { background-color: #9d9; box-shadow: 1px 1px 3px #454; }
  .bubble.working { background-color: #f90; box-shadow: 1px 1px 3px #740; }
  .bubble.crazy { background-color: #c44; box-shadow: 1px 1px 3px #622; }

</style>
