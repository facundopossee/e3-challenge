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
    //METODO QUE CALCULA RECURSIVAMENTE EL MAXIMO COMUN DIVISOR, AL RECIBIR DOS VALORES    
    gcd(a, b) {
      if (b == 0) return a;
      else return this.gcd(b, a % b);
    },
  },
  watch: {
    //METODO QUE SE ACCIONA CUANDO LA VARIABLE 'FRACTION' BINDEADA AL INPUT CAMBIA SU VALOR
    fraction: function () {
      //al recibir la variable 'fraction', se comprueba que tenga el formato de una fraccion
      let a = /^[0-9]{1,}\/[0-9]{1,}$/.test(this.fraction);
      if (a == false) {
        //si no es una fraccion simplemente muestra un mensaje
        this.fractionresult = "not a fraction";
      } else {
        //en el caso de ser una fraccion, se envian tanto el numerador como el denominador al metodo 'gcd' escrito mas arriba (linea 42)
        let arr = this.fraction.split("/", 2);
        let div = this.gcd(arr[0], arr[1]);
        //se simplifica la fraccion dividiendo ambas partes de la fraccion por el valor del metodo 'gcd' y se asigna a la variable 'fractionresult' para mostrarlo
        this.fractionresult = arr[0] / div + "/" + arr[1] / div;
      }
    },
    //METODO QUE SE ACCIONA CUANDO LA VARIABLE 'NAME' BINDEADA AL INPUT CAMBIA SU VALOR
    name: function () {
      //se testea el string ingresado comparandolo con el regex definido para el caso
      let a = /^([A-Z][a-z]{2,}( [A-Z][a-z]{2,}( [A-Z][a-z]{2,})?| [A-Z]\.( [A-Z][a-z]{2,})?)|([A-Z]\.( [A-Z][a-z]{2,}))|[A-Z]\.( [A-Z]\.)( [A-Z][a-z]{2,}))$/.test(
        this.name
      );
      //se asigna el valor booleano resultante del test anterior a la variable 'nameresult'
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
