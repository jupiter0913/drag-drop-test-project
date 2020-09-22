<template>
  <div class="wrapper">
    <Header />
    <div class="container">
      <div class="row">
        <draggable v-model="ContentJsonData" style="display: flex; justify-content: flex-start; flex-wrap: wrap">
          <div
            class="draggableCardContent"
            v-for="(element, index) in ContentJsonData"
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
</template>

<script>
import Vue from "vue";
import Header from "~/components/Header.vue";
import draggable from "vuedraggable";
import ContentJsonData from "@/assets/json/ContentJsonData.json";
export default {
  components: {
    Header,
    draggable,
  },
  data: () => ({
    ContentJsonData: [],
  }),
  mounted() {
    this.ContentJsonData = ContentJsonData;
  },
  methods: {
  },
};
</script>
