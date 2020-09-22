<template>
  <div class="wrapper">
    <Header />
    <div class="container">
      <div class="row">
        This is a Card Page.
      </div>
    </div>
  </div>
</template>

<script>
import Vue from "vue";
import Header from "~/components/Header.vue";
export default {
  components: {
    Header,
  },
  data: () => ({
  }),
  mounted() {
  },
  methods: {
  },
};
</script>
