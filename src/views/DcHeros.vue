<template>
  <h2 class="w-full text-4xl mb-10 font-bold text-secondary text-center">
    DC Heros ({{ totalHero }})
  </h2>
  <div class="w-full">
    <form
      @submit.prevent="addHero"
      class="flex max-w-sm mx-auto space-x-3 mb-10"
    >
      <input
        autofocus
        v-model="newHero"
        class="flex-1 appearance-none border border-transparent w-full py-2 px-4 bg-white text-gray-700 placeholder-gray-400 shadow-md rounded-sm text-base focus:outline-none focus:ring-2 focus:ring-primary focus:border-transparent"
        type="text"
        placeholder="New Hero"
      />
      <button
        class="flex-shrink-0 bg-primary text-white text-sm uppercase font-semibold py-2 px-4 rounded-sm shadow-md hover:bg-primary hover:bg-opacity-80 focus:outline-none focus:ring-2 focus:ring-primary focus:ring-offset-2 focus:ring-offset-purple-200"
        type="button"
      >
        add
      </button>
    </form>
  </div>
  <div class="block">
    <div
      class="transition-all flex justify-between items-center group px-6 py-5 max-w-full mx-auto w-72 border border-primary border-opacity-25 cursor-pointer rounded select-none overflow-hidden space-y-1 hover:bg-white shadow-lg hover:border-transparent my-2"
      v-for="(hero, index) in dcHeros"
      :key="hero.name"
    >
      <p class="font-semibold text-lg text-primary group-hover:text-gray-900">
        {{ hero.name }}
      </p>
      <button
        @click="removeHero(index)"
        class="bg-primary text-white text-sm font-semibold p-2 px-3 rounded-full shadow-md hover:bg-primary hover:bg-opacity-80 focus:outline-none focus:ring-2 focus:ring-primary focus:ring-offset-2 focus:ring-offset-purple-200 material-icons"
      >
        close
      </button>
    </div>
  </div>
</template>

<script>
import { computed, ref } from "vue";

export default {
  setup() {
    const newHero = ref(null);
    const dcHeros = ref([{ name: "Super Man" }]);

    const totalHero = computed({
      get: () => dcHeros.value.length,
    });

    const addHero = () => {
      if (newHero.value) {
        dcHeros.value.unshift({ name: newHero.value });
        newHero.value = null;
      } else {
        alert("Insert name");
      }
    };

    const removeHero = (index) => {
      dcHeros.value = dcHeros.value.filter((hero, i) => i !== index);
    };

    return { newHero, dcHeros, totalHero, addHero, removeHero };
  },
};
</script>
