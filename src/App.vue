<script setup>
  import MainLayout from "./layouts/MainLayout.vue";
  import Card from "./components/Card.vue";
  import {ref} from "vue";

  const isFlipped = ref(false);
  const isSelected = ref(false);
  const isOpenAll = ref(false);

  async function openCard(cardId) {
    flipCard();
    moveCard();
  }

  function moveCard(el) {
    isSelected.value = true;
  }

  function flipCard(el) {
    isFlipped.value = true;
  }
</script>

<template>
  <div>

  </div>
  <MainLayout>
    <div class="flex flex-col h-full items-center">
      <div class="h-1/2">

      </div>
      <div class="flex gap-5">
        <Card
            suit="Diamonds"
            rank="10"
            :is-flipped="isOpenAll"
        />
        <Card
            class="duration-1000"
            :class="{'-translate-y-64': isSelected, 'delay-1000': isFlipped}"
            suit="Hearts"
            rank="10"
            :is-flipped="isFlipped"
        />
        <Card
            suit="Diamonds"
            rank="K"
            :is-flipped="isOpenAll"
        />
      </div>
      <div class="w-full mt-5">
        <button :disabled="isFlipped" class="bg-blue-600 hover:bg-blue-700 transition-all border-none outline-0 ring-0 disabled:bg-gray-300 disabled:cursor-not-allowed" @click="openCard">
          Flip
        </button>
      </div>
      <div class="w-full mt-5" v-show="isFlipped">
        <button class="bg-blue-600 hover:bg-blue-700 transition-all border-none outline-0 ring-0" @click="isOpenAll = !isOpenAll;">
         {{ isOpenAll ? 'Hide' : 'Show All' }}
        </button>
      </div>
      <div class="absolute top-0 right-0 m-5">
        <button
            :disabled="!isSelected && !isFlipped"
            class="bg-blue-600 hover:bg-blue-700 transition-all border-none outline-0 ring-0 disabled:bg-gray-300 disabled:cursor-not-allowed"
            @click="isFlipped = false; isSelected = false; isOpenAll = false;"
        >
          <span>&#x21bb;</span>
        </button>
      </div>
    </div>

  </MainLayout>
</template>

<style scoped>

</style>
