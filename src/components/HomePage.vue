<template>
  <img class="midImg" src="../../public/assets/logo.png">
  <h1> barlow robotics </h1>
  <h2 style="font-weight: normal; color: greenyellow">scouting forms</h2>
  <ul v-if="list.length> 0" class="link-list">
    <li v-for="[i, name] of list.entries()" :key="i">
      <RouterLink :to="{ name: 'form', query: { name } }">{{ name }}</RouterLink>
    </li>
    <a href="https://forms.gle/uQfcvyEHe5YXpvrC6">pits</a>
  </ul>
  <p v-else>No configurations specified.</p>
  <h2 style="font-weight: normal; color: greenyellow">tools</h2>
  <ul class="link-list">
    <li>
      <RouterLink :to="{ name: 'inspector' }">data inspector</RouterLink>
    </li>
    <a href="https://docs.google.com/spreadsheets/d/1_PW__91LF_RVu54R96Nv3QEjM69gSNrZ0f1spxHtRjI/edit?usp=sharing">master scouting spreadsheet</a>
  </ul>
  <a href="https://github.com/FRC2834" style="color: lightslategrey; margin-top: 30px; margin-bottom: 20px; font-size: 11px">this app was created using a template by blackhawks 2834</a>
</template>

<script setup lang="ts">
// Fetch configurations list
const fetchResult = await fetch(`${import.meta.env.BASE_URL}assets/configurations.txt`);

if (!fetchResult.ok)
  throw new Error(`Configuration list fetch failed: HTTP ${fetchResult.status} (${fetchResult.statusText})`);

// Get text data, then convert to array
const textData = await fetchResult.text();
const list = $ref(textData.split("\n").map(value => value.trim()).filter(value => value.length > 0));
</script>

<style>

h1 {
  font-weight: normal;
  text-decoration: overline;
  font-size: 250%;
  margin: 0px;
  color: greenyellow;
}

.midImg {
  display: block;
  margin-left: auto;
  margin-right: auto;
}

</style>

<style lang="postcss">
.link-list {
  margin: 0;

  li {
    margin: 6px 0;
  }
}

</style>
