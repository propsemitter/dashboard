<script setup lang="ts">
import type { NavigationMenuItem } from '@nuxt/ui'

const open = ref(false)

const links = [[
  { label: 'Обзор', icon: 'i-lucide-layout-dashboard', to: '/' },
  { label: 'Проекты', icon: 'i-lucide-folder-kanban', to: '/projects' },
  { label: 'Задачи', icon: 'i-lucide-list-checks', to: '/tasks' },
  { label: 'Команда', icon: 'i-lucide-users', to: '/team' }
], [{ label: 'Уведомления', icon: 'i-lucide-bell', to: '/notifications' }]] satisfies NavigationMenuItem[][]

const groups = computed(() => [{ id: 'links', label: 'Перейти', items: links.flat() }])
</script>

<template>
  <UDashboardGroup unit="rem">
    <UDashboardSidebar id="default" v-model:open="open" collapsible resizable class="bg-elevated/25">
      <template #header="{ collapsed }">
        <TeamsMenu :collapsed="collapsed" />
      </template>
      <template #default="{ collapsed }">
        <UDashboardSearchButton :collapsed="collapsed" class="bg-transparent ring-default" />
        <UNavigationMenu :collapsed="collapsed" :items="links[0]" orientation="vertical" tooltip popover />
        <UNavigationMenu :collapsed="collapsed" :items="links[1]" orientation="vertical" tooltip class="mt-auto" />
      </template>
      <template #footer="{ collapsed }">
        <UserMenu :collapsed="collapsed" />
      </template>
    </UDashboardSidebar>
    <UDashboardSearch :groups="groups" />
    <slot />
  </UDashboardGroup>
</template>
