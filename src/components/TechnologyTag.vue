<template>
  <div class="c-btn" @click="addFilter(text)">
    <div class="c-btn__text">{{ text }}</div>
  </div>
</template>

<script>
export default {
  props: ["text"],
  methods: {
    addFilter(tag) {
      this.$emit("addFilter", tag);
    },
  },
};
</script>

<style lang="scss" scoped>
.c-btn {
  background-color: #effafa;
  color: #5ba4a4;
  font-weight: bolder;
  border-radius: 5px;
  margin: 8px;
  transition: all 0.2s;
  overflow: hidden;
  display: flex;
  cursor: pointer;
  @media only screen and (max-width: 850px) {
    font-size: 13px;
  }
}

.c-btn__text {
  padding: 7px;
}
</style>
