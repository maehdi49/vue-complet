<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <b-container v-if="posts && posts.length">
      <b-row>
        <b-col col lg="3" v-for="post in posts">
          <Post :postData="post" />
        </b-col>
      </b-row>
    </b-container >
  </div>
</template>

<script>
import Post from '@/components/Post.vue'
import axios from 'axios'
import moment from 'moment'

import Vue from 'vue'
import BootstrapVue from 'bootstrap-vue'
Vue.use(BootstrapVue)
import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'


var titre, lien, contenu, date, temps

export default {
  name: 'home',
  components: {
    Post
  },
  data() {
    return {
      posts: [],
      errors: []
    }
  },
  created () {
    var recupPost
    var now = moment()

    axios.get(`http://www.madeinblue.com/wp-json/wp/v2/posts`)
      .then(response => {
        // JSON responses are automatically parsed.
        for (var i = 0; i < response.data.length; i++) {
          titre = response.data[i]['title'].rendered
          contenu = response.data[i]['content'].rendered.slice(0, 150)+"..."
          lien = 'post/' + response.data[i]['id']

          date = response.data[i]['date']
          var date_obj = moment(date)

          temps = now.diff(date_obj, 'days') + 1

          moment.locale('fr')
          recupPost = {
            lien: lien,
            contenu: contenu,
            titre: titre,
            date: moment(date).format('LLLL'),
            temps: temps,
            site: "1"
          }

          this.posts.push(recupPost)
        }

      })
      .catch(e => {
        console.log(e)
      })

    axios.get(`https://www.laura-massis.com/wp-json/wp/v2/posts`)
      .then(response => {
        // JSON responses are automatically parsed.
        for (var i = 0; i < response.data.length; i++) {
          titre = response.data[i]['title'].rendered
          contenu = response.data[i]['content'].rendered.slice(0, 150)+"..."
          lien = 'post/' + response.data[i]['id']

          date = response.data[i]['date']
          var date_obj = moment(date)

          temps = now.diff(date_obj, 'days') + 1

          moment.locale('fr')
          recupPost = {
            lien: lien,
            contenu: contenu,
            titre: titre,
            date: moment(date).format('LLLL'),
            temps: temps,
            site: "3"
          }

          this.posts.push(recupPost)
        }

      })
      .catch(e => {
        console.log(e)
      })

    axios.get(`https://www.go-interim.fr/wp-json/wp/v2/posts`)
      .then(response => {
        // JSON responses are automatically parsed.
        for (var i = 0; i < response.data.length; i++) {
          titre = response.data[i]['title'].rendered
          contenu = response.data[i]['content'].rendered.slice(0, 150)+"..."
          lien = 'post/' + response.data[i]['id']

          date = response.data[i]['date']
          var date_obj = moment(date)

          temps = now.diff(date_obj, 'days') + 1

          moment.locale('fr')
          recupPost = {
            lien: lien,
            contenu: contenu,
            titre: titre,
            date: moment(date).format('LLLL'),
            temps: temps,
            site: "2"
          }

          this.posts.push(recupPost)
        }

      })
      .catch(e => {
        console.log(e)
      })
  }
}
</script>
