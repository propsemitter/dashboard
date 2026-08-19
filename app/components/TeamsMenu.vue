<script setup lang="ts">
import type { DropdownMenuItem } from '@nuxt/ui'

defineProps<{
  collapsed?: boolean
}>()

const modules = ref([{
  label: 'CMS сайта компании',
  icon: 'i-lucide-panels-top-left',
  to: '/cms'
}, {
  label: 'HR',
  icon: 'i-lucide-users-round',
  to: '/hr'
}, {
  label: 'Проекты',
  icon: 'i-lucide-folder-kanban',
  to: '/',
  active: true
}])
const selectedModule = ref(modules.value[2])

const items = computed<DropdownMenuItem[][]>(() => {
  return [modules.value.map(module => ({
    ...module,
    onSelect() {
      selectedModule.value = module
    }
  }))]
})
</script>

<template>
  <UDropdownMenu
    :items="items"
    :content="{ align: 'center', collisionPadding: 12 }"
    :ui="{ content: collapsed ? 'w-40' : 'w-(--reka-dropdown-menu-trigger-width)' }"
  >
    <UButton
      v-bind="{
        ...selectedModule,
        label: collapsed ? undefined : selectedModule?.label,
        trailingIcon: collapsed ? undefined : 'i-lucide-chevrons-up-down'
      }"
      color="neutral"
      variant="ghost"
      block
      :square="collapsed"
      class="data-[state=open]:bg-elevated"
      :class="[!collapsed && 'py-2']"
      :ui="{
        trailingIcon: 'text-dimmed'
      }"
    />
  </UDropdownMenu>
</template>
