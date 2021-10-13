<template>
  <div class="homepage">
    <div class="filtering">
      <div class="find-customer">
        <img src="../assets/img/icons/search.svg" alt="search-icon" />
        <input v-model="filterKey" placeholder="Find customers" />
      </div>
      <div class="filter-order">
        <custom-select :options="filterOptions" @select="selectOption" />
      </div>
    </div>
    <div class="data-container" v-if="!loading && mainData && mainData.length">
      <customer-comp
        v-for="customer of filterCustomers()"
        :key="customer.id"
        :customer="customer"
      />
    </div>
    <loader :loading="loading" />
  </div>
</template>

<script>
import { onMounted, ref } from "vue";
import Loader from "../components/Loader";
import CustomerComp from "../components/CustomerComp.vue";
import CustomSelect from "../components/CustomSelect.vue";
import _ from "lodash";
// import { customers } from "../assets/mock-data";

export default {
  name: "HomePage",
  components: {
    Loader,
    CustomerComp,
    CustomSelect,
  },
  setup() {
    const mainData = ref(null);
    const loading = ref(true);
    const error = ref(null);
    const filterKey = ref("");
    const selected = ref({
      value: 0,
      label: "Original",
    });
    const filterOptions = [
      {
        value: 0,
        label: "Original",
      },
      {
        value: 1,
        label: "Name (A-Z)",
      },
      {
        value: -1,
        label: "Name (Z-A)",
      },
    ];

    function fetchData() {
      // mainData.value = customers;
      // loading.value = false;
      // console.log("mock-customers", customers);

      loading.value = true;

      return fetch("https://jsonplaceholder.typicode.com/users", {
        method: "get",
        headers: {
          "content-type": "application/json",
        },
      })
        .then((res) => {
          if (!res.ok) {
            const error = new Error(res.statusText);
            error.json = res.json();
            throw error;
          }

          return res.json();
        })
        .then((json) => {
          mainData.value = json;
        })
        .catch((err) => {
          error.value = err;
          if (err.json) {
            return err.json.then((json) => {
              error.value.message = json.message;
            });
          }
        })
        .then(() => {
          loading.value = false;
        });
    }

    onMounted(() => {
      fetchData();
    });

    return {
      mainData,
      loading,
      error,
      filterKey,
      filterOptions,
      selected,
    };
  },
  methods: {
    filterCustomers() {
      if (_.isEmpty(this.mainData)) return [];

      let data = _.cloneDeep(this.mainData);

      if (this.filterKey) {
        data = _.filter(
          this.mainData,
          (o) =>
            (o.name &&
              o.name.toLowerCase().includes(this.filterKey.toLowerCase())) ||
            (o.username &&
              o.username.toLowerCase().includes(this.filterKey.toLowerCase()))
        );
      }
      if (this.selected.value === 1) {
        return _.sortBy(data, (o) => o.name);
      } else if (this.selected.value === -1) {
        return _.sortBy(data, (o) => o.name).reverse();
      } else {
        return data;
      }
    },
    selectOption(option) {
      this.selected = option;
    },
  },
};
</script>

<style scoped>
.homepage {
  width: 100%;
  max-width: 1600px;
  margin: auto;
  height: 100%;
  padding: 150px 90px 60px;
  box-sizing: border-box;
  position: relative;
}
.filtering {
  width: 100%;
  display: flex;
  justify-content: space-between;
}
.filter-order {
  margin-right: 20px;
}
.data-container {
  margin-top: 40px;
  width: 100%;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}
.find-customer {
  display: flex;
  padding: 15px 20px;
  background: white;
  border-radius: 8px;
  align-items: center;
  margin-left: 20px;
}
.find-customer img {
  width: 20px;
  height: 20px;
}
.find-customer input {
  border: none;
  outline: none;
  background: transparent;
  margin-left: 10px;
  font-size: 16px;
  width: 400px;
  font-family: "Rubik";
}
@media (max-width: 960px) {
  .homepage {
    padding: 130px 32px 32px;
  }
  .data-container {
    margin-top: 30px;
  }
  .find-customer {
    margin-left: 10px;
  }
  .filter-order {
    margin-right: 10px;
  }
  .find-customer input {
    width: 300px;
  }
}
@media (max-width: 768px) {
  .find-customer {
    margin-left: 20px;
  }
  .filter-order {
    margin-right: 20px;
  }
  .data-container {
    margin-top: 20px;
  }
  .find-customer input {
    width: 200px;
  }
}
@media (max-width: 600px) {
  .homepage {
    padding: 100px 25px 25px;
  }
  .filtering {
    flex-direction: column;
    align-items: flex-end;
  }
  .data-container {
    margin-top: 25px;
  }
  .find-customer {
    width: 100%;
    box-sizing: border-box;
  }
  .filter-order {
    margin-right: 0px;
    margin-top: 20px;
  }
}
</style>
