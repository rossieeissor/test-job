<template>
  <div class="beer-info">
    <div v-if="beerIsLoading" class="beer-info__loading">
      Looking for new beer for you ...
    </div>
    <p v-else class="beer-info__text">
      Try <strong>{{ beerInfo.name }}</strong> beer by
      <strong>{{ beerInfo.brand }}</strong
      >. {{ beerInfo.style }} style and {{ beerInfo.hop }} hop.
    </p>
  </div>
</template>

<script>
export default {
  props: {
    beerInfo: {
      type: Object,
      required: true,
    },
    beerIsLoading: {
      type: Boolean,
      required: true,
    },
  },
};
</script>

<style scoped>
.beer-info {
  position: relative;
  display: flex;
  justify-content: center;
  align-content: center;
  margin: 0 auto;
  min-width: 100%;
  min-height: 50%;
}

.beer-info__loading {
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 2rem;
  text-align: center;
}

.beer-info__text {
  font-size: 2rem;
  width: 90%;
  text-align: center;
}

@media screen and (max-width: 768px) {
  .beer-info__text {
    font-size: 1.6rem;
    margin: 0;
    position: absolute;
    top: 50%;
    -ms-transform: translateY(-50%);
    transform: translateY(-50%);
    margin-top: 20px;
  }
}
</style>
