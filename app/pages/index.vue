<script setup lang="ts">
const projects = [
  { name: 'Мобильное приложение', team: 'Product squad', status: 'В работе', progress: 72, due: '22 авг', color: 'primary' },
  { name: 'Платформа аналитики', team: 'Data team', status: 'В работе', progress: 48, due: '04 сен', color: 'info' },
  { name: 'Обновление API', team: 'Backend team', status: 'На паузе', progress: 31, due: '18 сен', color: 'neutral' }
]
const activity = [
  { title: 'Ирина закрыла задачу «Сценарии авторизации»', time: '12 минут назад', icon: 'i-lucide-check-circle-2', color: 'text-success' },
  { title: 'Алексей добавил комментарий в «Платформу аналитики»', time: '48 минут назад', icon: 'i-lucide-message-square', color: 'text-info' },
  { title: 'Новый релиз запланирован на 28 августа', time: '2 часа назад', icon: 'i-lucide-rocket', color: 'text-warning' }
]
</script>

<template>
  <UDashboardPanel id="overview">
    <template #header>
      <UDashboardNavbar title="Обзор">
        <template #leading><UDashboardSidebarCollapse /></template>
        <template #right><UButton icon="i-lucide-plus" label="Новый проект" to="/projects" /></template>
      </UDashboardNavbar>
    </template>
    <template #body>
      <div class="flex flex-col gap-8">
        <div>
          <p class="text-sm text-muted">Вторник, 19 августа 2026</p>
          <h1 class="mt-1 text-3xl font-semibold tracking-tight text-highlighted">Добрый день, команда</h1>
          <p class="mt-2 max-w-2xl text-muted">Короткий срез по активным проектам и задачам на этой неделе.</p>
        </div>
        <div class="grid gap-4 sm:grid-cols-2 xl:grid-cols-4">
          <UCard v-for="stat in [{ label: 'Активные проекты', value: '8', detail: '+2 за месяц', icon: 'i-lucide-folder-kanban' }, { label: 'Задачи в работе', value: '34', detail: '12 на этой неделе', icon: 'i-lucide-list-checks' }, { label: 'Просрочено', value: '5', detail: 'Нужно внимание', icon: 'i-lucide-clock-3' }, { label: 'Участники', value: '16', detail: '4 команды', icon: 'i-lucide-users' }]" :key="stat.label">
            <div class="flex items-start justify-between"><div><p class="text-sm text-muted">{{ stat.label }}</p><p class="mt-3 text-3xl font-semibold text-highlighted">{{ stat.value }}</p></div><UIcon :name="stat.icon" class="size-5 text-primary" /></div>
            <p class="mt-3 text-xs text-muted">{{ stat.detail }}</p>
          </UCard>
        </div>
        <div class="grid gap-6 xl:grid-cols-[1.4fr_1fr]">
          <UCard :ui="{ body: 'p-0 sm:p-0' }">
            <div class="flex items-center justify-between border-b border-default px-5 py-4"><div><h2 class="font-semibold text-highlighted">Активные проекты</h2><p class="mt-1 text-sm text-muted">Статус delivery по ключевым инициативам</p></div><UButton variant="ghost" color="neutral" label="Все проекты" to="/projects" trailing-icon="i-lucide-arrow-up-right" /></div>
            <div class="divide-y divide-default">
              <div v-for="project in projects" :key="project.name" class="flex flex-col gap-3 px-5 py-4 sm:flex-row sm:items-center sm:justify-between"><div class="min-w-0"><div class="flex items-center gap-2"><span class="size-2 rounded-full bg-primary" /><p class="truncate font-medium text-highlighted">{{ project.name }}</p></div><p class="mt-1 text-sm text-muted">{{ project.team }} · дедлайн {{ project.due }}</p></div><div class="flex items-center gap-4 sm:w-48"><div class="flex-1"><div class="mb-1 flex justify-between text-xs text-muted"><span>{{ project.status }}</span><span>{{ project.progress }}%</span></div><UProgress :model-value="project.progress" :color="project.color as any" size="sm" /></div></div></div>
            </div>
          </UCard>
          <UCard><div class="flex items-center justify-between"><div><h2 class="font-semibold text-highlighted">Последняя активность</h2><p class="mt-1 text-sm text-muted">Что происходит в workspace</p></div><UButton icon="i-lucide-ellipsis" color="neutral" variant="ghost" square /></div><div class="mt-6 flex flex-col gap-6"> <div v-for="item in activity" :key="item.title" class="flex gap-3"><UIcon :name="item.icon" :class="['mt-0.5 size-5', item.color]" /><div><p class="text-sm leading-5 text-highlighted">{{ item.title }}</p><p class="mt-1 text-xs text-muted">{{ item.time }}</p></div></div></div></UCard>
        </div>
      </div>
    </template>
  </UDashboardPanel>
</template>
