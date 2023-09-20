
<template>
 
  <div class="dark:bg-gray-900">
    <TransitionRoot as="template" :show="sidebarOpen">
      <Dialog as="div" class="relative z-50 lg:hidden" @close="sidebarOpen = false">
        <TransitionChild as="template" enter="transition-opacity ease-linear duration-300" enter-from="opacity-0"
          enter-to="opacity-100" leave="transition-opacity ease-linear duration-300" leave-from="opacity-100"
          leave-to="opacity-0">
          <div class="fixed inset-0 bg-gray-900/80" />
        </TransitionChild>

        <div class="fixed inset-0 flex">
          <TransitionChild as="template" enter="transition ease-in-out duration-300 transform"
            enter-from="-translate-x-full" enter-to="translate-x-0" leave="transition ease-in-out duration-300 transform"
            leave-from="translate-x-0" leave-to="-translate-x-full">
            <DialogPanel class="relative flex flex-1 w-full max-w-xs mr-16">
              <TransitionChild as="template" enter="ease-in-out duration-300" enter-from="opacity-0"
                enter-to="opacity-100" leave="ease-in-out duration-300" leave-from="opacity-100" leave-to="opacity-0">
                <div class="absolute top-0 flex justify-center w-16 pt-5 left-full">
                  <button type="button" class="-m-2.5 p-2.5" @click="sidebarOpen = false">
                    <span class="sr-only">Close sidebar</span>
                    <XMarkIcon class="w-6 h-6 text-white" aria-hidden="true" />
                  </button>
                </div>
              </TransitionChild>
              <!-- Sidebar component, swap this element with another sidebar if you like -->
              <div
                class="flex flex-col px-6 pb-4 overflow-y-auto bg-slate-50 dark:bg-gray-700 grow gap-y-5 ring-1 ring-white/10">
                <div class="flex items-center h-16 shrink-0">
                  <svg xmlns="http://www.w3.org/2000/svg" class="w-auto h-8" viewBox="0 0 128 128">
                    <path
                      d="M0 8.934l49.854.158 14.167 24.47 14.432-24.47L128 8.935l-63.834 110.14zm126.98.637l-24.36.02-38.476 66.053L25.691 9.592.942 9.572l63.211 107.89zm-25.149-.008l-22.745.168-15.053 24.647L49.216 9.73l-22.794-.168 37.731 64.476zm-75.834-.17l23.002.009m-23.002-.01l23.002.01"
                      fill="none" />
                    <path d="M25.997 9.393l23.002.009L64.035 34.36 79.018 9.404 102 9.398 64.15 75.053z" fill="#35495e" />
                    <path d="M.91 9.569l25.067-.172 38.15 65.659L101.98 9.401l25.11.026-62.966 108.06z" fill="#41b883" />
                  </svg>
                </div>
                <nav class="flex flex-col flex-1">
                  <ul role="list" class="flex flex-col flex-1 gap-y-7">
                    <li>
                      <ul role="list" class="-mx-2 space-y-1">
                        <li v-for="item in navigation" :key="item.name">
                          <a :href="item.href"
                            :class="[item.current ? 'bg-gray-800 text-white' : 'text-gray-400 hover:text-white hover:bg-gray-800', 'group flex gap-x-3 rounded-md p-2 text-sm leading-6 font-semibold']">
                            <component :is="item.icon" class="w-6 h-6 shrink-0" aria-hidden="true" />
                            {{ item.name }}
                          </a>
                        </li>
                      </ul>
                    </li>
                    <li>
                      <div class="text-xs font-semibold leading-6 text-gray-400">Your teams</div>
                      <ul role="list" class="mt-2 -mx-2 space-y-1">
                        <li v-for="team in teams" :key="team.name">
                          <a :href="team.href"
                            :class="[team.current ? 'bg-gray-800 text-white' : 'text-gray-400 hover:text-white hover:bg-gray-800', 'group flex gap-x-3 rounded-md p-2 text-sm leading-6 font-semibold']">
                            <span
                              class="flex h-6 w-6 shrink-0 items-center justify-center rounded-lg border border-gray-700 bg-gray-800 text-[0.625rem] font-medium text-gray-400 group-hover:text-white">{{
                                team.initial }}</span>
                            <span class="truncate">{{ team.name }}</span>
                          </a>
                        </li>
                      </ul>
                    </li>
                    <li class="mt-auto">
                      <a href="#"
                        class="flex p-2 -mx-2 text-sm font-semibold leading-6 text-gray-400 rounded-md group gap-x-3 hover:bg-gray-800 hover:text-white">
                        <Cog6ToothIcon class="w-6 h-6 shrink-0" aria-hidden="true" />
                        Settings
                      </a>
                    </li>
                  </ul>
                </nav>
              </div>
            </DialogPanel>
          </TransitionChild>
        </div>
      </Dialog>
    </TransitionRoot>

    <!-- Static sidebar for desktop -->
    <div class="hidden lg:fixed lg:inset-y-0 lg:z-50 lg:flex lg:w-72 lg:flex-col">
      <!-- Sidebar component, swap this element with another sidebar if you like -->
      <div class="flex flex-col px-6 pb-4 overflow-y-auto bg-slate-50 dark:bg-gray-700 grow gap-y-5">
        <div class="flex items-center h-16 shrink-0">
          <svg xmlns="http://www.w3.org/2000/svg" class="w-auto h-8" viewBox="0 0 128 128">
            <path
              d="M0 8.934l49.854.158 14.167 24.47 14.432-24.47L128 8.935l-63.834 110.14zm126.98.637l-24.36.02-38.476 66.053L25.691 9.592.942 9.572l63.211 107.89zm-25.149-.008l-22.745.168-15.053 24.647L49.216 9.73l-22.794-.168 37.731 64.476zm-75.834-.17l23.002.009m-23.002-.01l23.002.01"
              fill="none" />
            <path d="M25.997 9.393l23.002.009L64.035 34.36 79.018 9.404 102 9.398 64.15 75.053z" fill="#35495e" />
            <path d="M.91 9.569l25.067-.172 38.15 65.659L101.98 9.401l25.11.026-62.966 108.06z" fill="#41b883" />
          </svg>
        </div>
        <nav class="flex flex-col flex-1">
          <ul role="list" class="flex flex-col flex-1 gap-y-7">
            <li>
              <ul role="list" class="-mx-2 space-y-1">
                <li v-for="item in navigation" :key="item.name">
                  <a :href="item.href"
                    :class="[item.current ? 'bg-gray-800 text-white' : 'text-gray-400 hover:text-white hover:bg-gray-800', 'group flex gap-x-3 rounded-md p-2 text-sm leading-6 font-semibold']">
                    <component :is="item.icon" class="w-6 h-6 shrink-0" aria-hidden="true" />
                    {{ item.name }}
                  </a>
                </li>
              </ul>
            </li>
            <li>
              <div class="text-xs font-semibold leading-6 text-gray-400">UI ELEMENTS</div>
              <ul role="list" class="mt-2 -mx-2 space-y-1">
                <li v-for="team in teams" :key="team.name">
                  <a :href="team.href"
                    :class="[team.current ? 'bg-gray-800 text-white' : 'text-gray-400 hover:text-white hover:bg-gray-800', 'group flex gap-x-3 rounded-md p-2 text-sm leading-6 font-semibold']">
                    <span
                      class="flex h-6 w-6 shrink-0 items-center justify-center rounded-lg border border-gray-700 bg-gray-800 text-[0.625rem] font-medium text-gray-400 group-hover:text-white">{{
                        team.initial }}</span>
                    <span class="truncate">{{ team.name }}</span>
                  </a>
                </li>
              </ul>
            </li>
            <li class="mt-auto">
              <a href="#"
                class="flex p-2 -mx-2 text-sm font-semibold leading-6 text-gray-400 rounded-md group gap-x-3 hover:bg-gray-800 hover:text-white">
                <Cog6ToothIcon class="w-6 h-6 shrink-0" aria-hidden="true" />
                Settings
              </a>
            </li>
          </ul>
        </nav>
      </div>
    </div>

    <div class="lg:pl-72">
      <div
        class="sticky top-0 z-40 flex items-center h-16 px-4 transition-all shrink-0 gap-x-4 sm:gap-x-6 sm:px-6 lg:px-8"
        :class="{ 'bg-white dark:bg-slate-700 border-gray-200 shadow-sm border-b transition-all': isScrolled }">
        <button type="button" class="-m-2.5 p-2.5 text-gray-700 lg:hidden" @click="sidebarOpen = true">
          <span class="sr-only">Open sidebar</span>
          <Bars3Icon class="w-6 h-6" aria-hidden="true" />
        </button>

        <!-- Separator -->
        <div class="w-px h-6 bg-gray-900/10 lg:hidden" aria-hidden="true" />

        <div class="flex self-stretch flex-1 gap-x-4 lg:gap-x-6">
          <form class="relative flex flex-1" action="#" method="GET">
            <label for="search-field" class="sr-only">Search</label>
            <MagnifyingGlassIcon class="absolute inset-y-0 left-0 w-5 h-full text-gray-400 pointer-events-none"
              aria-hidden="true" />
            <input id="search-field"
              class="block w-full h-full py-0 pl-8 pr-0 text-gray-900 bg-transparent border-0 placeholder:text-gray-400 sm:text-sm"
              :class="{ 'bg-white dark:bg-slate-700 dark:text-white': isScrolled }" placeholder="Search..." type="search"
              name="search" />
          </form>
          <div class="flex items-center gap-x-4 lg:gap-x-6">
            <button @click="toggleDark()" type="button" class="-m-2.5 p-2.5 text-gray-400 hover:text-gray-500">
              <span class="sr-only">Color mode</span>
              <SunIcon v-if="!isDark" class="w-6 h-6" aria-hidden="true" />
              <MoonIcon v-else class="w-6 h-6" aria-hidden="true" />
            </button>
            <Popover>
              <PopoverButton v-slot="{ open }" type="button" class="-m-2.5 p-2.5 text-gray-400 hover:text-gray-500">
                <span class="sr-only">View shortcuts</span>
                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                  stroke="currentColor" class="w-6 h-6">
                  <path stroke-linecap="round" stroke-linejoin="round"
                    d="M13.5 16.875h3.375m0 0h3.375m-3.375 0V13.5m0 3.375v3.375M6 10.5h2.25a2.25 2.25 0 002.25-2.25V6a2.25 2.25 0 00-2.25-2.25H6A2.25 2.25 0 003.75 6v2.25A2.25 2.25 0 006 10.5zm0 9.75h2.25A2.25 2.25 0 0010.5 18v-2.25a2.25 2.25 0 00-2.25-2.25H6a2.25 2.25 0 00-2.25 2.25V18A2.25 2.25 0 006 20.25zm9.75-9.75H18a2.25 2.25 0 002.25-2.25V6A2.25 2.25 0 0018 3.75h-2.25A2.25 2.25 0 0013.5 6v2.25a2.25 2.25 0 002.25 2.25z" />
                </svg>
              </PopoverButton>
              <transition enter-active-class="transition duration-200 ease-out" enter-from-class="translate-y-1 opacity-0"
                enter-to-class="translate-y-0 opacity-100" leave-active-class="transition duration-150 ease-in"
                leave-from-class="translate-y-0 opacity-100" leave-to-class="translate-y-1 opacity-0">
                <PopoverPanel
                  class="absolute z-10 w-screen max-w-sm px-4 mt-3 transform -translate-x-32 max-h-44 left-3/4 sm:px-0 lg:max-w-sm">
                  <div
                    class="overflow-hidden bg-gray-200 divide-y divide-gray-200 rounded-lg shadow dark:bg-slate-400 sm:grid sm:grid-cols-2 sm:gap-px sm:divide-y-0">
                    <div v-for="(action, actionIdx) in actions" :key="action.title"
                      :class="[actionIdx === 0 ? 'rounded-tl-lg rounded-tr-lg sm:rounded-tr-none' : '', actionIdx === 1 ? 'sm:rounded-tr-lg' : '', actionIdx === actions.length - 2 ? 'sm:rounded-bl-lg' : '', actionIdx === actions.length - 1 ? 'rounded-bl-lg rounded-br-lg sm:rounded-bl-none' : '', 'group relative dark:bg-slate-700 bg-white p-6 focus-within:ring-2 focus-within:ring-inset focus-within:ring-blue-500']">
                      <div>
                        <span
                          :class="[action.iconBackground, action.iconForeground, 'inline-flex rounded-lg p-3 ring-4 ring-white']">
                          <component :is="action.icon" class="w-6 h-6" aria-hidden="true" />
                        </span>
                      </div>
                      <div class="mt-8">
                        <h3 class="text-base font-semibold leading-6 text-gray-900 dark:text-white">
                          <a :href="action.href" class="focus:outline-none">
                            <!-- Extend touch target to entire panel -->
                            <span class="absolute inset-0" aria-hidden="true" />
                            {{ action.title }}
                          </a>
                        </h3>
                        <p class="mt-2 text-sm text-gray-500 dark:text-gray-300">Doloribus dolorese.</p>
                      </div>
                      <span class="absolute text-gray-300 pointer-events-none right-6 top-6 group-hover:text-gray-400"
                        aria-hidden="true">
                        <svg class="w-6 h-6" fill="currentColor" viewBox="0 0 24 24">
                          <path
                            d="M20 4h1a1 1 0 00-1-1v1zm-1 12a1 1 0 102 0h-2zM8 3a1 1 0 000 2V3zM3.293 19.293a1 1 0 101.414 1.414l-1.414-1.414zM19 4v12h2V4h-2zm1-1H8v2h12V3zm-.707.293l-16 16 1.414 1.414 16-16-1.414-1.414z" />
                        </svg>
                      </span>
                    </div>
                  </div>
                </PopoverPanel>
              </transition>
            </Popover>
            <Popover>
              <PopoverButton v-slot="{ open }" type="button" class="-m-2.5 p-2.5 text-gray-400 hover:text-gray-500">
                <span class="sr-only">View notifications</span>
                <BellIcon class="w-6 h-6" aria-hidden="true" />
              </PopoverButton>
              <transition enter-active-class="transition duration-200 ease-out" enter-from-class="translate-y-1 opacity-0"
                enter-to-class="translate-y-0 opacity-100" leave-active-class="transition duration-150 ease-in"
                leave-from-class="translate-y-0 opacity-100" leave-to-class="translate-y-1 opacity-0">
                <PopoverPanel>
                  <div
                    class="absolute z-10 flex flex-col w-screen h-full max-w-sm px-4 mt-3 transform -translate-x-12 rounded-lg shadow-lg ring-1 ring-black ring-opacity-5 max-h-44 left-3/4 sm:px-0 lg:max-w-sm">
                    <div class="p-4 bg-gray-50 dark:bg-slate-700">
                      <a href="##"
                        class="flow-root px-2 py-2 transition duration-150 ease-in-out rounded-md hover:bg-gray-100 focus:outline-none focus-visible:ring focus-visible:ring-orange-500 focus-visible:ring-opacity-50">
                        <div class="flex flex-row justify-between">
                          <span class="flex items-center">
                            <span class="text-sm font-medium text-gray-900 dark:text-gray-300">
                              Notifications
                            </span>
                          </span>
                          <span class="block text-sm text-gray-500 dark:text-gray-300">
                            <svg xmlns="http://www.w3.org/2000/svg" fill="none"  viewBox="0 0 24 24" stroke-width="1.5"
                              stroke="currentColor" class="w-6 h-6">
                              <path stroke-linecap="round" stroke-linejoin="round"
                                d="M21.75 6.75v10.5a2.25 2.25 0 01-2.25 2.25h-15a2.25 2.25 0 01-2.25-2.25V6.75m19.5 0A2.25 2.25 0 0019.5 4.5h-15a2.25 2.25 0 00-2.25 2.25m19.5 0v.243a2.25 2.25 0 01-1.07 1.916l-7.5 4.615a2.25 2.25 0 01-2.36 0L3.32 8.91a2.25 2.25 0 01-1.07-1.916V6.75" />
                            </svg>

                          </span>
                        </div>
                      </a>
                    </div>
                    <div class="relative grid gap-8 bg-white dark:bg-slate-700 p-7 lg:grid-cols-1">
                      <a v-for="item in notifications" :key="item.name" :href="item.href"
                        class="flex items-center p-2 -m-3 transition duration-150 ease-in-out rounded-lg hover:bg-gray-50 focus:outline-none focus-visible:ring focus-visible:ring-orange-500 focus-visible:ring-opacity-50">
                        <div class="flex items-center justify-center w-10 h-10 text-white shrink-0 sm:h-12 sm:w-12">
                          <img width="30" height="30" src="https://img.icons8.com/ios-glyphs/30/user--v1.png"
                            alt="user--v1" />
                        </div>
                        <div class="ml-4">
                          <p class="text-sm font-medium text-gray-900 dark:text-gray-100">
                            {{ item.name }}
                          </p>
                          <p class="text-sm text-gray-500 dark:text-gray-200">
                            {{ item.description }}
                          </p>
                        </div>
                      </a>
                    </div>
                    <div class="p-4 dark:bg-slate-700 bg-gray-50">
                      <a href="##"
                        class="flow-root px-2 py-2 transition duration-150 ease-in-out rounded-md hover:bg-gray-100 focus:outline-none focus-visible:ring focus-visible:ring-orange-500 focus-visible:ring-opacity-50">
                        <span class="flex items-center justify-center">
                          <span class="text-sm font-medium text-blue-600">
                            View All Notificatoins
                          </span>
                        </span>
                      </a>
                    </div>
                  </div>
                </PopoverPanel>
              </transition>
            </Popover>



            <!-- Separator -->
            <!-- <div class="hidden lg:block lg:h-6 lg:w-px lg:bg-gray-900/10" aria-hidden="true" /> -->

            <!-- Profile dropdown -->
            <div class="relative">
              <button @click="open = !open" class="-m-1.5 flex items-center p-1.5">
                <span class="sr-only">Open user menu</span>
                <img class="w-8 h-8 rounded-full bg-gray-50"
                  src="https://demos.pixinvent.com/vuexy-vuejs-admin-template/demo-1/assets/avatar-1-129659bb.png"
                  alt="" />
              </button>

            </div>
          </div>
        </div>
      </div>

      <main class="py-10">
        <div class="h-screen px-4 sm:px-6 lg:px-8">
          <!-- Your content -->


        </div>
      </main>
      <TransitionRoot as="template" :show="open">
        <Dialog as="div" class="relative z-50" @close="open = false">
          <div class="fixed inset-0" />

          <div class="fixed inset-0 overflow-hidden">
            <div class="absolute inset-0 overflow-hidden">
              <div class="fixed inset-y-0 right-0 flex max-w-full pl-10 pointer-events-none">
                <TransitionChild as="template" enter="transform transition ease-in-out duration-500 sm:duration-700"
                  enter-from="translate-x-full" enter-to="translate-x-0"
                  leave="transform transition ease-in-out duration-500 sm:duration-700" leave-from="translate-x-0"
                  leave-to="translate-x-full">
                  <DialogPanel class="w-screen max-w-md pointer-events-auto">
                    <div class="flex flex-col h-full py-6 overflow-y-scroll bg-white shadow-xl dark:bg-slate-900">
                      <div class="px-4 sm:px-6">
                        <div class="flex items-start justify-between">
                          <DialogTitle class="text-base font-semibold leading-6 text-gray-900 dark:text-white">Panel title
                          </DialogTitle>
                          <div class="flex items-center ml-3 h-7">
                            <button type="button"
                              class="relative text-gray-400 bg-white rounded-md hover:text-gray-500 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2"
                              @click="open = false">
                              <span class="absolute -inset-2.5" />
                              <span class="sr-only">Close panel</span>
                              <XMarkIcon class="w-6 h-6" aria-hidden="true" />
                            </button>
                          </div>
                        </div>
                      </div>
                      <div class="relative flex-1 px-4 mt-6 sm:px-6">
                        <!-- Your content -->
                      </div>
                    </div>
                  </DialogPanel>
                </TransitionChild>
              </div>
            </div>
          </div>
        </Dialog>
      </TransitionRoot>
    </div>
    <footer
      :class="[isSticky ? 'sticky bottom-0 bg-white dark:bg-slate-700 transition-all duration-75' : 'transition-all duration-75']">
      >
      <div class="px-6 py-4 mx-auto max-w-7xl md:flex md:items-center md:justify-between lg:px-8">
        <div class="flex justify-center space-x-6 md:order-2">
          <a v-for="item in navigation_footer " :key="item.name" :href="item.href"
            class="text-gray-400 hover:text-gray-500">
            <span class="sr-only">{{ item.name }}</span>
          <a :href="item.href">{{ item.name }}</a>
          </a>
        </div>
        <div class="mt-8 md:order-1 md:mt-0">
          <p class="text-xs leading-5 text-center text-gray-300">&copy; 2020 Your Company, Inc. All rights reserved.</p>
        </div>
      </div>
    </footer>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import {
  Dialog,
  DialogPanel,
  Popover, PopoverButton, PopoverPanel,
  TransitionChild,
  TransitionRoot,
  DialogTitle
} from '@headlessui/vue'
import {
  Bars3Icon,
  BellIcon,
  CalendarIcon,
  ChartPieIcon,
  Cog6ToothIcon,
  DocumentDuplicateIcon,
  DocumentIcon,
  FolderIcon,
  HomeIcon,
  UsersIcon,
  XMarkIcon,
  SunIcon,
  MoonIcon,
  AcademicCapIcon,
  BanknotesIcon,
  CheckBadgeIcon,
  ClockIcon,
  ReceiptRefundIcon,
  CogIcon,
  UserIcon,
  QuestionMarkCircleIcon

} from '@heroicons/vue/24/outline'
import {
  ChevronDownIcon, MagnifyingGlassIcon, ArrowDownCircleIcon,
  ArrowPathIcon,
  ArrowUpCircleIcon,
} from '@heroicons/vue/20/solid'
import HelloWorld from './components/HelloWorld.vue'
import { defineComponent, h } from 'vue'
import { useDark, useToggle } from '@vueuse/core'

const isDark = useDark()
const toggleDark = useToggle(isDark)

const isScrolled = ref(false);
const isSticky = ref(false);

onMounted(() => {
  window.addEventListener("scroll", handleScroll);
  window.addEventListener("scroll", handleSticky);
});

const handleScroll = () => {
  if (window.scrollY > 0) {
    isScrolled.value = true;
  } else {
    isScrolled.value = false;
  }
};
let prevScrollY = ref(0);


const notifications = [
  {
    name: 'Congratulations Flora!',
    description: 'Won the monthly best seller badge.',
    href: '##',
    icon: `
      <svg
        width="48"
        height="48"
        viewBox="0 0 48 48"
        fill="none"
        aria-hidden="true"
        xmlns="http://www.w3.org/2000/svg"
      >
        <rect width="48" height="48" rx="8" fill="#FFEDD5" />
        <path
          d="M24 11L35.2583 17.5V30.5L24 37L12.7417 30.5V17.5L24 11Z"
          stroke="#FB923C"
          stroke-width="2"
        />
        <path
          fill-rule="evenodd"
          clip-rule="evenodd"
          d="M16.7417 19.8094V28.1906L24 32.3812L31.2584 28.1906V19.8094L24 15.6188L16.7417 19.8094Z"
          stroke="#FDBA74"
          stroke-width="2"
        />
        <path
          fill-rule="evenodd"
          clip-rule="evenodd"
          d="M20.7417 22.1196V25.882L24 27.7632L27.2584 25.882V22.1196L24 20.2384L20.7417 22.1196Z"
          stroke="#FDBA74"
          stroke-width="2"
        />
      </svg>
    `,
  },
  {
    name: 'Automations',
    description: 'Create your own targeted content',
    href: '##',
    icon: `
      <svg
        width="48"
        height="48"
        viewBox="0 0 48 48"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <rect width="48" height="48" rx="8" fill="#FFEDD5" />
        <path
          d="M28.0413 20L23.9998 13L19.9585 20M32.0828 27.0001L36.1242 34H28.0415M19.9585 34H11.8755L15.9171 27"
          stroke="#FB923C"
          stroke-width="2"
        />
        <path
          fill-rule="evenodd"
          clip-rule="evenodd"
          d="M18.804 30H29.1963L24.0001 21L18.804 30Z"
          stroke="#FDBA74"
          stroke-width="2"
        />
      </svg>
    `,
  },
  {
    name: 'Reports',
    description: 'Keep track of your growth',
    href: '##',
    icon: `
      <svg
        width="48"
        height="48"
        viewBox="0 0 48 48"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <rect width="48" height="48" rx="8" fill="#FFEDD5" />
        <rect x="13" y="32" width="2" height="4" fill="#FDBA74" />
        <rect x="17" y="28" width="2" height="8" fill="#FDBA74" />
        <rect x="21" y="24" width="2" height="12" fill="#FDBA74" />
        <rect x="25" y="20" width="2" height="16" fill="#FDBA74" />
        <rect x="29" y="16" width="2" height="20" fill="#FB923C" />
        <rect x="33" y="12" width="2" height="24" fill="#FB923C" />
      </svg>
    `,
  },
]

const handleSticky = () => {
  const currentScrollY = window.scrollY;

  if (currentScrollY > prevScrollY.value) {
    // Scrolling down, make the footer not sticky
    isSticky.value = false;
  } else {
    // Scrolling up, make the footer sticky
    isSticky.value = true;
  }

  prevScrollY.value = currentScrollY;
};


const navigation = [
  { name: 'Dashboard', href: '#', icon: HomeIcon, current: true },
]
const teams = [
  { id: 1, name: 'Typography', href: '#', initial: 'T', current: false },

]

const navigation_footer = [
  {
    name: 'Facebook',
    href: '#',
  },
  {
    name: 'Instagram',
    href: '#',
  },
  {
    name: 'Twitter',
    href: '#',
  },
  {
    name: 'GitHub',
    href: '#',
  },
  {
    name: 'YouTube',
    href: '#',
  },
]


const actions = [
  {
    title: 'Calendar',
    href: '#',
    icon: CalendarIcon,
    iconForeground: 'text-gray-700',
    iconBackground: 'bg-gray-100',
  },
  {
    title: 'Invoice App',
    href: '#',
    icon: DocumentIcon,
    iconForeground: 'text-gray-700',
    iconBackground: 'bg-gray-100',
  },
  {
    title: 'Users',
    href: '#',
    icon: UserIcon,
    iconForeground: 'text-gray-700',
    iconBackground: 'bg-gray-100',
  },
  {
    title: 'Dashboard',
    href: '#',
    icon: HomeIcon,
    iconForeground: 'text-gray-700',
    iconBackground: 'bg-gray-100',
  },
  {
    title: 'Settings',
    href: '#',
    icon: CogIcon,
    iconForeground: 'text-gray-700',
    iconBackground: 'bg-gray-100',
  },
  {
    title: 'Help Center',
    href: '#',
    icon: QuestionMarkCircleIcon,
    iconForeground: 'text-gray-700',
    iconBackground: 'bg-gray-100',
  },
]
const open = ref(false)
const sidebarOpen = ref(false)
</script>