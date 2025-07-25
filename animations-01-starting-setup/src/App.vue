<template>
  <div class="container">
    <div class="block" :class="{animate: animatedBlock}"></div>
    <button @click="animateBlock">Animate</button>
  </div>
    <div class="container">
    <transition name="user-button" mode="out-in">
    <button @click="showUsers" v-if="!usersVisible">Show Users</button>
    <button @click="hideUsers" v-else>Hide Users</button>
    </transition>
  </div>
  <div class="container">
    <list-data></list-data>
  </div>

  <div class="container">
    <transition
      :css="false"
      @before-enter = "beforeEnter"
      @enter = "enter"
      @after-enter = "afterEnter"
      @before-leave = "beforeLeave"
      @leave = "leave"
      @after-leave = "afterLeave"
      @enter-cancelled = "enterCancelled"
      @leave-cancelled = "leaveCancelled"
    >
    <p v-if="parIsVis">You're Gay</p>
    </transition>
    <button @click="showPar">Click me</button>
  </div>
  <base-modal @close="hideDialog" :open="dialogIsVisible">
    <p>This is a test dialog!</p>
    <button @click="hideDialog">Close it!</button>
  </base-modal>
  <div class="container">
    <button @click="showDialog">Show Dialog</button>
  </div>
</template>  

<script>
import ListData from "./components/ListData";
export default {
  components: {
    ListData
  },
  data() {
    return {
      animatedBlock: false,
      dialogIsVisible: false,
      parIsVis: false,
      usersVisible: false,
      enterInterval: null,
      leaveInterval: null,
    };
  },
  methods: {
    enterCancelled(el) {
      clearInterval(this.enterInterval);
      console.log(el);
    },
    leaveCancelled(el) {
      clearInterval(this.leaveInterval);
      console.log(el);
      },
    beforeEnter(el) {
      el.style.opacity = 0;
    },
    enter(el, done) {
      let round = 0;
      this.enterInterval = setInterval(() => {
        el.style.opacity = round;
        round += 0.1;
        if (round > 1) {
          clearInterval(this.enterInterval);
          done();
        }
      }, 20)
    },

    afterEnter(el) {},

    beforeLeave(el) {
      el.style.opacity = 1;
    },
    leave(el, done) {
      let round = 1;
      this.leaveInterval = setInterval(() => {
        el.style.opacity = round;
        round -= 0.1;
        if (round < 0) {
          clearInterval(this.leaveInterval);
          done();
        }
      }, 20)
    },
    afterLeave(el) {},
    showDialog() {
      this.dialogIsVisible = true;
    },
    hideDialog() {
      this.dialogIsVisible = false;
    },
    animateBlock() {
      this.animatedBlock = true;
    },
    showPar() {
      this.parIsVis = !this.parIsVis;
    },
    showUsers() {
      this.usersVisible = true;
    },
    hideUsers() {
      this.usersVisible = false;
    }
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}
html {
  font-family: sans-serif;
}
body {
  margin: 0;
}
button {
  font: inherit;
  padding: 0.5rem 2rem;
  border: 1px solid #810032;
  border-radius: 30px;
  background-color: #810032;
  color: white;
  cursor: pointer;
}
button:hover,
button:active {
  background-color: #a80b48;
  border-color: #a80b48;
}
.block {
  width: 8rem;
  height: 8rem;
  background-color: #290033;
  margin-bottom: 2rem;
}
.container {
  max-width: 40rem;
  margin: 2rem auto;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 2rem;
  border: 2px solid #ccc;
  border-radius: 12px;
}

.animate {
  animation: slidey-boy 2s ease-in-out forwards;
}

@keyframes slidey-boy {
  0% {
    opacity: 100%;
    transform: translateX(0) scale(1);
  }
  50%{
    opacity: 50%;
    transform: scale(1.2);
  }
  100%{
  opacity: 0;
  transform: translateX(120px) scale(1);
  }
}

.user-button-enter-active {
  animation: button-boy 0.5s ease-in-out forwards;
}

.user-button-leave-active {
  animation: button-boy 0.5s ease-in-out reverse;
}
@keyframes button-boy {
  from {
    opacity: 0;
  }

  to {
    opacity: 1;
  }
}
</style>