<template>
  <header class="container">
    <section class="title">
      Covid - latest info
    </section>
  </header>
</template>

<script>
export default {
  name: "Navbar"
}
</script>

<style scoped lang="scss">
* {
  background: hsl(300, 100%, 25%);
}
.container {
  width: 100vw;
  height: 4em;
  display: flex;
  align-items: center;
  justify-content: center;
  .title {
    font-size: 2em;
  }
}
</style>