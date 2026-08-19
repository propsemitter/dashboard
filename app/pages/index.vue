<script setup lang="ts">
const projects = [
  { name: 'Мобильное приложение', code: 'MOB-24', description: 'Клиентское приложение для пользователей сервиса.', modules: 6, environments: 3, artifacts: 8, status: 'В работе', color: 'primary', updated: 'Обновлён 12 минут назад' },
  { name: 'Платформа аналитики', code: 'DATA-12', description: 'Внутренняя платформа отчётности и продуктовых метрик.', modules: 4, environments: 4, artifacts: 11, status: 'В работе', color: 'info', updated: 'Обновлён сегодня' },
  { name: 'Обновление API', code: 'API-08', description: 'Версия API для интеграций и внешних клиентов.', modules: 3, environments: 2, artifacts: 5, status: 'На паузе', color: 'neutral', updated: 'Обновлён вчера' },
  { name: 'Дизайн-система', code: 'DS-03', description: 'Единые компоненты и правила интерфейсов продукта.', modules: 5, environments: 1, artifacts: 14, status: 'В работе', color: 'success', updated: 'Обновлён 2 дня назад' }
]
</script>

<template>
  <UDashboardPanel id="projects">
    <template #header>
      <UDashboardNavbar title="Проекты">
        <template #leading><UDashboardSidebarCollapse /></template>
        <template #right><UButton icon="i-lucide-plus" label="Новый проект" /></template>
      </UDashboardNavbar>
    </template>
    <template #body>
      <div class="flex flex-col gap-6">
        <div class="flex flex-col gap-1">
          <h1 class="text-2xl font-semibold tracking-tight text-highlighted">Проекты</h1>
          <p class="text-sm text-muted">Рабочие пространства для модулей, сред и артефактов.</p>
        </div>
        <div class="grid gap-3 md:grid-cols-2 xl:grid-cols-3">
          <UCard v-for="project in projects" :key="project.code" variant="subtle" class="transition-colors hover:border-primary/50">
            <NuxtLink :to="`/projects/${project.code}`" class="block">
              <div class="flex items-start justify-between gap-3">
                <div class="min-w-0">
                  <p class="text-xs font-medium uppercase tracking-wider text-primary">{{ project.code }}</p>
                  <h2 class="mt-1 truncate text-base font-semibold text-highlighted">{{ project.name }}</h2>
                </div>
                <UBadge :color="project.color as any" variant="subtle" size="sm">{{ project.status }}</UBadge>
              </div>
              <div class="mt-4 flex items-center gap-3 border-t border-default pt-3 text-xs text-muted">
                <span>{{ project.modules }} модулей</span>
                <span class="text-dimmed">·</span>
                <span>{{ project.environments }} среды</span>
                <span class="text-dimmed">·</span>
                <span>{{ project.artifacts }} ссылок</span>
              </div>
            </NuxtLink>
          </UCard>
        </div>
      </div>
    </template>
  </UDashboardPanel>
</template>
