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
          v-for="(tab, index) in tabs" :key="index"
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


    <!-- Tweets -->
    <main-bar>

      <template #home-title>
        <h1 class="text-xl font-bold">Home</h1>
        <i class="far fa-star text-xl text-blue-500"></i>
      </template>

      <template #tweet-field>
        <div class="flex-none">
          <img 
            src="https://avatars0.githubusercontent.com/u/38458781?s=460&u=f62c697c75225996d2b9ed5c8bd755cbaa19f2db&v=4" 
            alt="profile"
            class="w-12 h-12 rounded-full border border-gray-300"
          />
        </div>
        <form 
          class="w-full px-4 relative"
          @submit.prevent="onTweetStatus"
        >
          <textarea 
            placeholder="What's on your mind?" 
            class="mt-3 pb-3 w-full focus:outline-none"
            v-model="tweet.content"
          ></textarea>
          <div class="flex items-center">
            <i class="text-lg text-blue-500 mr-4 far fa-image"></i>
            <i class="text-lg text-blue-500 mr-4 fas fa-film"></i>
            <i class="text-lg text-blue-500 mr-4 far fa-chart-bar"></i>
            <i class="text-lg text-blue-500 mr-4 far fa-smile"></i>
          </div>
          <button 
            type="submit"
            class="h-10 px-4 text-white font-semibold bg-blue-500 hover:bg-blue-600 focus:outline-none rounded-full absolute bottom-0 right-0"
            @click.prevent="onTweetStatus"
          >
            Tweet
          </button>
        </form>
      </template>

      <template #tweet-user-fresh-post>
        <div 
          v-for="(tweet, index) in tweets" :key="index"
          class="w-full p-4 border-b hover:bg-lighter flex"
        >
          <div class="flex-none mr-4">
            <img src="https://avatars0.githubusercontent.com/u/38458781?s=460&u=f62c697c75225996d2b9ed5c8bd755cbaa19f2db&v=4" class="h-12 w-12 rounded-full flex-none"/>
          </div>
          <div class="w-full">
            <div class="flex items-center w-full">
              <p class="font-semibold"> Joshua galit </p>
              <p class="text-sm  text-gray-800 ml-2"> @angryboy </p>
              <p class="text-sm  text-gray-800 ml-2"> 1 sec </p>
              <i class="fas fa-angle-down  text-gray-800 ml-auto"></i>
            </div>
            <p class="py-2">
              {{ tweet.content }}
            </p>
            <div class="flex items-center justify-between w-full">
              <div class="flex items-center text-sm text-dark">
                <i class="far fa-comment mr-3"></i>
                <p> 0 </p>
              </div>
              <div class="flex items-center text-sm text-gray-800">
                <i class="fas fa-retweet mr-3"></i>
                <p> 0 </p>
              </div>
              <div class="flex items-center text-sm text-gray-800">
                <i class="fas fa-heart mr-3"></i>
                <p> 1 </p>
              </div>
              <div class="flex items-center text-sm text-gray-800">
                <i class="fas fa-share-square mr-3"></i>
              </div>
            </div>
          </div>
        </div>
      </template>

      <template #tweet-posts>
        <div 
          class="w-full p-4 border-b hover:bg-blue-100 flex"
          v-for="(follow, index) in following" :key="index"
        >
          <div class="flex-none mr-4">
            <img 
              :src="follow.src" 
              alt="profile" 
              class="w-12 h-12 rounded-full border border-gray-300 flex-none"
            >
          </div>
          <div class="w-full">
            <div class="flex items-center w-full">
              <p class="font-semibold">{{ follow.name }}</p>
              <p class="text-sm text-gray-800 ml-2">{{ follow.handle }}</p>
              <p class="text-sm text-gray-800 ml-2">{{ follow.time }}</p>
              <i class="fas fa-angle-down  text-gray-800 ml-auto"></i>
            </div>
            <p class="py-2">
              {{ follow.tweet }}
            </p>
            <div class="flex items-center justify-between w-full">
              <div class="flex items-center text-sm text-gray-800">
                <i class="far fa-comment mr-3"></i>
                <p>{{ follow.comments }}</p>
              </div>
              <div class="flex items-center text-sm text-gray-800">
                <i class="fas fa-retweet mr-3"></i>
                <p>{{ follow.retweets }}</p>
              </div>
              <div class="flex items-center text-sm text-gray-800">
                <i class="fas fa-heart mr-3"></i>
                <p>{{ follow.like }}</p>
              </div>
              <div class="flex items-center text-sm text-gray-800">
                <i class="fas fa-share-square mr-3"></i>
              </div>
            </div>
          </div>
        </div>
      </template>
    </main-bar>

    <!-- Trending -->
    <trending-section>
      <template #twitter-search>
        <input class="pl-12 rounded-full w-full p-2 bg-gray-300 focus:outline-none text-sm" placeholder="Search Twitter" />
		    <i class="fas fa-search absolute left-0 top-0 mt-5 ml-12 text-sm text-gray-500"></i>
      </template>
      <template #trending-title>
        <p class="text-lg font-bold text-gray-800">Trends For You</p>
				<i class="fas fa-cog text-lg text-blue-500"></i>
      </template>
      <template #trending-list>
        <button 
          v-for="(trend, index) in trending" :key="index"
          class="w-full flex justify-between hover:bg-gray-500 p-3 border-t border-gray-300 focus:outline-none"
        >
					<div>
						<p class="text-sm text-left leading-tight text-gray-700">{{ trend.top }}</p>
            <p class="font-bold text-left leading-tight text-gray-800">{{ trend.title }}</p>
            <p class="text-left leading-tight">{{ trend.bottom }}</p>
					</div>
          <i class="fas fa-angle-down text-lg"></i>
				</button>
        <button class="p-3 w-full hover:bg-gray-500 text-left text-blue-500 border-t border-gray-500 focus:outline-none">
          Show More
        </button>
      </template>

      <template #user-title>
        <p class="text-lg font-bold text-gray-800">Who To Follow</p>
      </template>
      <template #user-list>
        <button 
          class="w-full flex hover:bg-gray-500 p-3 border-t border-gray-300 focus:outline-none"
          v-for="(friend, index) in friends" :key="index"
        >
					<img 
            :src="friend.src" 
            alt="profile"
            class="w-12 h-12 rounded-full border border-gray-600"
          />
          <div class="hidden lg:block ml-4">
            <p class="text-sm font-bold leading-tight text-gray-800">{{ friend.name }}</p>
            <p class="text-sm leading-tight text-gray-800">{{ friend.handle }}</p>
          </div>
          <button class="ml-auto focus:outline-none text-sm text-blue-500 py-1 px-4 rounded-full border-2 border-blue-500">
            Follow
          </button>
				</button>
        <button class="p-3 w-full hover:bg-gray-500 text-left text-blue-500 border-t border-gray-500 focus:outline-none">
          Show More
        </button>
      </template>
    </trending-section>

  </div>
</template>

<script>
  export default {
    name: 'app',

    components: {
      SideBar: () => import('@/components/SideBar'),
      MainBar: () => import('@/components/MainBar'),
      TrendingSection: () => import('@/components/TrendingSection')
    },

    data () {
      return {
        tweet: { 
          content: ''
        },
        tweets: [
          { content: 'It is so nice outside!' }
        ],
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
        id: 'home',
        trending: [
          {top: 'Trending in TX', title: 'Gigi', bottom: 'Trending with: Rip Gigi'},
          {top: 'Music', title: 'We Won', bottom: '135K Tweets'},
          {top: 'Pop', title: 'Blue Ivy', bottom: '40k tweets'},
          {top: 'Trending in US', title: 'Denim Day', bottom: '40k tweets'},
          {top: 'Trending', title: 'When Beyonce', bottom: '25.4k tweets'},
        ],
        friends: [
          {src: 'https://avatars1.githubusercontent.com/u/65806779?s=460&u=03752090c3e22f46c1b7759b59daf1d871aada85&v=4', name: 'Gilchrist Calunia', handle: '@gilchrist32'},
          {src: 'https://avatars2.githubusercontent.com/u/26340308?s=460&u=f9dcea548505a99a2c873efb8b933aac0fe07abd&v=4', name: 'Jerome Villaruel', handle: '@veoscript'},
          {src: 'https://avatars2.githubusercontent.com/u/29187606?s=460&u=4503388a883486415e5d8a8a9eda1365cc7beeae&v=4', name: 'Resamae Cabulang', handle: '@mikie27'}
        ],
        following: [
          {src: 'https://avatars1.githubusercontent.com/u/65806779?s=460&u=03752090c3e22f46c1b7759b59daf1d871aada85&v=4', name: 'Gilchrist Calunia', handle: '@gilchrist32', time: '20 min', tweet: 'Should I just quarantine on mars??', comments: '1,000', retweets: '550', like: '1,000,003'},
          {src: 'https://avatars2.githubusercontent.com/u/26340308?s=460&u=f9dcea548505a99a2c873efb8b933aac0fe07abd&v=4', name: 'Jerome Villaruel', handle: '@veoscript', time: '55 min', tweet: 'Should me and the rock do another sub-par movie together????', comments: '2,030', retweets: '50', like: '20,003'},
          {src: 'https://avatars2.githubusercontent.com/u/29187606?s=460&u=4503388a883486415e5d8a8a9eda1365cc7beeae&v=4', name: 'Resamae Cabulang', handle: '@mikie27', time: '1.4 hr', tweet: 'Haha just made a flame thrower. Shld I sell them?', comments: '100,000', retweets: '1,000,002', like: '5,000,003'},
          {src: 'https://avatars0.githubusercontent.com/u/38458781?s=460&u=f62c697c75225996d2b9ed5c8bd755cbaa19f2db&v=4', name: 'Joshua Galit', handle: '@angryboy', time: '1.4 hr', tweet: 'Just did something crazyyyyyyy', comments: '100,500', retweets: '1,000,032', like: '5,000,103'}
        ]
      }
    },

    methods: {
      onTweetStatus () {
        let newTweet = {
          content: this.tweet.content
        }
        this.tweets.push (newTweet)
        this.tweet.content = null
      }
    }
  }
</script>

<style lang="scss" src="@/assets/css/app.scss"></style>
