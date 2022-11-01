<template>
  <div class="select">
    <div class="select-selected" @click="toggleDropDown">
      <div v-if="selected">{{ selected }}</div>
      <div v-else>Filter by gender</div>
    </div>
    <div v-if="isOptionsOpen" class="select-options">
      <div
        v-for="(item, idx) in options"
        :key="idx"
        @click="clickOption(item)"
        class="select-item"
      >
        {{ item }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["options", "selected"],
  data() {
    return {
      isOptionsOpen: false,
    };
  },
  methods: {
    toggleDropDown() {
      this.isOptionsOpen = !this.isOptionsOpen;
    },
    clickOption(value) {
      this.$emit("changeValue", value);
      this.toggleDropDown();
    },
  },
};
</script>

<style scoped>
.select {
  position: relative;
  min-width: 120px;
}
.select .select-selected {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 10px;
  border: 1px solid #e2e8f0;
  border-radius: 6px;
  font-size: 13px;
  cursor: pointer;
}
.select-options {
  position: absolute;
  width: 100%;
  top: 50px;
  z-index: 10;
}
.select-item {
  background: white;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 10px;
  border: 1px solid #e2e8f0;
  border-radius: 6px;
  font-size: 13px;
  cursor: pointer;
  margin-bottom: 5px;
  box-shadow: 0px 45px 112px rgba(0, 0, 0, 0.06),
    0px 22.7812px 48.825px rgba(0, 0, 0, 0.0405),
    0px 9px 18.2px rgba(0, 0, 0, 0.03),
    0px 1.96875px 6.475px rgba(0, 0, 0, 0.0195);
}
</style>
