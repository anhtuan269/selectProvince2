<template>
  <div class="Province">
    <select
      class="form-select"
      aria-label="Default select example"
      v-model="selected"
      @click="select"
    >
      <option>Chose Province</option>
      <option
        v-for="(province, index) in provinceList"
        :key="index"
        :value="province.id"
      >
        {{ province.name }}
      </option>
    </select>
  </div>
</template>

<script>
export default {
  data() {
    return {
      selected: this.selectedProvince,
    };
  },
  name: "Province",
  props: {
    provinceList: Array,
    selectedProvince: Number,
  },
  watch: {
    selected: function () {
      this.$emit("select:province", this.selected);
    },
  },
  computed: {},
  methods: {
    // select() {
    //   this.$emit('select:province', this.selected);
    // }
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
