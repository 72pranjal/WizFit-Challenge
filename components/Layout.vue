<template>
  <div class="conatiner">
    <div class="herder-image">
      <img src="/images/banner.png" alt="main Banner" />
    </div>
    <div class="heading">
      <div class="text-image">
        <h2>What is WizFit Challenge?</h2>
        <img src="/images/watch.png" alt="watch" />
      </div>
      <img class="player" src="/images/player.png" alt="Player" srcset="" />
    </div>
  </div>
</template>
<script>
export default {
  name: "Layout",
};
</script>

<style scoped>
.herder-image {
  width: 100%;
  margin-top: 5px;
}

.herder-image img {
  width: 100%;
  height: auto;
}

.heading {
  margin: 20px;
  text-align: center;
}

.heading h2 {
  font-size: 28px;
  color: brown;
  font-weight: 800;
}

.heading .player {
  width: 20%;
}

.heading .text-image {
  display: flex;
  justify-content: center;
  gap: 35px;
  align-items: center;
}
</style>
