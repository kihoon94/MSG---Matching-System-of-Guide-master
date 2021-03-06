<template>
  <v-ons-page :style="swipePosition">
    <custom-toolbar :style="swipeTheme" modifier="white-content">
      {{ title }}
      <v-ons-toolbar-button slot="right" modifier="white-content"
                            @click="$store.commit('splitter/toggle')"
      >
        <v-ons-icon icon="ion-navicon, material:md-menu"></v-ons-icon>
      </v-ons-toolbar-button>
    </custom-toolbar>

    <v-ons-tabbar position="auto"
      swipeable
      :modifier="md ? 'autogrow white-content' : ''"
      :on-swipe="md ? onSwipe : null"
      :tabbar-style="swipeTheme"
      :tabs="tabs"
      :index.sync="index"
      @postchange="showTip($event, 'Tip: Try swiping pages!')"
    ></v-ons-tabbar>
  </v-ons-page>
</template>

<script>
import test_1 from './pages/Camera.vue';
import test_2 from './pages/Home.vue';
import test_3 from './pages/Forms.vue';
import test_4 from './pages/Animations.vue';

// Just a linear interpolation formula
const lerp = (x0, x1, t) => parseInt((1 - t) * x0 + t * x1, 10);
// RGB colors
const red = [244, 67, 54];
const blue = [30, 136, 229];
const purple = [103, 58, 183];

export default {
  data () {
    return {
      shutUp: !this.md,
      showingTip: false,
      colors: red,
      animationOptions: {},
      topPosition: 0,
      tabs: [
        // {
        //   label: 'Test1',
        //   icon: 'ion-camera, material:md-camera',
        //   page: test_1,
        //   theme: red,
        //   style: this.md ? { maxWidth: '60px' } : {},
        //   top: -105 // Toolbar + Tabbar heights
        // },
        {
          label: 'Test2',
          icon: this.md ? null : 'ion-home',
          page: test_2,
          theme: red
        },
        {
          label: 'Test3',
          icon: this.md ? null : 'ion-edit',
          page: test_3,
          theme: blue
        },
        {
          label: 'Test4',
          icon: this.md ? null : 'ion-film-marker',
          page: test_4,
          theme: purple
        }
      ]
    };
  },

  methods: {
    onSwipe(index, animationOptions) {
      // Apply the same transition as ons-tabbar
      this.animationOptions = animationOptions;

      // Interpolate colors and top position
      const a = Math.floor(index), b = Math.ceil(index), ratio = index % 1;
      this.colors = this.colors.map((c, i) => lerp(this.tabs[a].theme[i], this.tabs[b].theme[i], ratio));
      this.topPosition = lerp(this.tabs[a].top || 0, this.tabs[b].top || 0, ratio);
    },
    showTip(e, message) {
      if (!this.shutUp && !(e && e.swipe) && !this.showingTip) {
        this.showingTip = true;
        this.$ons.notification.toast({
          message,
          buttonLabel: 'Shut up!',
          timeout: 2000
        }).then(i => {
          this.shutUp = i === 0;
          this.showingTip = false;
        });
      }
    }
  },

  computed: {
    index: {
      get() {
        return this.$store.state.tabbar.index;
      },
      set(newValue) {
        this.$store.commit('tabbar/set', newValue)
      }
    },
    title() {
      return this.md ? 'Onsen UI' : this.tabs[this.index].label;
    },
    swipeTheme() {
      return this.md && {
        backgroundColor: `rgb(${this.colors.join(',')})`,
        transition: `all ${this.animationOptions.duration || 0}s ${this.animationOptions.timing || ''}`
      }
    },
    swipePosition() {
      return this.md && {
        top: this.topPosition + 'px',
        transition: `all ${this.animationOptions.duration || 0}s ${this.animationOptions.timing || ''}`
      }
    }
  }
};
</script>

<style>
/* Custom 'white-content' modifier */

.page--material .toolbar--white-content__center,
.page--material .toolbar-button--white-content,
.page--material :checked + .tabbar--white-content__button {
  color: white;
}

.page--material .tabbar--white-content__button {
  color: rgba(255, 255, 255, 0.7);
}

.page--material .tabbar--white-content__border {
  background-color: white;
}
</style>
