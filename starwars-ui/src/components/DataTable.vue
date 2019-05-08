<template>
  <div class="container">
    <div class="row">
      <div class="col-12 mt-3 mb-3 d-flex justify-content-center">
        <img
        src="https://upload.wikimedia.org/wikipedia/commons/thumb/6/6c/Star_Wars_Logo.svg/1280px-Star_Wars_Logo.svg.png" alt="Star Wars Logo"
        width="280"
        height="140"
        >
      </div>
      <div class="col-12 mt-3 mb-5">
        <input class="form-control"
          type="number"
          name="distanceMLGT"
          id="distanceMLGT"
          v-model="distanceMGLT"
          @input="calculateTurnsMGLT"
        >
      </div>
      <div class="col-12 mb-5 table-responsive">
        <table class="table table-striped table-dark">
          <thead>
            <tr>
              <th scope="col">ID</th>
              <th scope="col">Starship</th>
              <th scope="col">Model</th>
              <th scope="col">Length</th>
              <th scope="col">Cost in Credits</th>
              <th scope="col">MGLT</th>
              <th scope="col">MGLT in Turns</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(item,index) in starships" :key="index">
              <td>{{ `#${index + 1}` }}</td>
              <td>{{ item.name }}</td>
              <td>{{ item.model }}</td>
              <td>{{ item.length }}</td>
              <td>{{ item.cost_in_credits }}</td>
              <td>{{ item.MGLT }}</td>
              <td>{{ turns[index] }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      starships: [],
      turns: [],
      distanceMGLT: '',
    };
  },
  methods: {
    getStarShips() {
      axios
        .post(`${process.env.API_URL}starships`)
        .then((res) => { this.starships = res.data.results; })
        /* eslint-disable no-console */
        .catch((error) => { console.error(error); });
    },
    calculateTurnsMGLT() {
      this.turns = [];
      this.starships.forEach((index) => {
        let calculateTurns = this.distanceMGLT / index.MGLT;
        if (calculateTurns < 1) {
          calculateTurns = '<1';
        } else {
          calculateTurns = Math.round(calculateTurns);
        }
        this.turns.push(calculateTurns);
      });
    },
  },
  mounted() {
    this.getStarShips();
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
@import '../assets/styles/app';
</style>
