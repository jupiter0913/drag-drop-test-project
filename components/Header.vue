<template>
  <header class="header" id="header">
    <div class="top_container">
      <div class="row align-items-center">
        <div class="col headerBlockB">
          <div class="mainNav">
            <button class="mobileNavBtn">
              <span></span>
              <span></span>
              <span></span>
            </button>
            <div class="overLay"></div>
            <nav class="navigation">
              <ul>
                <li @click="closeMenu">
                  <nuxt-link :to="{ path: '/' }">Home</nuxt-link>
                </li>
                <li @click="closeMenu">
                  <nuxt-link :to="{ path: '/Card' }">Card</nuxt-link>
                </li>                
              </ul>
            </nav>
          </div>
        </div>        
      </div>
    </div>
  </header>
</template>

<script>
export default {
  mounted() {
    $(".mobileNavBtn, .overLay").click(function() {
      if ($(this).parents("body").hasClass("openNav")) {
        $(this).parents("body").removeClass("openNav");
      } else {
        $(this).parents("body").addClass("openNav");
      }
    });
  },
  methods: {
    closeMenu() {
      $(".mobileNavBtn, .overLay").parents("body").removeClass("openNav");
    }
  }
};
</script>