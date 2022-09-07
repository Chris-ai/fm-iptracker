<template>
  <div class="wrap">
    <p>{{ label }}</p>
    <h3>{{ info }}</h3>
  </div>
</template>

<script>
export default {
  props: ["label", "info"],
};
</script>

<style lang="scss" scoped>
.wrap {
  margin: 0.5rem 0;
  max-width: 150px;
  word-wrap: break-word;

  // height: 100%;
  p {
    text-transform: uppercase;
    margin: 0.3rem;
    font-size: 10px;
    color: var(--dark-gray);
    font-weight: var(--fw-bold);
    letter-spacing: 1.5px;
    line-height: 1.5;
  }

  h3 {
    color: rgb(43, 43, 43);
  }

  @media (min-width: 650px) {
    display: flex;
    flex-direction: column;
    height: 100px;

    p {
      align-self: flex-start;
    }
  }
}
</style>