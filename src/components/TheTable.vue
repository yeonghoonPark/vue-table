<template>
  <div class="desk">
    <div class="container">
      <table class="table">
        <thead>
          <tr>
            <th v-for="theadTitle in theadTitles" :key="theadTitle.id">
              {{ theadTitle.title }}
            </th>
          </tr>
        </thead>
        <tbody>
          <tr
            v-for="(movie, index) in movieList"
            :key="movie.id"
            @click="selected = index"
            :class="selected === index ? 'is-green' : 'is-white'"
          >
            <td>
              {{ movie.movieName }}
            </td>
            <td>
              <input type="text" />
            </td>
            <td>
              <input type="text" />
            </td>
            <td>
              <input type="text" />
            </td>
            <td>
              <img
                :src="movie.imageSrc"
                :alt="movie.movieName"
                :class="selected === index ? 'is-show' : 'is-hidden'"
              />
              <div class="modal-poster" v-if="isPoster">
                <img :src="movie.imageSrc" :alt="movie.movieName" />
              </div>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import { reactive, ref } from "vue";
import minions2 from "../assets/minions2.jpg";
import hunt from "../assets/hunt.jpg";
import emergency_declaration from "../assets/emergency_declaration.jpg";
import { computed } from "@vue/reactivity";

export default {
  setup() {
    const theadTitles = reactive([
      { id: 0, title: "Ttile" },
      { id: 1, title: "Review" },
      { id: 2, title: "To Director" },
      { id: 3, title: "Grade" },
      { id: 4, title: "Poster" },
    ]);

    const movieList = reactive([
      {
        id: 0,
        movieName: "Minions2",
        imageSrc: minions2,
      },
      {
        id: 1,
        movieName: "Hunt",
        imageSrc: hunt,
      },
      {
        id: 2,
        movieName: "Emergency",
        imageSrc: emergency_declaration,
      },
    ]);

    const selected = ref(null);

    const isPoster = ref(false);

    return {
      theadTitles,
      movieList,
      selected,

      isPoster,
    };
  },
};
</script>

<style scoped>
.is-green {
  background-color: #3dc07433;
}

.is-white {
  background-color: #f8f8f5;
}
.is-show {
  margin: 0 auto;
  display: block;
}
.is-hidden {
  display: none;
}
.desk {
  width: 100%;
  margin: 88px auto 0;
}

.container {
  padding: 5rem;
}

table {
  width: 100%;
  border: 1px solid #111101;
  text-align: center;
}

thead tr th,
tbody tr td {
  padding: 1rem;
}

thead {
  background-color: #111101;
}

thead th {
  color: #fff;
}

tbody tr {
  background-color: #f8f8f5;
}

tbody tr td:first-child {
  font-weight: 600;
}

tbody tr td:last-child {
  padding: 0 1rem;
}

td img {
  width: 31px;
  height: 37px;
  cursor: zoom-in;
}

.modal-poster {
  position: fixed;
  top: 0;
  right: 0;
  left: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.9);
}

.modal-poster img {
  width: 340px;
  height: 520px;
  transform: translateY(20%);
}
</style>
