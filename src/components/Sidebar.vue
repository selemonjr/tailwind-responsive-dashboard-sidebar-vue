<script>
export default {
    name:"Sidebar",
    data() {
        return {
            windowWidth:null,
            mobileNav:null,
            mobile:null,
        }
    },
        mounted() {
        window.addEventListener("resize",this.checkScreenSize);
        return this.checkScreenSize()
    },
    methods: {
         handleRotate() {
        this.mobileNav = !this.mobileNav;
    },
    checkScreenSize() {
        this.windowWidth = window.innerWidth;
        if(this.windowWidth <= 766) {
            this.mobile = true;
        } else {
            this.mobileNav = false;
            this.mobile = false;
        }
    }
    },
    setup() {
        let sidebarMenu = [
  {
    label: "Menu",
    children: [
      { name: "Discover", path: "/"},
      { name: "Trending", path: "/about" },
      { name: "Streaming", path: "/"},
      { name: "Playlist", path: "/" },
      { name: "Bookmark", path: "/"},
    ],
  },
  {
    label: "Category",
    children: [
      { name: "Live Stream", path: "/"},
      { name: "Tutorial", path: "/" },
      { name: "Competition", path: "/"},
      { name: "Community", path: "/" },
    ],
  },
];
        return {
            sidebarMenu
        }
    }
    }
</script>
<template>
<div>
      <div v-show="mobile" v-cloak class="absolute z-10 right-2 top-2 " :class="{'bar-rotate':mobileNav}"  @click="handleRotate()" >
      <div class="bar1"></div>
      <div class="bar2"></div>
      <div class="bar3"></div>
    </div>
    <div>
      <div class="px-8 pt-2 -mt-10 divide-y divide-gray-800" v-show="!mobile">
    <div v-for="group in sidebarMenu" :key="group.name" class="py-10">
      <span class="tracking-widest text-gray-500 uppercase text-xxs">{{ group.label }}</span>
      <ul class="flex flex-col pt-5 space-y-8">
        <li v-for="menu in group.children" :key="menu.name" class="flex items-center space-x-4 group">
          <span class="p-2 text-gray-500 bg-gray-800 rounded-xl group-hover:text-white group-hover:bg-orange">
            <component class="fill-current" :is="menu.icon" />
          </span>
          <router-link :to="menu.path"><a class="text-md text-gray-500 group-hover:text-white group-hover:font-semibold" href="#">{{ menu.name }}</a></router-link>
        </li>
      </ul>
    </div>
  </div>
  </div>

  <transition name="slide">
      <div class="min-h-screen inset-y-0 overflow-auto bg-gray-900 fixed">
        <div class="px-8 pt-2 -mt-10" v-show="mobileNav">
    <h2 class="tracking-widest text-red-500 uppercase text-xxs py-10 font-bold">Sidebar</h2>
    <div v-for="group in sidebarMenu" :key="group.name" class="py-5 -mt-10 mb-7">
      <span class="tracking-widest text-gray-500 uppercase text-xxs">{{ group.label }}</span>
      <ul class="flex flex-col pt-5 space-y-5">
        <li v-for="menu in group.children" :key="menu.name" class="flex items-center space-x-4 group">
          <span class="p-2 text-gray-500 bg-gray-800 rounded-xl group-hover:text-white group-hover:bg-orange">
            <component class="fill-current" :is="menu.icon" />
          </span>
            <router-link :to="menu.path"><a class="text-md text-gray-500 group-hover:text-white group-hover:font-semibold" href="#">{{ menu.name }}</a></router-link>
        </li>
      </ul>
    </div>
  </div>
  </div>
  </transition>
  </div>
</template>
<style scoped>
.bar1,.bar2,.bar3 {
    margin: 5px;
    width: 35px;
    z-index:10;
    height: 3px;
    background-color: #fff;
    transition: all 300ms cubic-bezier(.84,.06,.52,1.8);
}
.bar-rotate .bar1{
  transform: rotate(40deg) translate(10px,3px);
}
.bar-rotate .bar2 {
  opacity:0;
}
.bar-rotate .bar3{
  transform: rotate(-45deg) translate(9px,-2px);
}
.slide-enter-from,
.slide-leave-to {
    opacity:0;
}
.slide-enter-active,
.slide-leave-active {
    transition:opacity .5s;
}
</style>