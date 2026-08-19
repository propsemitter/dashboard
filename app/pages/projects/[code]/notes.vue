<script setup lang="ts">
const route = useRoute()
const notes = [{ title: 'Проверить тексты onboarding', text: 'Нужно сверить финальные тексты перед передачей в разработку.', author: 'Анна Петрова', source: 'CRM', time: 'Вчера' }, { title: 'Обсудить лимиты API платежей', text: 'Зафиксировать ограничения и сценарий деградации.', author: 'Иван Соколов', source: 'Telegram', time: '2 дня назад' }]
</script>

<template>
  <UDashboardPanel id="project-notes">
    <template #header><UDashboardNavbar title="Заметки проекта"><template #leading><UButton to="/projects/MOB-24" icon="i-lucide-arrow-left" color="neutral" variant="ghost" /></template></UDashboardNavbar></template>
    <template #body><div class="mx-auto flex w-full max-w-5xl flex-col gap-6 p-4 sm:p-6"><div><p class="text-sm text-muted">Проект {{ route.params.code }}</p><h1 class="mt-2 text-2xl font-semibold text-highlighted">Все заметки</h1><p class="mt-1 text-sm text-muted">Заметки, собранные в CRM и внешних каналах проекта.</p></div><div class="divide-y divide-default border-y border-default"><article v-for="note in notes" :key="note.title" class="flex flex-col gap-3 py-5 sm:flex-row sm:items-start sm:justify-between"><div class="min-w-0"><div class="flex items-center gap-2"><UIcon name="i-lucide-sticky-note" class="size-4 text-primary" /><h2 class="font-medium text-highlighted">{{ note.title }}</h2></div><p class="mt-2 max-w-2xl text-sm leading-6 text-muted">{{ note.text }}</p><p class="mt-3 text-xs text-dimmed">{{ note.author }} · {{ note.time }}</p></div><UBadge color="neutral" variant="subtle" class="w-fit">{{ note.source }}</UBadge></article></div></div></template>
  </UDashboardPanel>
</template>
