<template>
  <div class="fondoimg">
    <div>
      <h1 class="titulo">{{ info.title }}</h1>
      <p class="year">{{ info.year }}</p>
      <p class="text">
        Hola, Bienvenido en este pagina<br />
        podras interactuar con diferentes<br />
        estilos de commics, Ademas de ello <br />
        podras dar una calificación de 1 a 5, <br />dependiento que tanto te
        gusto. <br />
        siendo 1 la calificación mas baja <br />
        y 5 la calificación mas alta,<br />
        esperamos te diviertas.
      </p>
      <img class="img" v-bind:src="info.img" v-bind:alt="info.alt" />
      <div>
        <star-rating v-model="rating"></star-rating>
      </div>
      <button class="rate" @click="rate">Calificar</button>
    </div>
  </div>
</template>

<script>
import StarRating from "vue-star-rating";
import axios from "axios";
export default {
  components: {
    StarRating,
  },
  name: "Cartoon",
  props: {
    msg: String,
  },
  data() {
    return {
      info: [],
      rating: 0,
    };
  },

  mounted() {
    console.log("entrando");
    this.getCartoon();
  },

  methods: {
    getRamdom(min = 1, max = 2466) {
      return parseInt(Math.random() * (max - min) + min);
    },
    getCartoon() {
      let number = this.getRamdom();
      let baseUrl = "http://localhost:8080/";
      //let baseUrl='https://xkcd.com/';
      let url = baseUrl + number + "/info.0.json";
      axios.get(url).then((response) => {
        console.log(response);
        this.info = response.data;
      });
    },
    rate() {
      if (this.rating != 0) {
        this.$toast.open(
          "has calificado: " + this.rating + " Gracias por tu Calificación "
        );
        this.getCartoon();
        this.rating = 0;
      } else {
        this.$toast.open({
          message: "Elija una Calificación correcta",
          type: "error",
        });
      }
    },
  },
};
</script>

<style scoped>
.background {
  background-color: #767b7f;
}
.titulo {
  font-style: bold;
  color: black;
  font-weight: 900;
}
.img {
  margin-bottom: 8px;
}
.vue-star-rating {
  width: 14%;
  margin-left: auto;
  margin-right: auto;
  margin-bottom: 30px;
  margin-top: 21px;
}

.rate {
  font-size: 26px;
  background: red;
  border-radius: 38px;
  width: 142px;
  font-weight: 600;
  cursor: pointer;
  margin: 10px;
  color: white;
  font-style: bold;
}

.year {
  color: black;
  font-weight: 900;
  font-style: bold;
}

.fondoimg {
  background-image: url("https://thumbs.dreamstime.com/z/fondo-de-la-turquesa-p%C3%A1gina-del-c%C3%B3mic-120800082.jpg");
}

.text {
  color: black;
  font-weight: bolder;
  text-align: justify;
  text-align: center;
  font-style: italic;
}
</style>