<template>
  <v-app id="keep">
    <v-navigation-drawer app v-model="drawer" fixed clipped class="grey lighten-4">
      <v-list dense class="grey lighten-4 nav-drawer">
        <template v-for="(item, i) in items">
          <v-layout v-if="item.heading" :key="i" row align-center>
           <!--  <v-flex xs6>
              <v-subheader v-if="item.heading">
                {{ item.heading }}
              </v-subheader>
            </v-flex>
            <v-flex xs6 class="text-xs-right">
              <v-btn small flat>edit</v-btn>
            </v-flex>-->
          </v-layout>
          <v-divider v-else-if="item.divider" :key="i" dark class="my-3"></v-divider>
          <v-list-tile v-else :key="i" @click="greet">
            <v-list-tile-action>
              <v-icon>{{ item.icon }}</v-icon>
            </v-list-tile-action>
            <v-list-tile-content>
              <v-list-tile-title class="grey--text">
                {{ item.text }}
              </v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>
        </template>
      </v-list>
    </v-navigation-drawer>
    <v-card flat>
        <v-layout row child-flex wrap app>
          <div>
            <v-toolbar class="amber brand">
              <v-toolbar-title>
                <router-link to="/" tag="span" style="cursor: pointer">
                  <div class="logo">
                    <img src="./assets/logo.png" alt="">
                  </div>
                </router-link>
              </v-toolbar-title>
              <v-spacer></v-spacer>
              <v-toolbar-side-icon @click="drawer = !drawer" dark></v-toolbar-side-icon>
            </v-toolbar>
          </div>
          <div style="flex-basis: 73%">
            <v-toolbar class="white">
              <v-text-field
                placeholder="Поиск"
                prepend-icon="search"
                solo-inverted
                hide-details>
              </v-text-field>
              <v-spacer></v-spacer>

              <div class="langselect">
                <v-select
                  :items="dropdown_lang"
                  box
                  placeholder="УКР"
                  hide-details
                ></v-select>
              </div>
              <div>
                <v-btn flat>
                  Выйти
                  <v-icon class="ml-1">exit_to_app</v-icon>
                </v-btn>
              </div>

            </v-toolbar>
          </div>
        </v-layout>
    </v-card>
    <v-content>
      <v-container fluid fill-height class="grey lighten-4">
        <v-layout justify-center align-center row>
          <!-- <v-flex shrink>
            <v-tooltip right>
              <template v-slot:activator="{ on }">
                <v-btn :href="source" icon large target="_blank" v-on="on">
                  <v-icon large>code</v-icon>
                </v-btn>
              </template>
              <span>Source</span>
            </v-tooltip>
            <v-tooltip right>
              <template v-slot:activator="{ on }">
                <v-btn icon large href="https://codepen.io/johnjleider/pen/jZQNbd" target="_blank" v-on="on">
                  <v-icon large>mdi-codepen</v-icon>
                </v-btn>
              </template>
              <span>Codepen</span>
            </v-tooltip>
          </v-flex> -->
          <v-flex xs12 sm6 offset-sm3>
            <v-card>
              <v-list two-line>
                <template v-for="(item, index) in list_items">
                  <v-list-tile
                    :key="item.title"
                    avatar
                    ripple
                    @click="toggle(index)"
                  >
                    <v-list-tile-content>
                      <v-list-tile-title>{{ item.title }}</v-list-tile-title>
                      <v-list-tile-sub-title class="text--primary">{{ item.headline }}</v-list-tile-sub-title>
                      <v-list-tile-sub-title>{{ item.subtitle }}</v-list-tile-sub-title>
                    </v-list-tile-content>

                    <v-list-tile-action>
                      <v-list-tile-action-text>{{ item.action }}</v-list-tile-action-text>
                      <v-icon
                        v-if="selected.indexOf(index) < 0"
                        color="grey lighten-1"
                      >
                        star_border
                      </v-icon>

                      <v-icon
                        v-else
                        color="yellow darken-2"
                      >
                        star
                      </v-icon>
                    </v-list-tile-action>

                  </v-list-tile>
                  <v-divider
                    v-if="index + 1 < list_items.length"
                    :key="index"
                  ></v-divider>
                </template>
              </v-list>
            </v-card>
          </v-flex>
        </v-layout>
      </v-container>
      <v-container>
        <!-- paginations -->
        <v-layout justify-end row>
          <div>
            <v-pagination
              v-model="page"
              :length="5"
              circle
            ></v-pagination>
          </div>
        </v-layout>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
  export default {
    data: () => ({
      page: '01',
      dropdown_lang: [
        {text: 'УКР'},
        {text: 'РУС'}
      ],
      drawer: null,
      items: [
        { icon: 'lightbulb_outline', text: 'Главная' },
        { icon: 'touch_app', text: 'Админ(ЦВШ)' },
        { divider: true },
        { icon: 'settings', text: 'Кандидаты' },
        { icon: 'chat_bubble', text: 'Статистика' },
        { icon: 'help', text: 'Соц.опрос' },
        { icon: 'phonelink', text: 'Вопросы' },
        { icon: 'keyboard', text: 'Активисты' }
      ],
      selected: [2],
      list_items: [
        {
          action: '15 min',
          headline: 'Brunch this weekend?',
          title: 'Ali Connors',
          subtitle: "I'll be in your neighborhood doing errands this weekend. Do you want to hang out?"
        },
        {
          action: '2 hr',
          headline: 'Summer BBQ',
          title: 'me, Scrott, Jennifer',
          subtitle: "Wish I could come, but I'm out of town this weekend."
        },
        {
          action: '6 hr',
          headline: 'Oui oui',
          title: 'Sandra Adams',
          subtitle: 'Do you have Paris recommendations? Have you ever been?'
        },
        {
          action: '12 hr',
          headline: 'Birthday gift',
          title: 'Trevor Hansen',
          subtitle: 'Have any ideas about what we should get Heidi for her birthday?'
        },
        {
          action: '18hr',
          headline: 'Recipe to try',
          title: 'Britta Holt',
          subtitle: 'We should eat this: Grate, Squash, Corn, and tomatillo Tacos.'
        }
      ]
    }),
    methods: {
      greet: function (event) {
        // `this` внутри методов указывает на экземпляр Vue
        alert('Привет, ' + this.name + '!')
        // `event` — нативное событие DOM
        if (event) {
          alert(event.target.tagName)
        }
      }
    },
    props: {
      source: String,
      page: String
    }
  }
</script>

<style lang="stylus">
  @import './stylus/main'
  #keep main .container {
    height: 660px;
  }

  .navigation-drawer__border {
    display: none;
  }

  .text {
    font-weight: 400;
  }
</style>
