<script setup>
import { ref } from 'vue';

const props = defineProps({
  type: {
    type: String,
    default: 'is-info',
  },
  duration: {
    type: Number,
    default: 5000,
  },
});

const visible = ref(false);

const show = () => {
  visible.value = true;
  if (props.duration > 0) {
    setTimeout(() => {
      visible.value = false;
    }, props.duration);
  }
};

const close = () => {
  visible.value = false;
};
</script>

<template>
  <div class="container mt-2">
    <button class="button is-primary" @click="show">Show Notification</button>
    
    <transition name="fade">
      <div v-if="visible" :class="['notification', type]">
        <button class="delete" @click="close"></button>
        <p>
          Lorem ipsum dolor sit amet, consectetur adipiscing elit lorem ipsum dolor.
          <strong>Pellentesque risus mi</strong>, tempus quis placerat ut, porta nec
          nulla. Vestibulum rhoncus ac ex sit amet fringilla. Nullam gravida purus diam,
          et dictum <a href="#">felis venenatis</a> efficitur.
        </p>
      </div>
    </transition>
  </div>
</template>