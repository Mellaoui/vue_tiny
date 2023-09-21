
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

    

    <div>
      <div
        class="sticky top-0 z-40 flex items-center h-16 px-4 transition-all bg-white dark:bg-slate-700 shrink-0 gap-x-4 sm:gap-x-6 sm:px-6 lg:px-8"
        :class="{ 'bg-white dark:bg-slate-700 border-gray-200 shadow-sm border-b transition-all': isScrolled }">
        <button type="button" class="-m-2.5 p-2.5 text-gray-700 lg:hidden" @click="sidebarOpen = true">
          <span class="sr-only">Open sidebar</span>
          <Bars3Icon class="w-6 h-6" aria-hidden="true" />
        </button>

        <!-- Separator -->
        <div class="w-px h-6 bg-gray-900/10 lg:hidden" aria-hidden="true" />
        <svg xmlns="http://www.w3.org/2000/svg" class="w-auto h-8" viewBox="0 0 128 128">
          <path
            d="M0 8.934l49.854.158 14.167 24.47 14.432-24.47L128 8.935l-63.834 110.14zm126.98.637l-24.36.02-38.476 66.053L25.691 9.592.942 9.572l63.211 107.89zm-25.149-.008l-22.745.168-15.053 24.647L49.216 9.73l-22.794-.168 37.731 64.476zm-75.834-.17l23.002.009m-23.002-.01l23.002.01"
            fill="none" />
          <path d="M25.997 9.393l23.002.009L64.035 34.36 79.018 9.404 102 9.398 64.15 75.053z" fill="#35495e" />
          <path d="M.91 9.569l25.067-.172 38.15 65.659L101.98 9.401l25.11.026-62.966 108.06z" fill="#41b883" />
        </svg>
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
                            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
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
      <div as="nav" class="hidden w-full bg-white shadow-sm dark:bg-slate-700 sm:inline-flex" :class="{ 'bg-white dark:bg-slate-700 border-gray-200 shadow-sm border-b transition-all': isScrolled }">
        <div class="w-full px-4 mx-auto sm:px-6 lg:px-8">
          <div class="flex h-16">
            <div class="flex">
              <nav class="hidden lg:flex lg:space-x-20 lg:py-2" aria-label="Global">
              

                <Popover v-slot="{ open }" class="relative">
                  <PopoverButton :class="open ? '' : 'text-opacity-90'">
                    <span
                      class="inline-flex items-center justify-between w-full px-4 py-2 text-sm font-medium text-gray-800 bg-gray-200 rounded-md hover:bg-gray-700 hover:text-white">
                      <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M2.25 12l8.954-8.955c.44-.439 1.152-.439 1.591 0L21.75 12M4.5 9.75v10.125c0 .621.504 1.125 1.125 1.125H9.75v-4.875c0-.621.504-1.125 1.125-1.125h2.25c.621 0 1.125.504 1.125 1.125V21h4.125c.621 0 1.125-.504 1.125-1.125V9.75M8.25 21h8.25" />
                      </svg>
                      <span class="ml-2">Dashbaord</span>
                      <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                        stroke="currentColor" class="w-6 h-6 ml-2">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M19.5 8.25l-7.5 7.5-7.5-7.5" />
                      </svg>
                    </span>
                  </PopoverButton>

                </Popover>

                <Popover v-slot="{ open }" class="relative">
                  <PopoverButton :class="open ? '' : 'text-opacity-90'">
                    <span
                      class="inline-flex items-center justify-between px-4 py-2 text-sm font-medium text-gray-800 bg-gray-200 rounded-md hover:bg-gray-700 hover:text-white">
                      <img class="w-6 h-6 hover:text-white" src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAAACXBIWXMAAAsTAAALEwEAmpwYAAAAdUlEQVR4nO2VYQqAIAyF3/E8d9FF7CAvgoIh6nKuQvCDgT+e+3CCApNGAoAdAI0Vrx5FYkdzCkmRO2SF2n4Z2ACsmbXMpQ2bBGfDJbN2E1jgU0Fv/S+wjo0eAnpfMr8W1BjjBBx+RDXU7OvPdeiURO3DmSDlAEeVyZCZgiE0AAAAAElFTkSuQmCC">
                      <span class="ml-2">Layouts</span>
                      <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                        stroke="currentColor" class="w-6 h-6 ml-2">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M19.5 8.25l-7.5 7.5-7.5-7.5" />
                      </svg>
                    </span>
                  </PopoverButton>
                </Popover>

                <Popover v-slot="{ open }" class="relative">
                  <PopoverButton :class="open ? '' : 'text-opacity-90'">

                    <span
                      class="inline-flex items-center justify-between px-4 py-2 text-sm font-medium text-white rounded-md bg-gradient-to-r from-orange-600 to-orange-400 hover:bg-gray-700 hover:text-white">
                      <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                        stroke="currentColor" class="w-6 h-6">
                        <path stroke-linecap="round" stroke-linejoin="round"
                          d="M13.5 16.875h3.375m0 0h3.375m-3.375 0V13.5m0 3.375v3.375M6 10.5h2.25a2.25 2.25 0 002.25-2.25V6a2.25 2.25 0 00-2.25-2.25H6A2.25 2.25 0 003.75 6v2.25A2.25 2.25 0 006 10.5zm0 9.75h2.25A2.25 2.25 0 0010.5 18v-2.25a2.25 2.25 0 00-2.25-2.25H6a2.25 2.25 0 00-2.25 2.25V18A2.25 2.25 0 006 20.25zm9.75-9.75H18a2.25 2.25 0 002.25-2.25V6A2.25 2.25 0 0018 3.75h-2.25A2.25 2.25 0 0013.5 6v2.25a2.25 2.25 0 002.25 2.25z" />
                      </svg>

                      <span class="ml-2">Apps</span>
                      <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                        stroke="currentColor" class="w-6 h-6 ml-2">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M19.5 8.25l-7.5 7.5-7.5-7.5" />
                      </svg>
                    </span>
                  </PopoverButton>
                  <transition enter-active-class="transition duration-200 ease-out"
                    enter-from-class="translate-y-1 opacity-0" enter-to-class="translate-y-0 opacity-100"
                    leave-active-class="transition duration-150 ease-in" leave-from-class="translate-y-0 opacity-100"
                    leave-to-class="translate-y-1 opacity-0">
                    <PopoverPanel
                      class="absolute left-0 top-auto z-30 w-[16rem] min-w-full mt-1 text-sm bg-white border border-gray-300 rounded shadow-m">
                      <span class="absolute top-0 left-0 w-3 h-3 ml-6 -mt-1 transform rotate-45 bg-white border"></span>
                      <div class="relative z-10 w-full py-1 bg-white rounded-lg shadow-lg ring-1 ring-black ring-opacity-5">
                        <ul class="list-reset">
                          <li
                            class="inline-flex items-center w-full px-4 transition-colors duration-100 cursor-pointer hover:bg-red-100 ">
                            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                              stroke="currentColor" class="w-6 h-6">
                              <path stroke-linecap="round" stroke-linejoin="round"
                                d="M6.75 3v2.25M17.25 3v2.25M3 18.75V7.5a2.25 2.25 0 012.25-2.25h13.5A2.25 2.25 0 0121 7.5v11.25m-18 0A2.25 2.25 0 005.25 21h13.5A2.25 2.25 0 0021 18.75m-18 0v-7.5A2.25 2.25 0 015.25 9h13.5A2.25 2.25 0 0121 11.25v7.5m-9-6h.008v.008H12v-.008zM12 15h.008v.008H12V15zm0 2.25h.008v.008H12v-.008zM9.75 15h.008v.008H9.75V15zm0 2.25h.008v.008H9.75v-.008zM7.5 15h.008v.008H7.5V15zm0 2.25h.008v.008H7.5v-.008zm6.75-4.5h.008v.008h-.008v-.008zm0 2.25h.008v.008h-.008V15zm0 2.25h.008v.008h-.008v-.008zm2.25-4.5h.008v.008H16.5v-.008zm0 2.25h.008v.008H16.5V15z" />
                            </svg>

                            <a href="#"
                              class="flex items-start w-full px-4 py-2 text-sm font-medium text-gray-900 no-underline transition-colors duration-100 cursor-pointer hover:bg-red-100 hover:no-underline">
                              <span class="flex-1">Calendar</span> </a>
                            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                              <path stroke-linecap="round" stroke-linejoin="round" d="M8.25 4.5l7.5 7.5-7.5 7.5" />
                            </svg>

                          </li>
                          <li
                            class="inline-flex items-center w-full px-4 transition-colors duration-100 cursor-pointer hover:bg-red-100 ">
                            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                              stroke="currentColor" class="w-6 h-6">
                              <path stroke-linecap="round" stroke-linejoin="round"
                                d="M10.125 2.25h-4.5c-.621 0-1.125.504-1.125 1.125v17.25c0 .621.504 1.125 1.125 1.125h12.75c.621 0 1.125-.504 1.125-1.125v-9M10.125 2.25h.375a9 9 0 019 9v.375M10.125 2.25A3.375 3.375 0 0113.5 5.625v1.5c0 .621.504 1.125 1.125 1.125h1.5a3.375 3.375 0 013.375 3.375M9 15l2.25 2.25L15 12" />
                            </svg>

                            <a href="#"
                              class="flex items-start w-full px-4 py-2 text-sm font-medium text-gray-900 no-underline transition-colors duration-100 cursor-pointer hover:bg-red-100 hover:no-underline">
                              <span class="flex-1">Invoice</span> </a>
                              <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                              <path stroke-linecap="round" stroke-linejoin="round" d="M8.25 4.5l7.5 7.5-7.5 7.5" />
                            </svg>
                          </li>
                          <li
                            class="relative inline-flex items-center w-full transition-colors duration-100 cursor-pointer hover:bg-red-100 "
                            @click="showChildren = !showChildren">
                            <span class="inline-flex items-center w-full px-4">
                              <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                                stroke="currentColor" class="w-6 h-6">
                                <path stroke-linecap="round" stroke-linejoin="round"
                                  d="M15 19.128a9.38 9.38 0 002.625.372 9.337 9.337 0 004.121-.952 4.125 4.125 0 00-7.533-2.493M15 19.128v-.003c0-1.113-.285-2.16-.786-3.07M15 19.128v.106A12.318 12.318 0 018.624 21c-2.331 0-4.512-.645-6.374-1.766l-.001-.109a6.375 6.375 0 0111.964-3.07M12 6.375a3.375 3.375 0 11-6.75 0 3.375 3.375 0 016.75 0zm8.25 2.25a2.625 2.625 0 11-5.25 0 2.625 2.625 0 015.25 0z" />
                              </svg>
  
                              <a href="#"
                                class="flex items-start w-full px-4 py-2 text-sm font-medium text-gray-900 no-underline transition-colors duration-100 cursor-pointer hover:bg-red-100 hover:no-underline">
                                <span class="flex-1">Users</span>
                                <span class="ml-2"> <i class="mdi mdi-chevron-right"></i> </span>
                              </a>
                              <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                                <path stroke-linecap="round" stroke-linejoin="round" d="M8.25 4.5l7.5 7.5-7.5 7.5" />
                              </svg>
                            </span>
                            <div
                              class="absolute top-0 z-30 w-56 min-w-full mt-1 text-sm transform translate-x-full bg-white border border-gray-300 rounded shadow-md inset-l-full"
                              v-show="showChildren" @mouseleave="showChildren = false">
                              <span
                                class="absolute top-0 left-0 w-3 h-3 mt-2 -ml-1 transform rotate-45 bg-white border"></span>
                              <div class="relative z-10 w-full py-1 bg-white rounded">
                                <ul class="list-reset">
                                  <li class="inline-flex items-center w-full px-4 transition-colors duration-100 cursor-pointer hover:bg-red-100">
                                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-3 h-3 rounded-full">
                                      <path stroke-linecap="round" stroke-linejoin="round" d="M5.25 7.5A2.25 2.25 0 017.5 5.25h9a2.25 2.25 0 012.25 2.25v9a2.25 2.25 0 01-2.25 2.25h-9a2.25 2.25 0 01-2.25-2.25v-9z" />
                                    </svg>

                                    <a href="#"
                                      class="flex items-start w-full px-4 py-2 no-underline transition-colors duration-100 cursor-pointer hover:bg-red-100 hover:no-underline">
                                      <span class="flex-1">List</span> </a>
                                  </li>
                                  <li class="inline-flex items-center w-full transition-colors duration-100 cursor-pointer hover:bg-red-100">
                                    <span class="inline-flex items-center w-full px-4 transition-colors duration-100 cursor-pointer hover:bg-red-100">
                                      <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-3 h-3 rounded-full">
                                      <path stroke-linecap="round" stroke-linejoin="round" d="M5.25 7.5A2.25 2.25 0 017.5 5.25h9a2.25 2.25 0 012.25 2.25v9a2.25 2.25 0 01-2.25 2.25h-9a2.25 2.25 0 01-2.25-2.25v-9z" />
                                    </svg>
                                    <a  v-on:mouseenter="showSubChildren = true"
                                      class="flex items-start w-full px-4 py-2 no-underline transition-colors duration-100 cursor-pointer hover:bg-red-100 hover:no-underline">
                                      <span class="flex-1">View</span> 
                                    </a></span>
                                      <div
                                        class="absolute top-0 z-30 w-56 min-w-full mt-8 text-sm transform translate-x-full bg-white border border-gray-300 rounded shadow-md inset-l-full"
                                        v-show="showSubChildren" @mouseleave="showSubChildren = false">
                                        <span
                                          class="absolute top-0 left-0 w-3 h-3 mt-2 -ml-1 transform rotate-45 bg-white border"></span>
                                        <div class="relative z-10 w-full py-1 bg-white rounded">
                                          <ul class="list-reset">
                                            <li class="inline-flex items-center w-full px-4 transition-colors duration-100 cursor-pointer hover:bg-red-100">
                                              <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-3 h-3 rounded-full">
                                                <path stroke-linecap="round" stroke-linejoin="round" d="M5.25 7.5A2.25 2.25 0 017.5 5.25h9a2.25 2.25 0 012.25 2.25v9a2.25 2.25 0 01-2.25 2.25h-9a2.25 2.25 0 01-2.25-2.25v-9z" />
                                              </svg>

                                              <a href="#"
                                                class="flex items-start w-full px-4 py-2 no-underline transition-colors duration-100 cursor-pointer hover:bg-red-100 hover:no-underline">
                                                <span class="flex-1">Account</span> </a>
                                            </li>
                                            <li class="inline-flex items-center w-full px-4 transition-colors duration-100 cursor-pointer hover:bg-red-100">
                                              <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-3 h-3 rounded-full">
                                                <path stroke-linecap="round" stroke-linejoin="round" d="M5.25 7.5A2.25 2.25 0 017.5 5.25h9a2.25 2.25 0 012.25 2.25v9a2.25 2.25 0 01-2.25 2.25h-9a2.25 2.25 0 01-2.25-2.25v-9z" />
                                              </svg>
                                              <a href="#"
                                                class="flex items-start w-full px-4 py-2 no-underline transition-colors duration-100 cursor-pointer hover:bg-red-100 hover:no-underline">
                                                <span class="flex-1">Security</span> </a>
                                            </li>
                                            <li class="inline-flex items-center w-full px-4 transition-colors duration-100 cursor-pointer hover:bg-red-100">
                                              <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-3 h-3 rounded-full">
                                                <path stroke-linecap="round" stroke-linejoin="round" d="M5.25 7.5A2.25 2.25 0 017.5 5.25h9a2.25 2.25 0 012.25 2.25v9a2.25 2.25 0 01-2.25 2.25h-9a2.25 2.25 0 01-2.25-2.25v-9z" />
                                              </svg>
                                              <a href="#"
                                                class="flex items-start w-full px-4 py-2 no-underline transition-colors duration-100 cursor-pointer hover:bg-red-100 hover:no-underline">
                                                <span class="flex-1">illing & Plans</span> </a>
                                            </li>
                                            <li class="inline-flex items-center w-full px-4 transition-colors duration-100 cursor-pointer hover:bg-red-100">
                                              <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-3 h-3 rounded-full">
                                                <path stroke-linecap="round" stroke-linejoin="round" d="M5.25 7.5A2.25 2.25 0 017.5 5.25h9a2.25 2.25 0 012.25 2.25v9a2.25 2.25 0 01-2.25 2.25h-9a2.25 2.25 0 01-2.25-2.25v-9z" />
                                              </svg>
                                              <a href="#"
                                                class="flex items-start w-full px-4 py-2 no-underline transition-colors duration-100 cursor-pointer hover:bg-red-100 hover:no-underline">
                                                <span class="flex-1">Notifications</span> </a>
                                            </li>
                                            <li class="inline-flex items-center w-full px-4 transition-colors duration-100 cursor-pointer hover:bg-red-100">
                                              <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-3 h-3 rounded-full">
                                                <path stroke-linecap="round" stroke-linejoin="round" d="M5.25 7.5A2.25 2.25 0 017.5 5.25h9a2.25 2.25 0 012.25 2.25v9a2.25 2.25 0 01-2.25 2.25h-9a2.25 2.25 0 01-2.25-2.25v-9z" />
                                              </svg>
                                              <a href="#"
                                                class="flex items-start w-full px-4 py-2 no-underline transition-colors duration-100 cursor-pointer hover:bg-red-100 hover:no-underline">
                                                <span class="flex-1">Connections</span> </a>
                                            </li>
                                          </ul>
                                        </div>
                                      </div>
                                  </li>
                                 
                                </ul>
                              </div>
                            </div>
                          </li>
                          <li
                            class="relative inline-flex items-center w-full px-4 transition-colors duration-100 cursor-pointer hover:bg-red-100 ">
                            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                              stroke="currentColor" class="w-6 h-6">
                              <path stroke-linecap="round" stroke-linejoin="round"
                                d="M10.343 3.94c.09-.542.56-.94 1.11-.94h1.093c.55 0 1.02.398 1.11.94l.149.894c.07.424.384.764.78.93.398.164.855.142 1.205-.108l.737-.527a1.125 1.125 0 011.45.12l.773.774c.39.389.44 1.002.12 1.45l-.527.737c-.25.35-.272.806-.107 1.204.165.397.505.71.93.78l.893.15c.543.09.94.56.94 1.109v1.094c0 .55-.397 1.02-.94 1.11l-.893.149c-.425.07-.765.383-.93.78-.165.398-.143.854.107 1.204l.527.738c.32.447.269 1.06-.12 1.45l-.774.773a1.125 1.125 0 01-1.449.12l-.738-.527c-.35-.25-.806-.272-1.203-.107-.397.165-.71.505-.781.929l-.149.894c-.09.542-.56.94-1.11.94h-1.094c-.55 0-1.019-.398-1.11-.94l-.148-.894c-.071-.424-.384-.764-.781-.93-.398-.164-.854-.142-1.204.108l-.738.527c-.447.32-1.06.269-1.45-.12l-.773-.774a1.125 1.125 0 01-.12-1.45l.527-.737c.25-.35.273-.806.108-1.204-.165-.397-.505-.71-.93-.78l-.894-.15c-.542-.09-.94-.56-.94-1.109v-1.094c0-.55.398-1.02.94-1.11l.894-.149c.424-.07.765-.383.93-.78.165-.398.143-.854-.107-1.204l-.527-.738a1.125 1.125 0 01.12-1.45l.773-.773a1.125 1.125 0 011.45-.12l.737.527c.35.25.807.272 1.204.107.397-.165.71-.505.78-.929l.15-.894z" />
                              <path stroke-linecap="round" stroke-linejoin="round" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
                            </svg>

                            <a href="#"
                              class="flex items-start w-full px-4 py-2 text-sm font-medium text-gray-900 no-underline transition-colors duration-100 cursor-pointer hover:bg-red-100 hover:no-underline">
                              <span class="flex-1">Roles & Permissions</span> </a>
                              <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                                <path stroke-linecap="round" stroke-linejoin="round" d="M8.25 4.5l7.5 7.5-7.5 7.5" />
                              </svg>
                          </li>
                        </ul>
                      </div>
                    </PopoverPanel>
                  </transition>
                </Popover>

                <Popover v-slot="{ open }" class="relative">
                  <PopoverButton :class="open ? '' : 'text-opacity-90'">
                    <span
                      class="inline-flex items-center justify-between px-4 py-2 text-sm font-medium text-gray-800 bg-gray-200 rounded-md hover:bg-gray-700 hover:text-white">
                      <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M19.5 14.25v-2.625a3.375 3.375 0 00-3.375-3.375h-1.5A1.125 1.125 0 0113.5 7.125v-1.5a3.375 3.375 0 00-3.375-3.375H8.25m2.25 0H5.625c-.621 0-1.125.504-1.125 1.125v17.25c0 .621.504 1.125 1.125 1.125h12.75c.621 0 1.125-.504 1.125-1.125V11.25a9 9 0 00-9-9z" />
                      </svg>
                      <span class="ml-2">Pages</span>
                      <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                        stroke="currentColor" class="w-6 h-6 ml-2">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M19.5 8.25l-7.5 7.5-7.5-7.5" />
                      </svg>
                    </span>
                  </PopoverButton>
                </Popover>

                <Popover v-slot="{ open }" class="relative">
                  <PopoverButton :class="open ? '' : 'text-opacity-90'">
                    <span
                      class="inline-flex items-center justify-between px-4 py-2 text-sm font-medium text-gray-800 bg-gray-200 rounded-md hover:bg-gray-700 hover:text-white">
                      <img class="w-6 h-6" src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAYAAAAeP4ixAAAACXBIWXMAAAsTAAALEwEAmpwYAAACVklEQVR4nO2YwWoUQRCGv9l4y8ZXMEFwPS57EEFUPGlyU5OLghAleQ3x5E1F8hoh5AHWqCT4BK7rSUwiaBIiulHZ00qHf6AZ4uxsz1QwoX9o2J6Z/mqmt7q6qiEqKioqKioq6sSqBTwB1oAPwAEwMGoHsrEmm852KSXALNA1fOmirQvc1TuNpCngnQf6DLwEbgINYFytoWvu3qb3/BsxQjSew90AJouCrgDfNHALWATGCoyrAXPAJ439DlwL/Jg87h5wgyFyhvsasKzZGVV1YEWMP8D1AMYwbj9vkpwr7OrBZyH+mJnF52LtA+dLsP7F3TnKfRNvTSxrQFnVvBl8WxEzy93ITvisbmwGulOeO2yLfd+Ieye9mHghdp7q9UjsTkl3zeMequWF2CLRaVSNKfo5G5eNuE20ew4Us620JBtPjbiPUSrgOrew07RstC25H9W5gJ0asrFtxO26Tk8dFwmsVPc2SAtuz3V+HsOHnJWNX0bcH6fKtV4dw2KfMVrsMz731ITflpeeWGyIZ7yN65IRt5lNUR5SvRbEfl9xirKQTVFQGZkWUlVGrwngi9j3jLi3/RuJUuKBUuSq0vhVr/StMo1fFXf9qAcmVawMVLyUMezGvvBK09D6PY/r3vUcBUrdlUA3m/Bm7DdwNYAxjNsvwnWHD1+9DWxREaLIbD3wfHe/oo+oZbiFDh9STXlrJg3NS8o2L+qfquv3tO6lodC113l/+xDVc7jrIdxEZWTnPzig62SjU6ia2j3bOs5MM2aL1pONtmwebnZRUVFRUVFRUZw8/QXaPTbSlRTPtwAAAABJRU5ErkJggg==">
                      <span class="ml-2">Components</span>
                      <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                        stroke="currentColor" class="w-6 h-6 ml-2">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M19.5 8.25l-7.5 7.5-7.5-7.5" />
                      </svg>
                    </span>
                  </PopoverButton>
                </Popover>

                <Popover v-slot="{ open }" class="relative">
                  <PopoverButton :class="open ? '' : 'text-opacity-90'">
                    <span
                      class="inline-flex items-center justify-between px-4 py-2 text-sm font-medium text-gray-800 bg-gray-200 rounded-md hover:bg-gray-700 hover:text-white">
                      <span>Forms</span>
                      <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                        stroke="currentColor" class="w-6 h-6 ml-2">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M19.5 8.25l-7.5 7.5-7.5-7.5" />
                      </svg>
                    </span>
                  </PopoverButton>
                </Popover>
                <Popover v-slot="{ open }" class="relative">
                  <PopoverButton :class="open ? '' : 'text-opacity-90'">
                    <span
                      class="inline-flex items-center justify-between px-4 py-2 text-sm font-medium text-gray-800 bg-gray-200 rounded-md hover:bg-gray-700 hover:text-white">
                      <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M3.75 6A2.25 2.25 0 016 3.75h2.25A2.25 2.25 0 0110.5 6v2.25a2.25 2.25 0 01-2.25 2.25H6a2.25 2.25 0 01-2.25-2.25V6zM3.75 15.75A2.25 2.25 0 016 13.5h2.25a2.25 2.25 0 012.25 2.25V18a2.25 2.25 0 01-2.25 2.25H6A2.25 2.25 0 013.75 18v-2.25zM13.5 6a2.25 2.25 0 012.25-2.25H18A2.25 2.25 0 0120.25 6v2.25A2.25 2.25 0 0118 10.5h-2.25a2.25 2.25 0 01-2.25-2.25V6zM13.5 15.75a2.25 2.25 0 012.25-2.25H18a2.25 2.25 0 012.25 2.25V18A2.25 2.25 0 0118 20.25h-2.25A2.25 2.25 0 0113.5 18v-2.25z" />
                      </svg>

                      <span class="ml-2">Tables</span>
                      <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                        stroke="currentColor" class="w-6 h-6 ml-2">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M19.5 8.25l-7.5 7.5-7.5-7.5" />
                      </svg>
                    </span>
                  </PopoverButton>
                </Popover>
                <Popover v-slot="{ open }" class="relative">
                  <PopoverButton :class="open ? '' : 'text-opacity-90 w-full'">
                    <span
                      class="inline-flex items-center justify-between px-4 py-2 text-sm font-medium text-gray-800 bg-gray-200 rounded-md hover:bg-gray-700 hover:text-white">
                      <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M3 13.125C3 12.504 3.504 12 4.125 12h2.25c.621 0 1.125.504 1.125 1.125v6.75C7.5 20.496 6.996 21 6.375 21h-2.25A1.125 1.125 0 013 19.875v-6.75zM9.75 8.625c0-.621.504-1.125 1.125-1.125h2.25c.621 0 1.125.504 1.125 1.125v11.25c0 .621-.504 1.125-1.125 1.125h-2.25a1.125 1.125 0 01-1.125-1.125V8.625zM16.5 4.125c0-.621.504-1.125 1.125-1.125h2.25C20.496 3 21 3.504 21 4.125v15.75c0 .621-.504 1.125-1.125 1.125h-2.25a1.125 1.125 0 01-1.125-1.125V4.125z" />
                      </svg>

                      <span class="ml-2">Charts&Maps</span>
                      <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                        stroke="currentColor" class="w-6 h-6 ml-2">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M19.5 8.25l-7.5 7.5-7.5-7.5" />
                      </svg>
                    </span>
                  </PopoverButton>
                </Popover>
                <Popover v-slot="{ open }" class="relative">
                  <PopoverButton :class="open ? '' : 'text-opacity-90'">
                    <span
                      class="inline-flex items-center justify-between px-4 py-2 text-sm font-medium text-gray-800 bg-gray-200 rounded-md hover:bg-gray-700 hover:text-white">
                      <span>Misc</span>
                      <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                        stroke="currentColor" class="w-6 h-6 ml-2">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M19.5 8.25l-7.5 7.5-7.5-7.5" />
                      </svg>
                    </span>
                  </PopoverButton>
                </Popover>
              
              </nav>

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
  Popover, PopoverButton, PopoverPanel, PopoverGroup,
  TransitionChild,
  TransitionRoot,
  DialogTitle,
  Disclosure, DisclosureButton, DisclosurePanel, Menu, MenuButton, MenuItem, MenuItems
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
const showChildren = ref(false)
const showSubChildren = ref(false)



const user = {
  name: 'Tom Cook',
  email: 'tom@example.com',
  imageUrl:
    'https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80',
}

const userNavigation = [
  { name: 'Your Profile', href: '#' },
  { name: 'Settings', href: '#' },
  { name: 'Sign out', href: '#' },
]

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
  {
    name: 'Dashboard', href: '#', icon: HomeIcon, current: true,
    submenu: {
      name: 'Item 1', href: '#', icon: HomeIcon, current: true,
      name: 'Item 1', href: '#', icon: HomeIcon, current: false,
      name: 'Item 1', href: '#', icon: HomeIcon, current: false,
      submenu: {
        name: 'Item 1', href: '#', icon: HomeIcon, current: true,
        name: 'Item 1', href: '#', icon: HomeIcon, current: false,
        name: 'Item 1', href: '#', icon: HomeIcon, current: false,
      }
    }
  },
  { name: 'Layout', href: '#', icon: HomeIcon, current: false },
  { name: 'Apps', href: '#', icon: HomeIcon, current: false },
  { name: 'Pages', href: '#', icon: HomeIcon, current: false },
  { name: 'Components', href: '#', icon: HomeIcon, current: false },
  { name: 'Forms', href: '#', icon: HomeIcon, current: false },
  { name: 'Tables', href: '#', icon: HomeIcon, current: false },
  { name: 'Charts & Maps', href: '#', icon: HomeIcon, current: false },
  { name: 'Misc', href: '#', icon: HomeIcon, current: false },
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

<style>.submenu {
  translate: 100% 105px 5rem;
  z-index: 9999;
}</style>