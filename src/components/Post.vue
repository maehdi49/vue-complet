<template>
    <div>
        <router-link :to="{ path: postData.lien , query: { site: postData.site } }">
            <h3 v-html="postData.titre"></h3>
        </router-link>

        <i>il y a {{postData.temps}} jours </i> | <i>  Publié le : {{postData.date}}</i>

        <p class="text-left mt-3">
            <span v-html="postData.contenu"></span>
        </p>
    </div>
</template>

<script>
export default {
  name: 'Post',
  props: ['postData']
}

</script>
