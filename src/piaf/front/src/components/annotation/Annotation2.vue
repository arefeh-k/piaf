<template>
  <v-app>
  <!--  Is always placed at the top of an application with a lower priority than v-system-bar -->
  <v-app-bar app hide-on-scroll>
    <Navbar :text="`Trouver une réponse`"/>
  </v-app-bar>

  <!-- Sizes your content based upon application components -->
  <v-content>
    <!-- Provides the application the proper gutter -->
    <v-container fluid>
      <AnnotationTask v-if="currentDocument" style="margin-bottom:150px;"/>
    </v-container>
    <!-- we need to put the Animation after the other components for the background to be beneath -->
    <Animation/>
  </v-content>

  <v-footer
  style="z-index:10"
  padless
  fixed
  min-height='150px'
  color='white'>
    <FooterAnswers :routeAfterValidation="`/annotation/`+$route.params.level+`/bravo`" :routeAfterReport="`/annotation/`+$route.params.level+`/report`"/>
  </v-footer>
</v-app>
</template>

<script>

import FooterAnswers from '../../components/FooterAnswers';
import AnnotationTask from './AnnotationTask';
import Navbar from '../../components/Navbar';
import Animation from '../../components/Animation.vue';

import { mapState } from 'vuex'

export default {
  name: 'App',
  components: {
    AnnotationTask,
    Navbar,
    FooterAnswers,
    Animation,
  },
  computed: mapState([
    'currentDocument',
  ]),
  created () {
      this.$store.dispatch('getUserDetails')
      this.$store.dispatch('resetDefaultStore')
      this.$store.dispatch('loadNewQuestion')
  },
};
</script>
