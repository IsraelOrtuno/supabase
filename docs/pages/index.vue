<script setup lang="ts">
const { data: page } = await useAsyncData('index', () => queryContent('/').findOne())

useSeoMeta({
  title: page.value.title,
  ogTitle: page.value.title,
  description: page.value.description,
  ogDescription: page.value.description,
  ogImage: 'https://supabase.nuxtjs.org/social-card.jpg',
  twitterImage: 'https://supabase.nuxtjs.org/social-card.jpg',
})
</script>

<template>
  <div>
    <ULandingHero
      v-if="page.hero"
      v-bind="page.hero"
    >
      <template #title>
        <MDC :value="page.hero.title" />
      </template>

      <MDC
        :value="page.hero.code"
        tag="pre"
        class="prose prose-primary dark:prose-invert max-w-none"
      />
    </ULandingHero>

    <ULandingSection :title="page.features.title">
      <UPageGrid>
        <ULandingCard
          v-for="(item, index) of page.features.items"
          :key="index"
          v-bind="item"
        />
      </UPageGrid>
    </ULandingSection>
  </div>
</template>
