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
              <b-button class="mt-3" size="sm" @click="expandEvent(expand, index)">
                <b-icon icon="plus"></b-icon>
              </b-button>
            </template>
            <template v-else>
              <b-button class="mt-3" size="sm" @click="expandEvent(expand, index)">
                <b-icon icon="dash"></b-icon>
              </b-button>
            </template>
            <div v-show="expand">
              <draggable
                v-model="CardJsonData1"
                style="display: flex; justify-content: flex-start; flex-wrap: wrap"
              >
                <div
                  class="draggableCardContent"
                  v-for="(element, index) in CardJsonData1"
                  :key="index"
                >
                  <div class="row pl-2 pr-2 w-100">
                    <div class="col-md-3 pr-2 pl-2">
                      <img class="avatar" :src="require(`~/assets/images/${element.avatar}`)" alt />
                    </div>
                    <div class="col-md-9 pr-2 pl-2">
                      <div>{{element.title}}</div>
                      <div>{{element.description}}</div>
                    </div>
                  </div>
                </div>
              </draggable>
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
    CardJsonData1: [],
    CardJsonData2: [],
    CardJsonData3: [],
  }),
  mounted() {
    this.CardJsonData = CardJsonData;
    this.CardJsonData1 = CardJsonData[0].data;
    this.CardJsonData2 = CardJsonData[1].data;
    this.CardJsonData3 = CardJsonData[2].data;
    console.log(this.CardJsonData1);
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
      console.log(expand, index);
      var tempExpands = this.expands;
      this.expands = [];
      for (var i = 0; i < tempExpands.length; i++) {
        if (i === index) {
          if (expand === true) {
            this.expands[i] = false;
          } else {
            this.expands[i] = true;
          }
        } else {
          this.expands[i] = tempExpands[i];
        }
      }
      for (i = 0; i < this.expands.length; i++) {
        if (this.expands[i] === true) {
          this.totalExpand = true;
        } else {
          this.totalExpand = false;
        }
      }
    },
    clickCard() {
      this.$router.push({ path: "/Card" });
    },
  },
};
</script>
