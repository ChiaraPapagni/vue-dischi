<template>
  <header id="site_header">
    <img src="../assets/img/logo.png" alt="Spotify" />
  </header>
  <!-- /#site_header -->
</template>

<script>
export default {};
</script>

<style lang="scss">
@import "../assets/scss/variables.scss";

#site_header {
  background-color: $light_background_color;

  img {
    width: 40px;
    height: 40px;
    margin: 0.5rem 0.7rem;
  }
}
</style>