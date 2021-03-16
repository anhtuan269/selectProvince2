<template>
  <div class="District">
    <select class="form-select" aria-label="Default select example">
      <option>Chose District</option>
      <template v-for="(district, index) in districtList" :key="index">
        <option
            v-show="selectedProvince === district.province_id"        
          :value="district.province_id"
        >
          {{ district.name }}
        </option>
      </template>
    </select>
  </div>
</template>

<script>
export default {
  name: "District",
  props: {
      districtList:Array,
      selectedProvince:Number
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
