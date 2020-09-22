<template>
  <div class="wrapper">
    <Header />
    <div class="container">
      <div class="row">
        <div class="col-md-12 mb-2">
          <div class="mt-1">
            <strong class="mr-3">Expand All:</strong>
            <template v-if="totalExpand === false">
              <b-button size="sm" @click="expandAllEvent">
                <b-icon icon="plus"></b-icon>
              </b-button>
            </template>
            <template v-else>
              <b-button size="sm" @click="expandAllEvent">
                <b-icon icon="dash"></b-icon>
              </b-button>
            </template>
          </div>
        </div>
        <div class="col-md-12" v-for="(expand, index) in expands" :key="index">
          <div class="row align-items-start mt-1 mb-1">
            <template v-if="expand === false">
              <b-button size="sm" @click="expandEvent(expand, index)">
                <b-icon icon="plus"></b-icon>
              </b-button>
            </template>
            <template v-else>
              <b-button size="sm" @click="expandEvent(expand, index)">
                <b-icon icon="dash"></b-icon>
              </b-button>
            </template>
            <div v-show="expand">
              <div
                class="row mx-3"
                v-for="(singleRowData, rowIndex) in CardJsonData[index]"
                :key="rowIndex"
              >
                <div
                  class="col-md-2 mb-1 mx-2 p-0"
                  v-for="(singleCellData, cellIndex) in singleRowData"
                  :key="cellIndex"
                >
                  <draggable>
                    <div
                      class="draggableCard"
                      @click="clickCard"
                    >{{singleCellData.title}}{{singleCellData.description}}</div>
                  </draggable>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Vue from "vue";
import Header from "~/components/Header.vue";
import { BootstrapVue, BootstrapVueIcons } from "bootstrap-vue";
import draggable from "vuedraggable";
import CardJsonData from "@/assets/json/CardJsonData.json";
Vue.use(BootstrapVue);
Vue.use(BootstrapVueIcons);

export default {
  components: {
    Header,
    draggable,
  },
  data: () => ({
    expands: [],
    totalExpand: true,
    CardJsonData: [],
  }),
  mounted() {
    this.CardJsonData = CardJsonData;
    for (var i = 0; i < this.CardJsonData.length; i++) {
      this.expands.push(true);
    }
  },
  methods: {
    expandAllEvent() {
      this.expands = [];
      if (this.totalExpand === true) {
        this.totalExpand = false;
      } else {
        this.totalExpand = true;
      }
      for (var i = 0; i < this.CardJsonData.length; i++) {
        this.expands[i] = this.totalExpand;
      }
    },
    expandEvent(expand, index) {
      var tempExpands = this.expands;
      this.expands= [];
      for(var i=0; i< tempExpands.length; i++) {
        if(i === index ){
          if (expand === true) {
            this.expands[i] = false;
          } else {
            this.expands[i] = true;
          }
        }else {
          this.expands[i] = tempExpands[i]
        }
      }
      for (i = 0; i<this.expands.length; i++) {
        if(this.expands[i] === true) {
          this.totalExpand = true
        } else {
          this.totalExpand = false
        }
      }
    },
    clickCard() {
      this.$router.push({path: '/Card'});
    },
  },
};
</script>
