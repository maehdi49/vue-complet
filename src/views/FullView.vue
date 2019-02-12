<template>
    <div class="full">
        <img alt="Vue logo" src="../assets/logo.png">
        <b-container>
            <b-row>
                <b-col >
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
  import 'bootstrap/dist/css/bootstrap.css'
  import 'bootstrap-vue/dist/bootstrap-vue.css'
  Vue.use(BootstrapVue)

  var titre, lien, contenu, date, temps

  export default {
    name: 'fullView',
      components: {
      Post
    },
    data() {
      return {
        post: [],
        errors: []
      }
    },
    created () {
      var recupPost
      var pageURL = window.location.href
      var ID = pageURL.substr(pageURL.lastIndexOf('/') + 1)
      var urlAPI = `https://www.go-interim.fr/wp-json/wp/v2/posts/` + ID
      if (this.$route.query.site === '1') {
        urlAPI = `http://www.madeinblue.com/wp-json/wp/v2/posts/` + ID
      } else if (this.$route.query.site === '3'){
        urlAPI = `https://www.laura-massis.com/wp-json/wp/v2/posts/` + ID
      }
      console.log(urlAPI)
      var now = moment()

      axios.get(urlAPI)
        .then(response => {
          // JSON responses are automatically parsed.
            titre = response.data['title'].rendered
            contenu = response.data['content'].rendered
            lien = response.data['link']

            date = response.data['date']
            var date_obj = moment(date)

            temps = now.diff(date_obj, 'days') + 1

            moment.locale('fr')
            recupPost = {
              lien: lien,
              contenu: contenu,
              titre: titre,
              date: moment(date).format('LLLL'),
              temps: temps
            }
            this.post = recupPost
        })
        .catch(e => {
          console.log(e)
        })
    }
  }
</script>
