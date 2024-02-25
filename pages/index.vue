<script setup lang="ts">
const { data: posts } = await useAsyncData("home", () =>
  queryContent("/articles")
    .only(["title", "description", "createdAt", "image", "_path"])
    .limit(12)
    .find()
);

console.log(posts);

const route = useRoute();
</script>

<template>
  <div>
    <h1 class="text-center text-5xl font-black my-8">Blog</h1>
    <ul class="grid grid-cols-3 gap-3">
      <li v-for="post in posts" :key="post._path">
        <NuxtLink :to="post._path">
          <CoverImage
            :src="post.image"
            :alt="post.title"
            class="w-full h-44 object-cover"
          />
          <h4 class="text-lg font-bold">{{ post.title }}</h4>
          <p class="text-slate-600">{{ post.description }}</p>
          <p class="text-xs">{{ $dayjs(post.createdAt).fromNow() }}</p>
        </NuxtLink>
      </li>
    </ul>
  </div>
</template>
