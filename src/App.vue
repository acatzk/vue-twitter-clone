<template>
  <div id="app" class="flex container h-screen w-full">
    <!-- SideBar -->
    <side-bar>

      <template #twitter-logo>
        <button class="h-12 w-12 hover:bg-blue-100 text-3xl rounded-full text-blue-500 focus:outline-none ml-2">
          <i class="fab fa-twitter"></i>
        </button> 
      </template> <!-- TWITTER ICON STYLE -->

      <template #twitter-tabs>
        <button 
          v-for="tab in tabs" :key="tab.id"
          :class="`flex items-center py-2 px-4 hover:bg-blue-100 rounded-full mr-auto focus:outline-none mb-3 text-gray-800 ${ id === tab.id ? 'text-blue-500' : ''}`"
          @click="id = tab.id"
        >
          <i :class="`${tab.icon} text-2xl mr-4 text-left`"></i>
          <p class="text-lg font-semibold text-left hidden lg:block">{{ tab.title }}</p>
        </button> 
      </template> <!-- TWITTER NAVIGATION STYLE -->

      <template #twitter-button>
        <button class="text-white bg-blue-500 rounded-full font-semibold focus:outline-none w-12 h-12 lg:h-auto lg:w-full p-3 hover:bg-blue-600">
          <p class="hidden lg:block">Tweet</p>
          <i class="fa fa-plus lg:hidden"></i>
        </button> 
      </template> <!-- TWEET BUTTON -->

      <template #twitter-avatar>
        <button 
          class="lg:w-full flex items-center focus:outline-none hover:bg-gray-100 rounded-full p-2"
          @click="dropdown = !dropdown"
        >
          <img 
            src="https://avatars0.githubusercontent.com/u/38458781?s=460&u=f62c697c75225996d2b9ed5c8bd755cbaa19f2db&v=4" 
            alt="profile"
            class="w-10 h-10 rounded-full border border-gray-600"
          >
          <div class="hidden lg:block ml-4">
            <p class="text-sm font-bold leading-tight text-gray-800">Joshua Galit</p>
            <p class="text-sm leading-tight text-gray-800">@angryboy</p>
          </div>
          <i class="hidden lg:block fas fa-angle-down ml-auto text-lg"></i>
        </button> <!-- USER AVATAR -->

        <div 
          v-if="dropdown"
          class="absolute bottom-0 left-0 w-full rounded-lg shadow-md border bg-white mb-16"
        >
          <button 
            class="p-3 w-full flex items-center focus:outline-none hover:bg-gray-100"
            @click="dropdown = false"
          >
            <img 
              src="https://avatars0.githubusercontent.com/u/38458781?s=460&u=f62c697c75225996d2b9ed5c8bd755cbaa19f2db&v=4" 
              alt="profile"
              class="w-10 h-10 rounded-full border border-gray-600"
            >
            <div class="ml-4">
              <p class="text-sm font-bold leading-tight text-gray-800">Joshua Galit</p>
              <p class="text-sm leading-tight text-gray-800">@angryboy</p>
            </div>
            <i class="fas fa-check ml-auto text-blue-500"></i>
          </button>
          <button 
            class="w-full text-left hover:bg-gray-200 border-t border-gray-100 focus:outline-none text-sm p-3"
            @click="dropdown = false"
          >
            Add an existing account
          </button>
          <button 
            class="w-full text-left hover:bg-gray-200 border-t border-gray-100 focus:outline-none text-sm p-3"
            @click="dropdown = false"
          >
            Log out @angryboy
          </button>
        </div> <!-- DROP DOWN PROFILE IMAGE -->

      </template>

    </side-bar>

  </div>
</template>

<script>
  export default {
    name: 'app',

    components: {
      SideBar: () => import('@/components/SideBar')
    },

    data () {
      return {
        tabs: [
          {icon: 'fas fa-home', title: 'Home', id:'home'},
          {icon: 'fas fa-hashtag', title: 'Explore', id: 'explore'},
          {icon: 'far fa-bell', title: 'Notifications', id: 'notifications'},
          {icon: 'far fa-envelope', title: 'Messages', id: 'messages'},
          {icon: 'far fa-bookmark', title: 'Bookmarks', id: 'bookmarks'},
          {icon: 'fas fa-clipboard-list', title: 'Lists', id: 'lists'},
          {icon: 'far fa-user', title: 'Profile', id: 'profile'},
          {icon: 'fas fa-ellipsis-h', title: 'More', id: 'more'}
        ],
        dropdown: false,
        id: 'home'
      }
    }
  }
</script>

<style lang="scss"></style>
