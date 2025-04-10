<template>
  <div >
    <div class="spinner"></div>
  </div>
</template>


<style scoped>

.spinner {
  border: 6px solid rgba(255, 255, 255, 0.5); 
  border-top-color: var(--custom-color); 
  border-radius: 50%;
  width: 70px;
  height: 70px;
  animation: spin 1s linear infinite;
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>