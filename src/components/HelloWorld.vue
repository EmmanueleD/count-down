<template>
  <div class="hello">
    <div class="container">
      <div class="item">
        <div class="number">{{ days }}</div>
        <div class="label">{{ daysLab }}</div>
      </div>
      <div class="item">
        <div class="number">{{ hours }}</div>
        <div class="label">{{ hoursLab }}</div>
      </div>
      <div class="item">
        <div class="number">{{ minutes }}</div>
        <div class="label">{{ minutesLab }}</div>
      </div>
      <div class="item">
        <div class="number">{{ seconds }}</div>
        <div class="label">{{ secondsLab }}</div>
      </div>
    </div>
    <div class="links">
      <router-link tag="li" class="nav-link" to="/">From Orlando</router-link>
      <router-link tag="li" class="nav-link" to="/or">From Forlì</router-link>
    </div>
  </div>
</template>

<script>
import { differenceInSeconds } from "date-fns";
export default {
  name: "HelloWorld",
  data() {
    return {
      interval: null,
      days: 0,
      hours: 0,
      minutes: 0,
      seconds: 0,
      daysLab: "Giorni",
      hoursLab: "Ore",
      minutesLab: "Minuti",
      secondsLab: "Secondi",
      finish: "",
    };
  },
  created() {
    this.finish = new Date(2021, 11, 7, 16, 20, 0, 0);
  },
  mounted() {
    setInterval(() => {
      this.interval = differenceInSeconds(this.finish, new Date());

      this.days = Math.floor(this.interval / 86400);
      this.hours = Math.floor((this.interval - this.days * 86400) / 3600);
      this.minutes = Math.floor(
        (this.interval - this.days * 86400 - this.hours * 3600) / 60
      );
      this.seconds = Math.floor(
        this.interval -
          this.days * 86400 -
          this.hours * 3600 -
          this.minutes * 60
      );
    }, 1000);
  },
  methods: {
    setDateToOrlando() {
      this.finish = new Date(2021, 11, 7, 10, 20, 0, 0);
    },
    setDateToForli() {
      this.finish = new Date(2021, 11, 7, 16, 20, 0, 0);
    },
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Bebas+Neue&display=swap");
.hello {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  font-family: "Bebas Neue", cursive;
  color: white;
  background: url("../assets/noidue.jpg");
  background-position: center;
  background-size: cover;
}

.container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  width: 100vw;
  height: auto;
}

.item {
  padding: 5rem;
  align-self: center;
  min-width: 200px;
  flex-grow: 2;
  text-shadow: 0 0 2px #fff;
}

.number,
.label {
  display: grid;
  place-items: center;
}

.number {
  font-size: 10rem;
}

.label {
  font-size: 5rem;
}

.links {
  width: 30%;
  display: flex;
  justify-content: space-around;
}

a.nav-link {
  color: white;
  font-size: 1.5rem;
  text-decoration: none;
}

a.router-link-active {
  text-decoration: underline;
  color: white;
}

@media only screen and (max-width: 414px) {
  .item {
    padding: 0px;
    min-width: 0px;
  }

  .number {
    font-size: 5rem;
  }

  .label {
    font-size: 2rem;
  }
}
</style>
