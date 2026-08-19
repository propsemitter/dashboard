<script setup lang="ts">
const route = useRoute()
const code = String(route.params.code)
const activeTab = ref('about')

const projects: Record<string, { name: string; description: string; status: string; owner: string; updated: string; modules: string[]; environments: { name: string; detail: string; status: string }[]; artifacts: { name: string; type: string; url: string }[] }> = {
  'MOB-24': {
    name: 'Мобильное приложение', description: 'Клиентское приложение для пользователей сервиса.', status: 'В работе', owner: 'Продуктовая команда', updated: 'Сегодня, 10:42',
    modules: ['Авторизация', 'Профиль пользователя', 'Каталог', 'Уведомления', 'Платежи', 'Поддержка'],
    environments: [{ name: 'Production', detail: 'app.example.com', status: 'Стабильна' }, { name: 'Staging', detail: 'staging.app.example.com', status: 'Готова' }, { name: 'Development', detail: 'Локальная среда', status: 'Активна' }],
    artifacts: [{ name: 'Техническая документация', type: 'Документация', url: 'docs.example.com/mobile' }, { name: 'Макеты приложения', type: 'Figma', url: 'figma.com/file/mobile-app' }, { name: 'API контракт', type: 'OpenAPI', url: 'api.example.com/openapi' }]
  }
}

const project = computed(() => projects[code] ?? projects['MOB-24'])
const tabs = [{ value: 'about', label: 'О проекте', icon: 'i-lucide-layout-dashboard' }, { value: 'modules', label: 'Модули', icon: 'i-lucide-box' }, { value: 'environments', label: 'Среды', icon: 'i-lucide-server' }, { value: 'artifacts', label: 'Артефакты', icon: 'i-lucide-link-2' }]
</script>

<template>
  <UDashboardPanel id="project-detail">
    <template #header>
      <UDashboardNavbar :title="project.name">
        <template #leading><UDashboardSidebarCollapse /></template>
        <template #right><UButton icon="i-lucide-more-horizontal" color="neutral" variant="ghost" square /></template>
      </UDashboardNavbar>
    </template>
    <template #body>
      <div class="flex flex-col gap-6">
        <div class="flex flex-col gap-3 border-b border-default pb-6 sm:flex-row sm:items-start sm:justify-between">
          <div><div class="flex items-center gap-2"><NuxtLink to="/" class="text-sm text-muted hover:text-highlighted">Проекты</NuxtLink><UIcon name="i-lucide-chevron-right" class="size-4 text-dimmed" /><span class="text-sm text-muted">{{ code }}</span></div><h1 class="mt-3 text-2xl font-semibold text-highlighted">{{ project.name }}</h1><p class="mt-1 max-w-2xl text-sm text-muted">{{ project.description }}</p></div>
          <UBadge color="primary" variant="subtle">{{ project.status }}</UBadge>
        </div>

        <div class="flex gap-1 overflow-x-auto border-b border-default" role="tablist" aria-label="Разделы проекта">
          <button v-for="tab in tabs" :key="tab.value" type="button" role="tab" :aria-selected="activeTab === tab.value" class="flex shrink-0 items-center gap-2 border-b-2 px-4 py-3 text-sm font-medium transition-colors" :class="activeTab === tab.value ? 'border-primary text-highlighted' : 'border-transparent text-muted hover:text-highlighted'" @click="activeTab = tab.value"><UIcon :name="tab.icon" class="size-4" />{{ tab.label }}</button>
        </div>

        <section v-if="activeTab === 'about'" class="grid gap-4 md:grid-cols-3" role="tabpanel">
          <UCard><p class="text-sm text-muted">Статус</p><p class="mt-2 font-semibold text-highlighted">{{ project.status }}</p></UCard>
          <UCard><p class="text-sm text-muted">Владелец</p><p class="mt-2 font-semibold text-highlighted">{{ project.owner }}</p></UCard>
          <UCard><p class="text-sm text-muted">Последнее изменение</p><p class="mt-2 font-semibold text-highlighted">{{ project.updated }}</p></UCard>
          <UCard class="md:col-span-3"><div class="flex items-center gap-3"><div class="flex size-10 items-center justify-center rounded-lg bg-elevated"><UIcon name="i-lucide-info" class="size-5 text-primary" /></div><div><h2 class="font-semibold text-highlighted">Быстрая информация</h2><p class="mt-1 text-sm text-muted">В проекте {{ project.modules.length }} модулей, {{ project.environments.length }} среды и {{ project.artifacts.length }} артефакта.</p></div></div></UCard>
        </section>

        <section v-else-if="activeTab === 'modules'" role="tabpanel"><UCard><div class="flex items-center justify-between"><div><h2 class="font-semibold text-highlighted">Модули проекта</h2><p class="mt-1 text-sm text-muted">Основные части проекта</p></div><UButton icon="i-lucide-plus" label="Добавить модуль" variant="soft" /></div><div class="mt-5 grid gap-2 sm:grid-cols-2 lg:grid-cols-3"><div v-for="module in project.modules" :key="module" class="flex items-center gap-3 rounded-lg border border-default px-3 py-3"><UIcon name="i-lucide-box" class="size-4 text-primary" /><span class="text-sm text-highlighted">{{ module }}</span></div></div></UCard></section>

        <section v-else-if="activeTab === 'environments'" role="tabpanel"><UCard><div class="flex items-center justify-between"><div><h2 class="font-semibold text-highlighted">Среды проекта</h2><p class="mt-1 text-sm text-muted">Окружения и точки доступа</p></div><UButton icon="i-lucide-plus" label="Добавить среду" variant="soft" /></div><div class="mt-5 flex flex-col gap-3"><div v-for="environment in project.environments" :key="environment.name" class="flex items-center justify-between gap-4 rounded-lg border border-default px-4 py-3"><div class="flex items-center gap-3"><span class="size-2 rounded-full bg-success" /><div><p class="text-sm font-medium text-highlighted">{{ environment.name }}</p><p class="mt-1 text-xs text-muted">{{ environment.detail }}</p></div></div><span class="text-xs text-muted">{{ environment.status }}</span></div></div></UCard></section>

        <section v-else role="tabpanel"><UCard><div class="flex items-center justify-between"><div><h2 class="font-semibold text-highlighted">Артефакты проекта</h2><p class="mt-1 text-sm text-muted">Ссылки на документацию, макеты и контракты</p></div><UButton icon="i-lucide-plus" label="Добавить ссылку" variant="soft" /></div><div class="mt-5 divide-y divide-default"><a v-for="artifact in project.artifacts" :key="artifact.name" href="#" class="flex items-center justify-between gap-4 py-3 first:pt-0 last:pb-0"><div class="flex items-center gap-3"><div class="flex size-9 items-center justify-center rounded-lg bg-elevated"><UIcon name="i-lucide-link-2" class="size-4 text-primary" /></div><div><p class="text-sm font-medium text-highlighted">{{ artifact.name }}</p><p class="mt-1 text-xs text-muted">{{ artifact.type }} · {{ artifact.url }}</p></div></div><UIcon name="i-lucide-arrow-up-right" class="size-4 text-muted" /></a></div></UCard></section>
      </div>
    </template>
  </UDashboardPanel>
</template>
