<template>
  <div id="app">
    <div class="container">
      <div>
        <h3>Fractions validator</h3>
        <input type="text" placeholder="enter a fraction" v-model="fraction" />
        <p>{{ this.fractionresult }}</p>
      </div>
      <br />
      <div>
        <h3>Names validator</h3>
        <input type="text" placeholder="enter a name" v-model="name" />
        <p>{{ this.nameresult }}</p>
      </div>
    </div>
    <div class="text">
      <h5>
        This website was developed for an E3 Ecommerce technical exam by
        <a href="https://facundoposse.vercel.app/">Facundo Posse</a>
      </h5>
      <h5>
        Clone the repository on
        <a href="https://github.com/facundopossee/e3-challenge">Github</a>
      </h5>
    </div>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      name: "",
      fraction: "",
      nameresult: false,
      fractionresult: "",
    };
  },
  methods: {
    gcd(a, b) {
      var aux;
      var i1 = Math.max(a, b);
      var i2 = Math.min(a, b);
      do {
        aux = i2;
        i2 = i1 % i2;
        i1 = aux;
      } while (i2 !== 0);
      return i1;
    },
  },
  watch: {
    fraction: function () {
      let a = /^[0-9]{1,}\/[0-9]{1,}$/.test(this.fraction);
      if (a == false) {
        this.fractionresult = "not a fraction";
      } else {
        let arr = this.fraction.split("/", 2);
        let div = this.gcd(arr[0], arr[1]);

        this.fractionresult = arr[0] / div + "/" + arr[1] / div;
      }
    },
    name: function () {
      let a = /^([A-Z][a-z]{2,}( [A-Z][a-z]{2,}( [A-Z][a-z]{2,})?| [A-Z]\.( [A-Z][a-z]{2,})?)|([A-Z]\.( [A-Z][a-z]{2,}))|[A-Z]\.( [A-Z]\.)( [A-Z][a-z]{2,}))$/.test(
        this.name
      );
      this.nameresult = a;
    },
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 30vh;
}
.container {
  margin: 0 auto;
}
.text {
  padding-top: 20px;
}
</style>
