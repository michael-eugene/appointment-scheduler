<script setup>
const user = useSupabaseUser();
</script>
<template>
  <div class="mx-auto flex flex-col p-4 text-center justify-between">
    <p class="font-bold text-left">Booking Summary</p>
    <div></div>
    <div class="flex justify-between">
      <p>Total</p>
      <p>$10</p>
    </div>
  </div>
</template>

<style scoped></style>
