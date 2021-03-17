<template>
  <div id="props">
    <Province
      :provinceList="provinces"
      :selectedProvince="dataProvince"
      @select:province="dataProvince = $event"
    >
    </Province>
    <District
      :districtList="districts"
      :selectedProvince="dataProvince"
      @select:province="dataProvince = $event"
    />
  </div>
  <Slot>
    <template v-slot:title >
      <h2 >{{ title }}</h2>
    </template>
    <template v-slot:content >
      <p >
        Lorem ipsum dolor, sit amet consectetur adipisicing elit. Aliquam eaque
        vitae, nobis quisquam facere dolores possimus? A, itaque? Sunt eos, nisi
        facere qui error magnam eum sed dolores aut exercitationem?
      </p>
    </template>
     <p class="default">default slot</p>

  </Slot>
</template>
<script>
import Province from "./components/Province.vue";
import District from "./components/District.vue";
import Slot from "./components/Slot.vue";

export default {
  name: "App",
  components: {
    Province,
    District,
    Slot,
  },
  data() {
    return {
      provinces: [],
      districts: [],
      dataProvince: 0,
      title: "Multy Slots",
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
#app #props {
  display: grid;
  grid-template-columns: 45% 45%;
  justify-content: space-between;
}
#app .form-control select option {
  cursor: pointer;
}
#app p {
  max-width: 480px;
  text-align: center;
  margin: auto;
}
#app .default {
  color: red;
}
</style>
