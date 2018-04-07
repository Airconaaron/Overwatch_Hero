<template>
   <v-container grid-list-md text-xs-center>
     <v-layout row wrap>
       <v-flex xs6>
         <h2>Your Team</h2>
         <ul>
           <li v-for="person in friend.people" v-if="person.selected == true" :key="person.id" >
             <Roster :name="person.name" :image="person.bg" :role="person.role" :score="person.score" :friend='1' @click.native="heroDeselect(1, person.id)"></Roster>
           </li>
           <li v-for="n in (6 - friend.number)" :key="n + 50" >
             <Roster :friend='1'></Roster>
           </li>
         </ul>
       </v-flex>
       <v-flex xs6>
         <h2>Enemy Team</h2>
         <ul>
           <li v-for="person in enemy.people" v-if="person.selected == true" :key="person.id" >
             <Roster :name="person.name" :image="person.bg" :role="person.role" :score="person.score" :friend='0' @click.native="heroDeselect(0, person.id)"></Roster>
           </li>
           <li v-for="n in (6 - enemy.number)" :key="n + 50" >
             <Roster :friend='0'></Roster>
           </li>
         </ul>
       </v-flex>

       <v-flex xs6>
        <ul>
          <!--  .sort(this.compareScore) -->
          <li v-for="person in friend.people" v-if="person.selected === false" :key="person.id" >
            <HeroPicker :name="person.name" :image="person.bg" :role="person.role" :score="person.score" :left='false' @click.native="heroSelect(1, person.id)"></HeroPicker>
          </li>
        </ul>
        <!-- <v-card dark color="secondary">
          <v-card-text class="px-0">6</v-card-text>
        </v-card> -->
      </v-flex>
      <v-flex xs6>
        <ul>
          <li v-for="person in enemy.people" v-if="person.selected === false" :key="person.id">
            <HeroPicker :name="person.name" :image="person.bg" :role="person.role" :score="person.score" :left='true' @click.native="heroSelect(0, person.id)"></HeroPicker>
          </li>
        </ul>
        <!-- <v-card dark color="secondary">
          <v-card-text class="px-0">6</v-card-text>
        </v-card> -->
      </v-flex>
      <v-flex xs12>
        <h2>Map</h2>
        <ul>
          <li v-for="person in map.list" :key="person.id">
            <Map :name="person.name" :image="person.bg" @click.native="mapSelect"></Map>
          </li>
        </ul>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import HeroPicker from '@/components/HeroPicker'
import Roster from '@/components/Roster'
import Map from '@/components/Map'
export default {
  name: 'HomePage',
  components: {
    HeroPicker,
    Roster,
    Map
  },
  methods: {
    mapSelect: function (event) {
      // console.log(this.friend.people)
      // alert('hello')
      this.randomizeScore()
    },
    heroSelect: function (t, id) {
      if (t === 1) {
        if (this.friend.number < 6) {
          for (var person of this.friend.people) {
            if (person.id === id) {
              person.selected = true
              this.friend.number += 1
              this.randomizeScore()
            }
          }
        }
      } else {
        if (this.enemy.number < 6) {
          for (var person1 of this.enemy.people) {
            if (person1.id === id) {
              person1.selected = true
              this.enemy.number += 1
              this.randomizeScore()
            }
          }
        }
      }
    },
    heroDeselect: function (t, id) {
      if (t === 1) {
        for (var person of this.friend.people) {
          if (person.id === id) {
            person.selected = false
            this.friend.number -= 1
            this.randomizeScore()
          }
        }
      } else {
        for (var person1 of this.enemy.people) {
          if (person1.id === id) {
            person1.selected = false
            this.enemy.number -= 1
            this.randomizeScore()
          }
        }
      }
    },
    randomizeScore: function () {
      for (var person of this.friend.people) {
        person.score = Math.ceil(Math.random() * 100)
      }
      for (var person1 of this.enemy.people) {
        person1.score = Math.ceil(Math.random() * 100)
      }
      // this.friend.people.sort(this.compareScore)
    },
    compareScore: function (a, b) {
      if (a.score < b.score) { return 1 }
      if (a.score > b.score) { return -1 }
      return 0
    }
  },
  data () {
    return {
      friend: {
        people: [
          {id: 0, name: 'Doomfist', bg: 'portraits/doomfist-portrait-small.png', role: 'dps', score: 50, selected: true},
          {id: 1, name: 'Genji', bg: 'portraits/genji-portrait-small.png', role: 'dps', score: 50, selected: false},
          {id: 2, name: 'McCree', bg: 'portraits/mccree-portrait-small.png', role: 'dps', score: 50, selected: false},
          {id: 3, name: 'Pharah', bg: 'portraits/pharah-portrait-small.png', role: 'dps', score: 50, selected: false},
          {id: 4, name: 'Reaper', bg: 'portraits/reaper-portrait-small.png', role: 'dps', score: 50, selected: false},
          {id: 5, name: 'Soldier:76', bg: 'portraits/soldier76-portrait-small.png', role: 'dps', score: 50, selected: false},
          {id: 6, name: 'Sombra', bg: 'portraits/sombra-portrait-small.png', role: 'dps', score: 50, selected: false},
          {id: 7, name: 'Tracer', bg: 'portraits/tracer-portrait-small.png', role: 'dps', score: 50, selected: false},
          {id: 8, name: 'Bastion', bg: 'portraits/bastion-portrait-small.png', role: 'def', score: 50, selected: false},
          {id: 9, name: 'Hanzo', bg: 'portraits/hanzo-portrait-small.png', role: 'def', score: 50, selected: false},
          {id: 10, name: 'Junkrat', bg: 'portraits/junkrat-portrait-small.png', role: 'def', score: 50, selected: false},
          {id: 11, name: 'Mei', bg: 'portraits/mei-portrait-small.png', role: 'def', score: 50, selected: false},
          {id: 12, name: 'Torbjörn', bg: 'portraits/torbjorn-portrait-small.png', role: 'def', score: 50, selected: false},
          {id: 13, name: 'Widowmaker', bg: 'portraits/widowmaker-portrait-small.png', role: 'def', score: 50, selected: false},
          {id: 14, name: 'D.VA', bg: 'portraits/dva-portrait-small.png', role: 'tank', score: 50, selected: false},
          {id: 15, name: 'Orisa', bg: 'portraits/orisa-portrait-small.png', role: 'tank', score: 50, selected: false},
          {id: 16, name: 'Reinhardt', bg: 'portraits/reinhardt-portrait-small.png', role: 'tank', score: 50, selected: false},
          {id: 17, name: 'Roadhog', bg: 'portraits/roadhog-portrait-small.png', role: 'tank', score: 50, selected: false},
          {id: 18, name: 'Winston', bg: 'portraits/winston-portrait-small.png', role: 'tank', score: 50, selected: false},
          {id: 19, name: 'Zarya', bg: 'portraits/zarya-portrait-small.png', role: 'tank', score: 50, selected: false},
          {id: 20, name: 'Ana', bg: 'portraits/ana-portrait-small.png', role: 'heal', score: 50, selected: false},
          {id: 21, name: 'Brigitte', bg: 'portraits/brigitte-portrait-small.png', role: 'heal', score: 50, selected: false},
          {id: 22, name: 'Lúcio', bg: 'portraits/lucio-portrait-small.png', role: 'heal', score: 50, selected: false},
          {id: 23, name: 'Mercy', bg: 'portraits/mercy-portrait-small.png', role: 'heal', score: 50, selected: false},
          {id: 24, name: 'Moira', bg: 'portraits/moira-portrait-small.png', role: 'heal', score: 50, selected: false},
          {id: 25, name: 'Symmetra', bg: 'portraits/symmetra-portrait-small.png', role: 'heal', score: 50, selected: false},
          {id: 26, name: 'Zenyatta', bg: 'portraits/zenyatta-portrait-small.png', role: 'heal', score: 50, selected: false}
        ],
        number: 1
      },
      enemy: {
        people: [
          {id: 0, name: 'Doomfist', bg: 'portraits/doomfist-portrait-small.png', role: 'dps', score: 50, selected: false},
          {id: 1, name: 'Genji', bg: 'portraits/genji-portrait-small.png', role: 'dps', score: 50, selected: false},
          {id: 2, name: 'McCree', bg: 'portraits/mccree-portrait-small.png', role: 'dps', score: 50, selected: false},
          {id: 3, name: 'Pharah', bg: 'portraits/pharah-portrait-small.png', role: 'dps', score: 50, selected: false},
          {id: 4, name: 'Reaper', bg: 'portraits/reaper-portrait-small.png', role: 'dps', score: 50, selected: false},
          {id: 5, name: 'Soldier:76', bg: 'portraits/soldier76-portrait-small.png', role: 'dps', score: 50, selected: false},
          {id: 6, name: 'Sombra', bg: 'portraits/sombra-portrait-small.png', role: 'dps', score: 50, selected: false},
          {id: 7, name: 'Tracer', bg: 'portraits/tracer-portrait-small.png', role: 'dps', score: 50, selected: false},
          {id: 8, name: 'Bastion', bg: 'portraits/bastion-portrait-small.png', role: 'def', score: 50, selected: false},
          {id: 9, name: 'Hanzo', bg: 'portraits/hanzo-portrait-small.png', role: 'def', score: 50, selected: false},
          {id: 10, name: 'Junkrat', bg: 'portraits/junkrat-portrait-small.png', role: 'def', score: 50, selected: false},
          {id: 11, name: 'Mei', bg: 'portraits/mei-portrait-small.png', role: 'def', score: 50, selected: false},
          {id: 12, name: 'Torbjörn', bg: 'portraits/torbjorn-portrait-small.png', role: 'def', score: 50, selected: false},
          {id: 13, name: 'Widowmaker', bg: 'portraits/widowmaker-portrait-small.png', role: 'def', score: 50, selected: false},
          {id: 14, name: 'D.VA', bg: 'portraits/dva-portrait-small.png', role: 'tank', score: 50, selected: false},
          {id: 15, name: 'Orisa', bg: 'portraits/orisa-portrait-small.png', role: 'tank', score: 50, selected: false},
          {id: 16, name: 'Reinhardt', bg: 'portraits/reinhardt-portrait-small.png', role: 'tank', score: 50, selected: true},
          {id: 17, name: 'Roadhog', bg: 'portraits/roadhog-portrait-small.png', role: 'tank', score: 50, selected: false},
          {id: 18, name: 'Winston', bg: 'portraits/winston-portrait-small.png', role: 'tank', score: 50, selected: false},
          {id: 19, name: 'Zarya', bg: 'portraits/zarya-portrait-small.png', role: 'tank', score: 50, selected: false},
          {id: 20, name: 'Ana', bg: 'portraits/ana-portrait-small.png', role: 'heal', score: 50, selected: false},
          {id: 21, name: 'Brigitte', bg: 'portraits/brigitte-portrait-small.png', role: 'heal', score: 50, selected: false},
          {id: 22, name: 'Lúcio', bg: 'portraits/lucio-portrait-small.png', role: 'heal', score: 50, selected: false},
          {id: 23, name: 'Mercy', bg: 'portraits/mercy-portrait-small.png', role: 'heal', score: 50, selected: false},
          {id: 24, name: 'Moira', bg: 'portraits/moira-portrait-small.png', role: 'heal', score: 50, selected: false},
          {id: 25, name: 'Symmetra', bg: 'portraits/symmetra-portrait-small.png', role: 'heal', score: 50, selected: false},
          {id: 26, name: 'Zenyatta', bg: 'portraits/zenyatta-portrait-small.png', role: 'heal', score: 50, selected: false}
        ],
        number: 1
      },
      map: {
        list: [
          {id: 0, name: 'None', bg: 'Blank.png'},
          {id: 1, name: 'Hanamura', bg: 'maps/hanamura.jpg'},
          {id: 2, name: 'Horizon Lunar Colony', bg: 'maps/lunar.jpg'},
          {id: 3, name: 'Temple of Anubis', bg: 'maps/anubis.jpg'},
          {id: 4, name: 'Volskaya Industries', bg: 'maps/volskaya.jpg'},
          {id: 5, name: 'Dorado', bg: 'maps/dorado.jpg'},
          {id: 6, name: 'Junkertown', bg: 'maps/junkertown.jpg'},
          {id: 7, name: 'Route 66', bg: 'maps/route-66.jpg'},
          {id: 8, name: 'Watchpoint: Gilbratar', bg: 'maps/gibraltar.jpg'},
          {id: 9, name: 'Ilios', bg: 'maps/ilios.jpg'},
          {id: 10, name: 'Lijiang Tower', bg: 'maps/lijiang_tower.jpg'},
          {id: 11, name: 'Nepal', bg: 'maps/nepal.jpg'},
          {id: 12, name: 'Oasis', bg: 'maps/oasis.jpg'},
          {id: 13, name: 'Blizzard World', bg: 'maps/blizzardworld.jpg'},
          {id: 14, name: 'Eichenwalde', bg: 'maps/eichenwalde.jpg'},
          {id: 15, name: 'Hollywood', bg: 'maps/hollywood.jpg'},
          {id: 16, name: 'King\'s Row', bg: 'maps/kings-row.jpg'},
          {id: 17, name: 'Numbani', bg: 'maps/numbani.jpg'}
        ],
        current: 0
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 10px 2px;
}
a {
  color: #42b983;
}

</style>
