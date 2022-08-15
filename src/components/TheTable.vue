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
            @click="(selected = index), (selectedModalTotal = index)"
            :class="selected === index ? 'is-green' : 'is-white'"
          >
            <td>
              {{ movie.movieName }}
            </td>
            <td>
              <ReviewInput v-model="movie.review" maxlength="15" />
            </td>
            <td>
              <ToDirectorInput v-model="movie.toDirector" maxlength="15" />
            </td>
            <td>
              <GradeInput v-model="movie.grade" type="number" max="5" min="0" />
            </td>
            <td>
              <img
                :src="movie.imageSrc"
                :alt="movie.movieName"
                :class="selected === index ? 'is-show' : 'is-hidden'"
                @click="showModalPoster(index)"
              />
              <!-- v-if, modal-poster -->
              <div
                class="modal-poster"
                :class="selectedModalPoster"
                v-if="
                  selectedModalPoster === index ? (isModalPoster = true) : null
                "
              >
                <img :src="movie.imageSrc" :alt="movie.movieName" />
                <div class="button-box">
                  <ModalPosterCloseButton
                    :isButton="false"
                    @click="selectedModalPoster = false"
                    message="Close"
                  />
                </div>
              </div>
            </td>
          </tr>
        </tbody>
      </table>
      <!-- v-if, modal-total -->
      <div class="modal-total" :class="selectedModalTotal" v-if="isModalTotal">
        <div
          v-for="(movie, index) in movieList"
          :key="movie.id"
          class="container"
          :class="selectedModalTotal === index ? 'is-show' : 'is-hidden'"
        >
          <h2>{{ movie.movieName }}</h2>
          <span>✧ Review : {{ movie.review }}</span>
          <span>✧ To Director : {{ movie.toDirector }}</span>
          <span>✧ Grade : {{ movie.grade }}</span>
          <img :src="movie.imageSrc" :alt="movie.movieName" />
          <div class="button-box">
            <ModalTotalCloseButton
              :isButton="false"
              @click="isModalTotal = false"
              message="Close"
              style="margin-top: 3rem"
            />
          </div>
        </div>
      </div>
      <div class="button-box">
        <SaveButton :isButton="true" message="Save" @click="onPrint" />
        <!-- isModalTotal = true -->
      </div>
    </div>
  </div>
</template>

<script>
import { reactive, ref } from "vue";
import minions2 from "../assets/minions2.jpg";
import hunt from "../assets/hunt.jpg";
import emergency_declaration from "../assets/emergency_declaration.jpg";
import appearance_of_dragon from "../assets/appearance_of_dragon.jpg";
import semantic_error_the_movie from "../assets/symantec_error_the_movie.jpg";
import ModalPosterCloseButton from "../components/DefaultButton.vue";
import SaveButton from "../components/DefaultButton.vue";
import ReviewInput from "../components/DefaultInput.vue";
import ToDirectorInput from "../components/DefaultInput.vue";
import GradeInput from "../components/DefaultInput.vue";
import ModalTotalCloseButton from "../components/DefaultButton.vue";

export default {
  components: {
    ModalPosterCloseButton,
    SaveButton,
    ReviewInput,
    ToDirectorInput,
    GradeInput,
    ModalTotalCloseButton,
  },
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
        review: "",
        toDirector: "",
        grade: "",
        imageSrc: minions2,
      },
      {
        id: 1,
        movieName: "Hunt",
        review: "",
        toDirector: "",
        grade: "",
        imageSrc: hunt,
      },
      {
        id: 2,
        movieName: "Emergency",
        review: "",
        toDirector: "",
        grade: "",
        imageSrc: emergency_declaration,
      },
      {
        id: 3,
        movieName: "Dragon's Rise",
        oneLineReview: "",
        toDirector: "",
        grade: "",
        imageSrc: appearance_of_dragon,
      },
      {
        id: 4,
        movieName: "Semantic Error",
        oneLineReview: "",
        toDirector: "",
        grade: "",
        imageSrc: semantic_error_the_movie,
      },
    ]);
    const selected = ref(null);
    const selectedModalPoster = ref(null);
    const isModalPoster = ref(false);
    const selectedModalTotal = ref(null);
    const isModalTotal = ref(false);

    const showModalPoster = (index) => {
      selectedModalPoster.value = index;
    };

    const onPrint = () => {
      movieList.forEach((movie) => {
        if (movie.id === selectedModalTotal.value) {
          if (
            movie.review === "" ||
            movie.toDirector === "" ||
            movie.grade === ""
          ) {
            alert("Please write it without any blanks");
          } else {
            isModalTotal.value = true;
          }
        }
      });
    };

    return {
      theadTitles,
      movieList,
      selected,
      selectedModalPoster,
      isModalPoster,
      showModalPoster,
      selectedModalTotal,
      isModalTotal,
      onPrint,
    };
  },
};
</script>

<style scoped>
.is-close {
  margin-top: 7.5rem;
  border: 2px solid #f8f8f5;
  background-color: rgb(243, 99, 99);
  color: #f8f8f5;
}
.is-save {
  border: 2px solid #f8f8f5;
  background-color: rgb(143, 143, 248);
  color: #f8f8f5;
}
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
  border: 2px solid #111101;
  border-radius: 5px;
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
  font-weight: 900;
  color: #fff;
}

tbody tr {
  background-color: #f8f8f5;
}

tbody tr td:first-child {
  font-weight: 900;
}

tbody tr td:last-child {
  padding: 0 1rem;
}

td img {
  width: 31px;
  height: 37px;
  border: 2px solid #f8f8f5;
  border-radius: 5px;
  cursor: zoom-in;
}
.modal-poster {
  position: fixed;
  top: 0;
  right: 0;
  left: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.5);
}
.modal-poster img {
  width: 340px;
  height: 520px;
  border: 2px solid #f8f8f5;
  border-radius: 5px;
  transform: translateY(20%);
  cursor: default;
}
.modal-total {
  position: fixed;
  top: 0;
  right: 0;
  left: 0;
  bottom: 0;
  padding: 5rem;
  background: rgba(0, 0, 0, 0.5);
}
.modal-total > .container {
  position: relative;
  width: 65%;
  margin-top: 2rem;
  padding: 2rem;
  border-radius: 5px;
  border: 5px solid #f8f8f5;
  background: #0f0f0d;
  color: #ffffff;
}
.modal-total > .container h2 {
  text-align: center;
  font-size: 2rem;
}
.modal-total > .container span {
  display: block;
  padding: 1rem;
  font-weight: 900;
  font-size: 1.2rem;
}
.modal-total > .container img {
  width: 260px;
  position: absolute;
  top: -50px;
  right: -100px;
  border: 2px solid #f8f8f5;
  border-radius: 5px;
}
.button-box {
  text-align: center;
}
</style>
