<template>
  <div>
    <v-layout class="v-card white secondary--text" row wrap>
      <v-flex pt-5 pb-4 px-5 xs12>
        <div :class="{[$store.state.colorTheme] : true}" style="height:5px;width:100%"></div>
        <v-layout py-3 wrap row>
          <v-flex xs6>
            <div class="display-1 bold">
              <span :class="{[colorTheme] : true}">
                {{ $store.state.mallData.name }}
              </span>
            </div>
          </v-flex>
           <v-flex text-xs-right xs6>
            <div class="display-1">
              <span :class="{[colorTheme] : true}">
                {{ $store.state.mallData.phoneNr }}
              </span>
            </div>
          </v-flex>
          <v-flex xs6>
            <div class="subheading">
              {{ $store.state.mallData.zip }},
              {{ $store.state.mallData.city }},
              {{ $store.state.mallData.country }}
            </div>
          </v-flex>
           <v-flex text-xs-right xs6>
            <div class="subheading">
              {{ $store.state.mallData.email }}
            </div>
          </v-flex>
        </v-layout>
        <div :class="{[$store.state.colorTheme] : true}" style="height:5px;width:100%"></div>
      </v-flex>
      <v-flex pb-3 px-5 xs12>
        <div class="pt-2" v-if="$store.state.mallData.sammanfattning.length > 0">
          <div :class="{[colorTheme] : true}">
            <span class="title bold">
              {{ $store.getters.whatLang[0] }}
            </span>
          </div>
          <div class="body-1">
            {{ $store.state.mallData.sammanfattning }}
          </div>
        </div>
        <div class="title bold pt-4 pb-3">
          <div :class="{[colorTheme] : true}">
            {{ $store.getters.whatLang[1] }}
          </div>
        </div>
        <div class="pb-4" :key="x.id" v-for="x in $store.state.mallData.work">
          <div class="subheading bold secondary--text">
            {{ x.roll }}, {{ x.corp }}
          </div>
          <div class="body-2 pt-1 pb-2 secondary--text">
            {{ x.period }}
          </div>
          <div>
            <ul>
              <span :key="index" v-for="(d, index) in x.description.split('.')">
                <li v-if="index < (x.description.split('.').length - 1)">
                  {{ d }}
                </li>
              </span>
            </ul>
          </div>
        </div>
        <div v-if="$store.state.mallData.education.length > 0">
          <div class="title bold pt-3 pb-3">
            <div :class="{[colorTheme] : true}">
              {{ $store.getters.whatLang[3] }}
            </div>
          </div>
          <div class="pb-3" :key="x.id" v-for="x in $store.state.mallData.education">
            <div class="subheading bold secondary--text">
              {{ x.subject }}
            </div>
            <div class="subheading secondary--text">
              {{ x.school }}
            </div>
            <div class="body-2 pt-1 pb-2 secondary--text">
              {{ x.period }}
            </div>
          </div>
        </div>
        <div v-if="$store.state.mallData.skills.length > 0">
          <div class="title bold pt-3 pb-3">
            <div :class="{[colorTheme] : true}">
              {{ $store.getters.whatLang[2] }}
            </div>
          </div>
          <ul>
            <span :key="i" v-for="(x, i) in $store.state.mallData.skills">
              <li class="secondary--text">
                {{ x }}
              </li>
            </span>
          </ul>
        </div>
        <div v-if="$store.state.mallData.languages.length > 0">
          <div class="title bold pt-3 pb-3">
            <div :class="{[colorTheme] : true}">
              {{ $store.getters.whatLang[8] }}
            </div>
          </div>
           <div class="pb-3" :key="x.id" v-for="x in $store.state.mallData.languages">
              <div style="margin-bottom:-10px" class="subheading bold">
                {{ x.lang }}
              </div>
              <div style="position:relative;width:60%">
                <v-progress-linear height="10px" :value="x.niva * 20" color="secondary"></v-progress-linear>
                <div style="position:absolute;right:0;top:10px" class="secondary--text body-1">
                  {{ level(x.niva) }}
                </div>
              </div>
          </div>
        </div>
        <div class="pb-3" v-if="$store.state.mallData.hobbier.length > 0">
          <div class="title bold pt-3 pb-3">
            <div :class="{[colorTheme] : true}">
              {{ $store.getters.whatLang[6] }}
            </div>
          </div>
          <ul>
            <span class="mb-4" :key="i" v-for="(x, i) in $store.state.mallData.hobbier">
              <li class="body-2">
                {{ x }}
              </li>
            </span>
          </ul>
        </div>
        <div class="pb-3" v-if="$store.state.mallData.utmarkelser.length > 0">
          <div class="title bold pt-3 pb-3">
            <div :class="{[colorTheme] : true}">
              {{ $store.getters.whatLang[4] }}
            </div>
          </div>
          <ul>
            <span class="mb-4" :key="i" v-for="(x, i) in $store.state.mallData.utmarkelser">
              <li class="body-2">
                {{ x }}
              </li>
            </span>
          </ul>
        </div>
        <div class="pb-3" v-if="$store.state.mallData.volontararbete.length > 0">
          <div class="title bold pt-3 pb-3">
            <div :class="{[colorTheme] : true}">
              {{ $store.getters.whatLang[9] }}
            </div>
          </div>
          <ul>
            <span class="mb-4" :key="i" v-for="(x, i) in $store.state.mallData.volontararbete">
              <li class="body-2">
                {{ x }}
              </li>
            </span>
          </ul>
        </div>
        <div class="pb-3" v-if="$store.state.mallData.links.length > 0">
          <div class="title bold pt-3 pb-3">
            <div :class="{[colorTheme] : true}">
              {{ $store.getters.whatLang[7] }}
            </div>
          </div>
          <ul>
            <span class="mb-4" :key="i" v-for="(x, i) in $store.state.mallData.links">
              <li class="body-2">
                <a target="_blank" :href="x">{{ x }}</a>
              </li>
            </span>
          </ul>
        </div>
        <div v-if="$store.state.mallData.referenser.length > 0">
          <div class="title pt-3 bold">
            <span :class="{[colorTheme] : true}">
              {{ $store.getters.whatLang[5] }}
            </span>
          </div>
          <div style="width:50%" :key="x.id" v-for="(x, i) in $store.state.mallData.referenser" :class="{'grey lighten-3' : i % 2 === 0, 'white' : i % 2 !== 0, 'px-1 my-3 py-1 body-1' : true}">
            <div class="bold">
              {{ x.name }}
            </div>
              <div class="body-2">
              {{ x.tel }}
            </div>
            <div>
              {{ x.relation }}
            </div>
          </div>
        </div>
      </v-flex>
    </v-layout>
  </div>
</template>

<script>
export default {
  data: () => ({
    msg: true
  }),
  computed: {
    headingClass () {
      return 'subheading bold px-3 py-1 darken-3 borderTopAndBottom'
    },
    darkenClass () {
      return 'darken-3'
    },
    colorTheme () {
      return this.$store.state.colorTheme.split(' ')[0] + '--text'
    }
  },
  methods: {
    level (x) {
      let levels
      if (this.$store.state.choosedLang === 0) {
        levels = ['Låg', 'Medel', 'Bra', 'Mycket bra', 'Strålande']
      } else if (this.$store.state.choosedLang === 1) {
        levels = ['Low', 'Average', 'Good', 'Very good', 'Excellent']
      }
      if (x === 1) {
        return levels[0]
      } else if (x === 2) {
        return levels[1]
      } else if (x === 3) {
        return levels[2]
      } else if (x === 4) {
        return levels[3]
      } else if (x === 5) {
        return levels[4]
      } else {
        return ''
      }
    }
  }
}
</script>

<style>
.borderTopAndBottom {
  border-top: 1px solid #fff!important;
  border-bottom: 1px solid #fff!important;
}
</style>
