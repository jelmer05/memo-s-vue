<script setup>
import { ref } from "vue";

const showModal = ref(false);
const memo = ref("");
const newNode = ref([]);
const errorMsg = ref("");

function generateRandomBackground() {
  var color =
    "rgb(" +
    Math.floor(Math.random() * 256) +
    "," +
    Math.floor(Math.random() * 256) +
    "," +
    Math.floor(Math.random() * 256) +
    ")";
  return color;
}

const addMemo = () => {
  if (memo.value.length < 10) {
    return (errorMsg.value = "Minimaal 10 tekens");
  }
  newNode.value.push({
    id: Math.floor(Math.random() * 1000000),
    text: memo.value,
    date: new Date(),
    background: generateRandomBackground(),
  });
  memo.value = "";
  showModal.value = false;
  errorMsg.value = "";
};
</script>
<template>
  <main>
    <div v-if="showModal" class="overlay">
      <div class="modal">
        <textarea
          v-model.trim="memo"
          name="memo
        "
          id=""
          cols="30"
          rows="10"
        ></textarea>
        <p v-if="errorMsg" style="color: red">{{ errorMsg }}</p>
        <div class="btn btn-warning" @click="addMemo">voeg memo</div>
        <div class="btn btn-secondary" @click="showModal = false">close</div>
      </div>
    </div>
    <div class="container">
      <header>
        <div class="row justify-content-between">
          <div class="col-md-4">
            <h1 class="">
              berichten
              <a href="https://jelmervanderveen.nl"></a>jelmervanderveen.nl
            </h1>
          </div>
          <div class="col-md-3">
            <button class="btn btn-lg btn-success" @click="showModal = true">
              +
            </button>
          </div>
        </div>
      </header>
      <div class="card-container">
        <div
          v-for="Node in newNode"
          class="card-memo"
          :key="Node.id"
          :style="{ backgroundColor: Node.background }"
        >
          <p class="main-text">{{ Node.text }}</p>
          <p class="date">
            {{ Node.date.toLocaleDateString("en-Us") }}
          </p>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
main {
  position: relative;
  height: 100vh;
  width: 100vw;
}
header {
  height: 100px;
  display: flex;
  align-items: center;
}
.row {
  width: 100%;
}
h1 {
  text-transform: capitalize;
  font-weight: bold;
}
.card-container {
  margin-top: 30px;
  display: flex;
  flex-wrap: wrap;
}
.card-memo {
  border-radius: 22px;
  width: 225px;
  height: 225px;
  background: white;
  display: flex;
  justify-content: space-around;
  padding: 10px;
  margin-bottom: 20px;
  margin-right: 20px;

  /* text-align: center; */

  flex-direction: column;
  color: black;
}

.overlay {
  position: absolute;
  width: 100%;
  height: 100%;
  background: rgba(186, 186, 186, 0.52);

  z-index: 1;
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal {
  z-index: 2;
  position: relative;
  display: flex;
  flex-direction: column;
  width: 750px;
  height: auto;
  border-radius: 11px;
  background: white;
  opacity: 1;
  justify-content: center;
}
</style>
