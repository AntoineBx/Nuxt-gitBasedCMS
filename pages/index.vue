<script setup>
  
useHead({
  script: [
    { src: "https://identity.netlify.com/v1/netlify-identity-widget.js" },
  ],
});

const data = ref([]);

const { data: result, refresh } = await useAsyncData('bloggg', () => 
  queryContent('blog').find()
);

if (result) {
  data.value = unref(result);
  console.log(data.value);
}
</script>

<template>
 <div v-if="data.length">
    <div v-for="article in data" :key="article._path">
      <NuxtLink :to="article._path">
        <h2>{{ article.title }}</h2>
        <p>{{ article.description }}</p>
      </NuxtLink>
    </div>
  </div>
  <div v-else>
    <p>Loading...</p>
  </div>
</template>