<script setup>
import { computed, ref, onMounted } from 'vue';

const props = defineProps({
  message: {
    type: String,
    required: true
  },
  color: {
    type: String,
    required: false,
    validator(value) {
      return [
        'primary',
        'link',
        'info',
        'success',
        'warning',
        'danger',
        'white',
        'light',
        'dark'
      ].includes(value);
    }
  },
  light: Boolean,
  duration: {
    type: Number,
    default: 3000
  }
});

const visible = ref(false);
const typeClass = computed(() => {
  let classes = ['notification'];
  if (props.color) classes.push(`is-${props.color}`);
  if (props.light) classes.push('is-light');
  return classes.join(' ');
});

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

onMounted(show);
</script>

<template>
  <transition name="fade">
    <div v-if="visible" :class="typeClass">
      <button class="delete" @click="close"></button>
      <slot>{{ message }}</slot>
    </div>
  </transition>
</template>
