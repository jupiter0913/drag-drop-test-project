<template>
  <div class="wrapper">
    <Header />
    <div class="container">
      <div class="row">
        <div class="col-md-12">
          <div class="mt-1">
            <strong class="mr-3">Expand All:</strong>
            <template v-if="totalExpand === false">
              <b-button size="sm" @click="expandEvent">
                <b-icon icon="plus"></b-icon>
              </b-button>
            </template>
            <template v-else>
              <b-button size="sm" @click="expandEvent">
                <b-icon icon="dash"></b-icon>
              </b-button>
            </template>
          </div>
        </div>
        <div class="col-md-12" v-for="(expand, index) in expands" :key="index">
          <div> {{CardJsonData[index]}}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Vue from "vue";
import Header from "~/components/Header.vue";
import { BootstrapVue, BootstrapVueIcons } from 'bootstrap-vue';

import CardJsonData from "@/assets/json/CardJsonData.json";
Vue.use(BootstrapVue)
Vue.use(BootstrapVueIcons)

export default {
  components: {
    Header
  },
  data: () => ({
    expands: [],
    totalExpand: true,
    CardJsonData: []
  }),
  mounted() {
    this.CardJsonData = CardJsonData
    for(var i = 0; i < this.CardJsonData.length; i++) {
      this.expands.push(true);
    }
  },
  methods: {
    expandEvent() {
      for (var i = 0; i < this.count; i++) {
        if (this.expands[i] === false) {
          this.totalExpand = false;
        }
      }
      this.expands = [];
      if (this.totalExpand === true) {
        this.totalExpand = false;
        for (var i = 0; i < this.count; i++) {
          this.expands[i] = false;
        }
      } else {
        this.totalExpand = true;
        for (var i = 0; i < this.count; i++) {
          this.expands[i] = true;
        }
      }
    },
  }
};
</script>
