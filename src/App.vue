<template>
  <div>
    <div class="container">
      <h2>hello</h2>

      <div class="form-group">
        <label for="name">Name</label>
        <input
          type="text"
          v-model.trim="carName"
          id="name"
          class="form-control"
        />
      </div>
      <div class="form-group">
        <label for="year">Year</label>
        <input
          type="text"
          id="year"
          v-model.number="year"
          class="form-control"
        />
      </div>
      <button class="btn btn-success" @click="createCar">
        Create Car
      </button>
      <button class="btn btn-primary ml-3" @click="loadCars">Load Cars</button>
      <hr />
      <ul class="list-group">
        <li class="list-group-item" v-for="(item, k) in cars" :key="k">
          <strong>{{ item.carName }}</strong> - {{ item.year }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      carName: "",
      year: 2013,
      cars: [],
      resource: null
    };
  },
  methods: {
    createCar() {
      const car = {
        carName: this.carName,
        year: this.year
      };
      // this.$http.post("http://localhost:3000/cars", car).then(response => {
      //   return response.json().then(newCar => {
      //     console.log(newCar);
      //   });
      // });

      this.resource.save({}, car);
    },
    loadCars() {
      // this.$http.get("http://localhost:3000/cars").then(response => {
      //   response.json().then(cars => {
      //     this.cars = cars;
      //   });
      // });
      this.resource
        .get()
        .then(response => response.json().then(cars => (this.cars = cars)));
    }
  },
  created() {
    this.resource = this.$resource("cars");
  }
};
</script>
