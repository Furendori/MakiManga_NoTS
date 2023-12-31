<script setup lang="ts">
import { onMounted, ref } from "vue";
import type { MangaInterface } from "@/interfaces/MangaInterface";

const mangas = ref<MangaInterface[]>([]);
const isLoading = ref(true);


const getMangas = async () => {

  const response = await fetch("http://localhost:5500/mangas/", {
        method: "GET",
        headers: {
          "Content-Type": "application/json",
        },
      })
      mangas.value = await response.json();

  isLoading.value = false;
};

onMounted(() => {
  getMangas();
});
</script>

<template>
  <h2>Les licences</h2>
  <div class="main-container">
    <div class="manga-card" v-for="manga in mangas">
      <div class="manga-img">
        <img :src="manga.image" alt=""/>
      </div>
      <div class="manga-name">
        <p>{{ manga.nameFR }}</p>
        <p>{{ manga.nameJP }}</p>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
.main-container {
  display: flex;
  flex-wrap: wrap;
  .manga-card {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 380px;
    width: 250px;
    .manga-img {
      margin: auto;
      height: 280px;
      width: 180px;
      box-shadow: 10px 5px 5px $primary-color;
      
      img {
        height: 280px;
        width: 180px;
        object-fit: cover;
        transition: 0.3s;

        &:hover {
          transform: scale(1.1);
          cursor: pointer;
        }
      }
    }
    .manga-name {
      margin: auto;

      p{
        margin: 0;
      }
    }
  }
}
</style>