<template>
  <v-row>
    <v-col>
      <v-tabs v-model='tabsModel' background-color='transparent' slider-size='3' centered>
        <v-tabs-slider color='#f15381'></v-tabs-slider>
        <v-tab
          v-for='(tab, i) in tabs'
          :key='i'
          class='primary--text'
          style='color:#f15381 !important'
        >
        {{tab}}</v-tab>
        <v-tabs-items v-model='tabsModel'>
          <v-tab-item>
            <v-row>
              <v-spacer></v-spacer>
              <v-col v-for='(index) in 3' :key='index' cols='2'>
                <v-hover>
                  <template v-slot:default='{ hover }'>
                    <v-card iclass='mx-auto mb-2'>
                      test
                    </v-card>
                  </template>
                </v-hover>
                <span> test + {{index}}</span>
              </v-col>
              <v-spacer></v-spacer>
            </v-row>
          </v-tab-item>
          <v-tab-item>
            <v-row>
              <v-spacer></v-spacer>
              <v-col v-for='(index) in 3' :key='index' cols='2'>
                <v-hover>
                  <template v-slot:default='{ hover }'>
                    <v-card id="cardIframe" class='mx-auto mb-2' height='250px'>
                        <span> test + {{index}}</span>
                    </v-card>
                  </template>
                </v-hover>
                <span> test + {{index}}</span>
              </v-col>
              <v-spacer></v-spacer>
            </v-row>
          </v-tab-item>
        </v-tabs-items>
      </v-tabs>
    </v-col>
  </v-row>
</template>

<script lang='ts'>
import { Vue, Prop, Component, Watch } from 'vue-property-decorator'
import moment from 'moment'
import _ from 'lodash'
import { Getter, Action } from 'vuex-class'

@Component
export default class TestTabComponent extends Vue {

  public tabs = ['Test1', 'Test2', 'Test3']
  public tabsModel = null
  public widthIframe = '0px'

  @Watch('$vuetify.breakpoint.width')
  @Watch('tabsModel')
  private calWidth() {
      const cardIframe = document.getElementById('cardIframe')
      console.log(cardIframe)
      const width = cardIframe ? cardIframe.clientWidth : 0
      this.widthIframe = (width * 4) + 'px'
  }

  private created() {
    this.calWidth()
  }

}
</script>