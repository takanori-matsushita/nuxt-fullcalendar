<template>
  <div class="container">
    <client-only>
      <full-calendar />
    </client-only>
  </div>
</template>

<script>
export default {}
</script>

<style>
/* Sample `apply` at-rules with Tailwind CSS */
.container {
  @apply mt-10 mx-auto;
}
</style>
