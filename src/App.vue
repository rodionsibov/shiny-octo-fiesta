<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
</script>

<template>
  <form data-multi-step>
    <div data-step="1" class="card">
      <div class="form-group">
        <label for="email">Email</label>
        <input type="email" name="email" id="email">
      </div>
      <div class="form-group">
        <label for="password">Password</label>
        <input type="password" name="password" id="password">
      </div>
      <button type="button">Next</button>
    </div>
    <div data-step="2" class="card"></div>
    <div data-step="3" class="card">
      <button class="btn-primary" type="submit">Submit</button>
    </div>
  </form>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
