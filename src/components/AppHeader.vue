<script setup lang="ts">
import { ref, computed } from 'vue'
import type { ComputedRef } from 'vue'
import { useUserStore } from '@/stores/user'
import { getAuth, signOut } from 'firebase/auth'
import { useRouter } from 'vue-router'

const userStore = useUserStore()
const router = useRouter()

interface IMenuItem {
  label: string
  icon: string
  path: string
  show: boolean
}

const items = ref<IMenuItem[]>([
  {
    label: 'Map',
    icon: 'pi pi-map',
    path: '/',
    show: true
  },
  {
    label: 'Screens',
    icon: 'pi pi-images',
    path: '/screens',
    show: true
  },
  {
    label: 'Statistic',
    icon: 'pi pi-chart-pie',
    path: '/statistic',
    show: true
  }
])

</script>
<template>
  <app-menubar :model="items" class="menu">
    <template #item="{ item, props }">
      <template v-if="item.show">
        <router-link :to="item.path" class="flex align-items-center" v-bind="props.action">
          <span :class="item.icon" class="p-menuitem-icon" />
          <span class="ml-2">{{ item.label }}</span>
        </router-link>
      </template>
    </template>
  </app-menubar>
</template>

<style scoped>
.menu {
  margin: 30px 0;
}
.menu-exit {
  cursor: pointer;
}
.exit {
  display: flex;
  align-items: center;
}
</style>
