<template>
  <Province
    :provinceList="provinces"
    :selectedProvince="dataProvince"
    @select:province="dataProvince = $event"
  />
  <District
    :districtList="districts"
    :selectedProvince="dataProvince"
    @select:province="dataProvince = $event"
  />
</template>

<script>
import Province from "./components/Province.vue";
import District from "./components/District.vue";

export default {
  name: "App",
  components: {
    Province,
    District,
  },
  data() {
    return {
      provinces: [],
      districts: [],
      dataProvince: 0,
    };
  },
  mounted() {
    this.fetchData();
  },
  methods: {
    fetchData() {
      fetch(
        "https://api.muabannhanh.com/province/list?session_token=cb2663ce82a9f4ba448ba435091e27bb&phone=0362342558"
      )
        .then((res) => res.json())
        .then((data) => {
          if (data.status === 200) {
            data.result.map((p) => {
              this.provinces.push({
                id: p.id,
                name: p.name,
              });
              p.district.map((d) => {
                this.districts.push({
                  id: d.id,
                  name: d.name,
                  province_id: d.province_id,
                });
              });
            });
          }
        })
        .catch((err) => alert(err));
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#app {
  display: grid;
  grid-template-columns: 45% 45%;
  justify-content: space-between;
}
#app .form-control select option {
  cursor: pointer;
}
</style>
