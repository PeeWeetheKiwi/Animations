<template>
    <transition-group tag="ul" name="animal-list">
      <li v-for="animal in animals" :key="animal" @click="removeAnimal(animal)"> {{ animal }}</li>
    </transition-group>
  <div>
    <input type="text" ref="animalNameInput"/>
    <button @click="addAnimal()">Add Animal</button>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      animals: ['Dog', 'Cat', 'Jaguar', 'Parrot']
    }
  },
  methods: {
    removeAnimal(animal) {
      this.animals = this.animals.filter(a => a !== animal);
    },
    addAnimal() {
      const enteredAnimal = this.$refs.animalNameInput.value;
      this.animals.unshift(enteredAnimal);
    }
  }
}
</script>

<style scoped>
ul {
  list-style: none;
  margin: 1rem 0;
  padding: 0;
}
li {
  border: 1px solid black;
  padding: 1rem;
  text-align: center;
}

.animal-list-enter-active {
  animation: animal-boy 0.7s ease-out forwards;
}

.animal-list-leave-active {
  animation: animal-boy 0.7s ease-in-out reverse;
}

@keyframes animal-boy {
  from {
    opacity: 0;
    transform: scale(0.8);
  }
  to {
    opacity: 1;
    transform: scale(1);
  }
}

.animal-list-move {
  transition:transform 0.5s ease;
}
</style>