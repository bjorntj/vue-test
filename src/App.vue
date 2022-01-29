<template>
  <div id="main">
    <TransitionRoot as="template" :show="sidebarOpen">
      <Dialog as="div" class="fixed inset-0 flex z-40 md:hidden" @close="sidebarOpen = false">
        <TransitionChild as="template" enter="transition-opacity ease-linear duration-300" enter-from="opacity-0" enter-to="opacity-100" leave="transition-opacity ease-linear duration-300" leave-from="opacity-100" leave-to="opacity-0">
          <DialogOverlay class="fixed inset-0 bg-gray-600 bg-opacity-75"/>
        </TransitionChild>
        <TransitionChild as="template" enter="transition ease-in-out duration-300 transform" enter-from="-translate-x-full" enter-to="translate-x-0" leave="transition ease-in-out duration-300 transform" leave-from="translate-x-0" leave-to="-translate-x-full">
          <div class="relative flex-1 flex flex-col max-w-xs w-full pt-5 pb-4 bg-gray-900">
            <TransitionChild as="template" enter="ease-in-out duration-300" enter-from="opacity-0" enter-to="opacity-100" leave="ease-in-out duration-300" leave-from="opacity-100" leave-to="opacity-0">
              <div class="absolute top-0 right-0 -mr-12 pt-2">
                <button type="button" class="ml-1 flex items-center justify-center h-10 w-10 rounded-full focus:outline-none focus:ring-2 focus:ring-inset focus:ring-white" @click="sidebarOpen = false">
                  <span class="sr-only">Close sidebar</span>
                  <XIcon class="h-6 w-6 text-white" aria-hidden="true"/>
                </button>
              </div>
            </TransitionChild>
            <div class="flex-shrink-0 flex items-center px-4">
              <img src="@/assets/HC.png" alt="Havleik Consulting"/>
            </div>
            <div class="mt-5 flex-1 h-0 overflow-y-auto">
              <nav class="px-2 space-y-1" v-if="loggedIn">
                <nav-link
                  :to="{ name: 'Home' }"
                  @click.native="sidebarOpen = false"
                  :navicon="homeIcon">
                  Home
                </nav-link>
                <nav-link
                  :to="{ name: 'About' }"
                  @click.native="sidebarOpen = false"
                  :navicon="usersIcon">
                  About
                </nav-link>
              </nav>
            </div>
          </div>
        </TransitionChild>
        <div class="flex-shrink-0 w-14" aria-hidden="true">
          <!-- Dummy element to force sidebar to shrink to fit close icon -->
        </div>
      </Dialog>
    </TransitionRoot>

    <!-- Static sidebar for desktop -->
    <div class="hidden md:flex md:w-64 md:flex-col md:fixed md:inset-y-0" >
      <!-- Sidebar component, swap this element with another sidebar if you like -->
      <div class="flex-1 flex flex-col min-h-0 bg-gray-900">
        <div class="flex items-center h-16 flex-shrink-0 px-4 bg-white">
          <img class="h-8 w-auto" src="@/assets/HC.png" alt="Havleik Consulting"/>
        </div>
        <div class="flex-1 flex flex-col overflow-y-auto" >
          <nav class="flex-1 px-2 py-4 space-y-1" >
            <nav-link
              :to="{ name: 'Home' }"
              :navicon="homeIcon">
              Home
            </nav-link>
            <nav-link
              :to="{ name: 'About' }"
              @click.native="sidebarOpen = false"
              :navicon="usersIcon">
              About
            </nav-link>
          </nav>
        </div>
      </div>
    </div>
    <div class="md:pl-64 flex flex-col">
      <div class="sticky top-0 z-10 flex-shrink-0 flex h-16 bg-white dark:bg-gray-900 shadow">
        <button type="button" class="px-4 border-r border-gray-200 dark:border-gray-500 text-gray-500 focus:outline-none focus:ring-2 focus:ring-inset focus:ring-indigo-500 md:hidden" @click="sidebarOpen = true">
          <span class="sr-only">Open sidebar</span>
          <MenuAlt2Icon class="h-6 w-6" aria-hidden="true"/>
        </button>
        <div class="flex-1 px-4 flex justify-between">
          <div class="flex-1 flex">
            <div class="relative w-full text-gray-800 dark:text-gray-400 focus-within:text-gray-600">
              <div class="absolute inset-y-0 left-0 flex items-center pointer-events-none text-lg sm:text-2xl text-xs font-bold">
                <div class="flex items-baseline">
                  Title
                  <div class="ml-4 text-xs text-gray-300 dark:text-gray-700">
                    v.{{ appVersion }}
                  </div>
                </div>
              </div>
            </div>
            <!--            <form class="w-full flex md:ml-0" action="#" method="GET">
                          <label for="search-field" class="sr-only">Search</label>
                          <div class="relative w-full text-gray-400 focus-within:text-gray-600">
                            <div class="absolute inset-y-0 left-0 flex items-center pointer-events-none">
                              <SearchIcon class="h-5 w-5" aria-hidden="true" />
                            </div>
                            <input id="search-field" class="block w-full h-full pl-8 pr-3 py-2 border-transparent text-gray-900 placeholder-gray-500 focus:outline-none focus:placeholder-gray-400 focus:ring-0 focus:border-transparent sm:text-sm" placeholder="Search" type="search" name="search" />
                          </div>
                        </form>-->
          </div>
          <div class="ml-4 flex items-center md:ml-6">
            <!--            <button type="button" class="bg-white p-1 rounded-full text-gray-400 hover:text-gray-500 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
                          <span class="sr-only">View notifications</span>
                          <BellIcon class="h-6 w-6" aria-hidden="true" />
                        </button>-->

            <!-- Profile dropdown -->
            <Menu as="div" class="ml-3 relative">
              <div class="flex">
                <MenuButton class="max-w-xs bg-white flex items-center text-sm rounded-full focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
                  <span class="sr-only">Open user menu</span>
                  <!--                  <img class="h-8 w-8 rounded-full" src="https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80" alt=""/>-->
                  <img class="h-8 w-8 rounded-full" :src="gravatar" alt=""/>
                </MenuButton>
                <div class="ml-3">
                  <p class="text-xs font-light text-gray-700 dark:text-gray-200 mr-6">
                    {{ fullname }}
                  </p>
                </div>
              </div>
              <transition enter-active-class="transition ease-out duration-100" enter-from-class="transform opacity-0 scale-95" enter-to-class="transform opacity-100 scale-100" leave-active-class="transition ease-in duration-75" leave-from-class="transform opacity-100 scale-100" leave-to-class="transform opacity-0 scale-95">
                <MenuItems class="origin-top-right absolute right-0 mt-2 w-48 rounded-md shadow-lg py-1 bg-white dark:bg-gray-900 ring-1 ring-black ring-opacity-5 focus:outline-none" >
                  <!--                  <MenuItem v-for="item in userNavigation" :key="item.name" v-slot="{ active }">
                                      <router-link :to="{ name: item.href }" @click.native="profiles(item.href)" :class="[active ? 'bg-gray-100 dark:bg-gray-600' : '', 'block px-4 py-2 text-sm text-gray-700 dark:text-gray-100']">{{ item.name }}</router-link>
                                    </MenuItem>-->
                  <MenuItem v-slot="{ active }">
                    <router-link :to="{ name: 'Profile' }" @click.native="profiles('Profile')" :class="[active ? 'bg-gray-100 dark:bg-gray-600' : '', 'block px-4 py-2 text-sm text-gray-700 dark:text-gray-100']">
                      <span class="flex gap-3">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6V4m0 2a2 2 0 100 4m0-4a2 2 0 110 4m-6 8a2 2 0 100-4m0 4a2 2 0 110-4m0 4v2m0-6V4m6 6v10m6-2a2 2 0 100-4m0 4a2 2 0 110-4m0 4v2m0-6V4" />
                        </svg>
                        Profile
                      </span>
                    </router-link>
                  </MenuItem>
                  <MenuItem v-slot="{ active }">
                    <span @click="toggleTheme()" :class="[active ? 'bg-gray-100 dark:bg-gray-600' : '', 'block px-4 py-2 text-sm text-gray-700 dark:text-gray-100']" class="flex gap-3">
                      <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z" />
                      </svg>
                      Toogle
                    </span>
                  </MenuItem>
                  <MenuItem v-slot="{ active }">
                    <span @click="localeEN()" :class="[active ? 'bg-gray-100 dark:bg-gray-600' : '', 'block px-4 py-2 text-sm text-gray-700 dark:text-gray-100']" class="flex gap-3">
                      <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5h12M9 3v2m1.048 9.5A18.022 18.022 0 016.412 9m6.088 9h7M11 21l5-10 5 10M12.751 5C11.783 10.77 8.07 15.61 3 18.129" />
                      </svg>
                      English
                    </span>
                  </MenuItem>
                  <MenuItem v-slot="{ active }">
                    <span @click="localeNO()" :class="[active ? 'bg-gray-100 dark:bg-gray-600' : '', 'block px-4 py-2 text-sm text-gray-700 dark:text-gray-100']" class="flex gap-3">
                      <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5h12M9 3v2m1.048 9.5A18.022 18.022 0 016.412 9m6.088 9h7M11 21l5-10 5 10M12.751 5C11.783 10.77 8.07 15.61 3 18.129" />
                      </svg>
                      Norsk
                    </span>
                  </MenuItem>
                  <MenuItem v-slot="{ active }">
                    <span @click="profiles('Signout')" :class="[active ? 'bg-gray-100 dark:bg-gray-600' : '', 'block px-4 py-2 text-sm text-gray-700 dark:text-gray-100']" class="flex gap-3">
                      <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 16l4-4m0 0l-4-4m4 4H7m6 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h4a3 3 0 013 3v1" />
                      </svg>
                      Sign out
                    </span>
                  </MenuItem>
                </MenuItems>
              </transition>
            </Menu>
          </div>
        </div>
      </div>

      <main class="flex-1">
        <div class="py-6">
          <!--          <div class="max-w-7xl mx-auto px-4 sm:px-6 md:px-8">
                      <h1 class="text-2xl font-semibold text-gray-900 dark:text-gray-100">Dashboard</h1>
                    </div>-->
          <div class="max-w-8xl mx-auto px-4 sm:px-6 md:px-8 dark:text-gray-100 mt-4 z-0 relative">
            <div class="flex justify-center">
<!--              <loader class="absolute z-50"/>-->
            </div>
            <div class="flex justify-center">
<!--              <snack class="absolute z-50"/>-->
            </div>
            <router-view/>
          </div>
        </div>
      </main>
    </div>
  </div>
</template>

<script>
import {
  Dialog,
  DialogOverlay,
  Menu,
  MenuButton,
  MenuItem,
  MenuItems,
  TransitionChild,
  TransitionRoot,
} from '@headlessui/vue'
import {
  BellIcon,
  CalendarIcon,
  ChartBarIcon,
  FolderIcon,
  HomeIcon,
  InboxIcon,
  MenuAlt2Icon,
  UsersIcon,
  XIcon,
  ViewListIcon,
  InformationCircleIcon
} from '@heroicons/vue/outline'
import { SearchIcon } from '@heroicons/vue/solid'
/*import Loader from "@/components/Loader";
import Snack from "@/components/Snack";*/
import NavLink from "@/components/NavLink";
import { computed, ref } from "vue";

export default {
  name: 'MainLayout',
  components: {
    Dialog,
    DialogOverlay,
    Menu,
    MenuButton,
    MenuItem,
    MenuItems,
    TransitionChild,
    TransitionRoot,
    BellIcon,
    MenuAlt2Icon,
    SearchIcon,
    XIcon,
    ViewListIcon,
    InformationCircleIcon,
    NavLink
  },
  setup() {
    const sidebarOpen = ref(false);

    //const store = useStore();

    const gravatar = computed(() => '')
    const loggedIn = computed(() => true)
    const fullname = computed(() => 'Bjørn T Johansen')
    const homeIcon = computed(() => InformationCircleIcon())
    const viewListIcon = computed(() => ViewListIcon())
    const usersIcon = computed(() => UsersIcon())
    //const documentIcon = computed(() => DocumentIcon())
    const appVersion = computed(() => '1.0.0')
    const appTitle = computed(() => 'App Title')

    const profiles = (name) => {
      /*if (name === 'Signout') {
        console.log('Signout');
        store.dispatch('authModule/logout');
      } else {
        store.commit('setLoading', true);
      }*/
    }

    const toggleTheme = () => {
      /*store.dispatch('themeModule/toggleTheme');*/
    }

    return {
      sidebarOpen,
      gravatar,
      loggedIn,
      fullname,
      homeIcon,
      viewListIcon,
      usersIcon,
      appVersion,
      profiles,
      toggleTheme,
      appTitle
    }
  },
}
</script>

<style>

</style>
