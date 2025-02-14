
<template>
    <Teleport to="body">
      <transition name="fade">
        <div v-if="visible" :class="['notification', typeClass]">
          <button class="delete" @click="close">Uus teade!</button>
          <div class="content">
            <slot></slot>
          </div>
        </div>
      </transition>
    </Teleport>
  </template>
  
  <script setup>
  import { ref, computed, onMounted } from 'vue';
  
  const props = defineProps({
    type: {
      type: String,
      default: 'is-info',
    },
    duration: {
      type: Number,
      default: 3000,
    },
  });
  
  const visible = ref(false);
  const typeClass = computed(() => `notification ${props.type}`);
  
  const show = () => {
    visible.value = true;
    if (props.duration > 0) {
      setTimeout(close, props.duration);
    }
  };
  
  const close = () => {
    visible.value = false;
  };
  
  onMounted(show);
  </script>
  
  <style scoped>
  .notification {
    position: fixed;
    top: 20px;
    right: 20px;
    max-width: 350px;
    padding: 15px;
    border-radius: 5px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    z-index: 1000;
    display: flex;
    align-items: center;
    background-color: white;
    border-left: 5px solid;
  }
  
  .notification.is-info {
    border-color: #209cee;
    background-color: #eff6ff;
    color: #209cee;
  }
  
  .notification.is-success {
    border-color: #23d160;
    background-color: #f0fff4;
    color: #23d160;
  }
  
  .notification.is-warning {
    border-color: #ffdd57;
    background-color: #fffbe6;
    color: #ffdd57;
  }
  
  .notification.is-danger {
    border-color: #ff3860;
    background-color: #fff5f7;
    color: #ff3860;
  }
  
  .content {
    flex: 1;
    font-size: 16px;
  }
  
  .delete {
    background: none;
    border: none;
    cursor: pointer;
    font-size: 20px;
    color: #333;
  }
  
  .fade-enter-active, .fade-leave-active {
    transition: opacity 0.5s, transform 0.3s ease-out;
  }
  .fade-enter, .fade-leave-to {
    opacity: 0;
    transform: translateY(-10px);
  }
  </style>