<template>
  <div class="fixed-bg">

    <h1 v-html="$t('host')"></h1>

    <div class="img-flow-horiz">
      <div v-for="(name, ind) in $t('hosts')">
        <!-- img used in v-for should be put directly in /static/img dir -->
        <!-- reference: http://www.jianshu.com/p/f82c5ecbd3a5 -->
        <img :src="'/static/img/host-' + ind + '.png'">
        <p>{{ name }}</p>
      </div>
    </div>

    <h1 v-html="$t('organizer')"></h1>
    <img src="../assets/hackx.png">

    <h1 v-html="$t('sponsor')"></h1>

    <div>
      <div class="img-flow-horiz img-sp" v-for="sp in sponsors">
        <div v-for="(href, name) in sp">
          <!-- img used in v-for should be put directly in /static/img dir -->
          <a :href="href" target="_blank">
            <img :src="'/static/img/brands/' + name + '.png'">
          </a>
        </div>
      </div>
    </div>

    <div class="flex-wrapper">
      <div class="column">
        <div>
          <p v-html="$t('rightStatement')"></p>
        </div>
      </div>
      <div class="column">
        <div>
          <img id="qrcode" src="../assets/qrcode.png">
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app-footer',
  data () {
    return {
      sponsors: [{
        'wework': 'https://www.wework.cn/',
        'vivex': 'https://vivex.vive.com/',
        'netease': 'http://www.163.com/',
        'neteasedj': 'https://dongjian.163.com/'
      }, {
        'neteasegame': 'http://game.163.com/',
        'genaro': 'https://genaro.network/',
        'lls': 'https://www.liulishuo.com/',
        'innospace': 'http://www.innospaceplus.com.cn/'
      }, {
        'ibm': 'http://ibm.com/cloud-computing',
        'ruffchain': 'https://ruffchain.com/',
        'dfrobot': 'https://www.dfrobot.com/',
        'mgy': 'http://www.mushroomcloud.cc/'
      }]
    }
  }
}
</script>

<style scoped>
h1 {
  /* do not use margin top because it will influence fixed-bg */
  padding-top: 70px;
  margin-top: 0;
  margin-bottom: 70px;
}
img {
  max-height: 180px;
}
.img-flow-horiz {
  display: flex;
  justify-content: space-around;
  flex-wrap: wrap;
  align-items: center;
}
.img-flow-horiz img {
  max-width: 200px;
}
.img-flow-horiz p {
  max-width: 200px;
  margin-left: auto;
  margin-right: auto;
}

.column {
  display: flex;
  flex-direction: column;
  justify-content: center;
}
#qrcode {
  height: 200px;
}

@media screen and (min-width: 600px) {
  .flex-wrapper {
    display: flex;
  }
  .column {
    width: 50%;
    height: 300px;
  }
}
@media screen and (max-width: 600px) {
  .column {
    height: 200px;
  }
}
</style>
