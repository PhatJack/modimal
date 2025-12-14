<template>
  <UHeader class="bg-default h-auto backdrop-blur-none">
    <template #left>
      <NuxtLink to="/">
        <AppLogo class="h-10 w-auto shrink-0" />
      </NuxtLink>
    </template>

    <div class="" @mouseleave="closeMenu">
      <nav class="hidden lg:flex">
        <div
          v-for="item in items"
          :key="item.label"
          class="relative py-2"
          @mouseenter="openMenu(item)"
        >
          <UButton size="lg" variant="link" class="text-base text-gray-700 hover:text-gray-900">
            {{ item.label }}
          </UButton>
          <div
            v-show="openLabel === item.label"
            class="fixed top-14 left-0 z-40 h-dvh w-full bg-black/20 backdrop-blur perspective-normal"
          >
            <!-- Content layer -->
            <Transition name="dropdown">
              <div
                v-show="openLabel === item.label"
                class="bg-default relative z-50 w-full overflow-hidden"
              >
                <div
                  class="relative z-50 mx-auto size-full max-w-(--ui-container) px-4 sm:px-6 lg:px-8"
                >
                  <ul class="size-full py-2">
                    <li v-for="child in item.children" :key="child.label">
                      <UButton>
                        {{ child.label }}
                      </UButton>
                    </li>
                  </ul>
                </div>
              </div>
            </Transition>
          </div>
        </div>
      </nav>
    </div>
    <template #right>
      <!-- <UColorModeButton /> -->

      <UButton to="#" icon="i-lucide-search" aria-label="Search" color="neutral" variant="ghost" />
      <UButton
        to="#"
        icon="i-lucide-user-round"
        aria-label="User"
        color="neutral"
        variant="ghost"
      />
      <UButton
        to="#"
        icon="i-lucide-heart"
        aria-label="Favorites"
        color="neutral"
        variant="ghost"
      />
      <UButton
        to="#"
        icon="i-lucide-shopping-basket"
        aria-label="Shopping Basket"
        color="neutral"
        variant="ghost"
      />
    </template>
  </UHeader>
</template>

<script setup lang="ts">
const openLabel = ref<string | null>(null);
const items = ref([
  {
    label: 'Collection',
    children: [
      {
        label: 'Introduction',
        description: 'Fully styled and customizable components for Nuxt.',
        icon: 'i-lucide-house',
      },
      {
        label: 'Installation',
        description: 'Learn how to install and configure Nuxt UI in your application.',
        icon: 'i-lucide-cloud-download',
      },
      {
        label: 'Icons',
        icon: 'i-lucide-smile',
        description: 'You have nothing to do, @nuxt/icon will handle it automatically.',
      },
      {
        label: 'Colors',
        icon: 'i-lucide-swatch-book',
        description: 'Choose a primary and a neutral color from your Tailwind CSS theme.',
      },
      {
        label: 'Theme',
        icon: 'i-lucide-cog',
        description:
          'You can customize components by using the `class` / `ui` props or in your app.config.ts.',
      },
    ],
  },
  {
    label: 'New In',
    children: [
      {
        label: 'defineShortcuts',
        icon: 'i-lucide-file-text',
        description: 'Define shortcuts for your application.',
        to: '/docs/composables/define-shortcuts',
      },
      {
        label: 'useOverlay',
        icon: 'i-lucide-file-text',
        description: 'Display a modal/slideover within your application.',
        to: '/docs/composables/use-overlay',
      },
      {
        label: 'useToast',
        icon: 'i-lucide-file-text',
        description: 'Display a toast within your application.',
        to: '/docs/composables/use-toast',
      },
    ],
  },
  {
    label: 'Modiweek',
    children: [
      {
        label: 'Link',
        icon: 'i-lucide-file-text',
        description: 'Use NuxtLink with superpowers.',
        to: '/docs/components/link',
      },
      {
        label: 'Modal',
        icon: 'i-lucide-file-text',
        description: 'Display a modal within your application.',
        to: '/docs/components/modal',
      },
      {
        label: 'NavigationMenu',
        icon: 'i-lucide-file-text',
        description: 'Display a list of links.',
        to: '/docs/components/navigation-menu',
      },
      {
        label: 'Pagination',
        icon: 'i-lucide-file-text',
        description: 'Display a list of pages.',
        to: '/docs/components/pagination',
      },
      {
        label: 'Popover',
        icon: 'i-lucide-file-text',
        description: 'Display a non-modal dialog that floats around a trigger element.',
        to: '/docs/components/popover',
      },
      {
        label: 'Progress',
        icon: 'i-lucide-file-text',
        description: 'Show a horizontal bar to indicate task progression.',
        to: '/docs/components/progress',
      },
    ],
  },
  {
    label: 'Plus Size',
  },
  {
    label: 'Sustainability',
  },
]);

interface MenuItem {
  label: string;
  children?: Array<{
    label: string;
    description?: string;
    icon?: string;
    to?: string;
  }>;
}

function openMenu(item: MenuItem) {
  if (!item.children) {
    closeMenu();
    return;
  }
  openLabel.value = item.label;
}

function closeMenu() {
  openLabel.value = null;
}
</script>

<style scoped>
.dropdown-enter-active,
.dropdown-leave-active {
  transition:
    transform 0.5s cubic-bezier(0.16, 1, 0.3, 1),
    opacity 0.25s ease;
  transform-origin: top;
}

.dropdown-enter-from,
.dropdown-leave-to {
  transform: scaleY(0.85) skewX(10deg);
  opacity: 0;
}

.dropdown-enter-to,
.dropdown-leave-from {
  transform: scaleY(1) skewX(0deg);
  opacity: 1;
}
</style>
