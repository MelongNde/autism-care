<template>
  <div>
    <v-container grid-list-xs>
      <h1 class="text-xl-h4">Learn emotions</h1>
    </v-container>

    <v-divider :inset="inset"></v-divider>

    <v-container grid-list-xs>
      <h4 class="text-xl-h4">Mans</h4>
    </v-container>

    <v-container class="my-5" grid-list-xs>
      <v-layout row>
        <v-flex xs12 md3 v-for="(boyEmotion , index) in boyEmotions" :key="index" class="justify-center">
          <v-card
            ml-10
            light
            :loading="loading"
            class="pa-2 justify-center"
            max-width="374"
          >
            <v-img
              height="250"
              :src= boyEmotion.image
            ></v-img>

            <v-card-title>{{boyEmotion.title}}</v-card-title>

            <v-card-text>
              <v-row
                align="center"
                class="mx-0"
              >
                {{boyEmotion.description}}
              </v-row>
            </v-card-text>
          </v-card>
        </v-flex>
      </v-layout>
    </v-container>

     <v-container grid-list-xs>
      <h4 class="text-xl-h4">Girls</h4>
    </v-container>

    <v-container class="my-5" grid-list-xs>
      <v-layout row>
        <v-flex xs12 md3 v-for="(girlEmotion , index) in girlEmotions" :key="index" class="justify-center">
          <v-card
            ml-10
            light
            :loading="loading"
            class="pa-2 justify-center"
            max-width="374"
          >
            <v-img
              height="250"
              :src= girlEmotion.image
            ></v-img>

            <v-card-title>{{girlEmotion.title}}</v-card-title>

            <v-card-text>
              <v-row
                align="center"
                class="mx-0"
              >
                {{girlEmotion.description}}
              </v-row>
            </v-card-text>
          </v-card>
        </v-flex>
      </v-layout>
    </v-container>
  </div>
</template>

<script>
/* eslint-disable */
export default {
  data() {
    return{
      inset: false,
      boyEmotions: [
        {
          image: '/emotions/man-happy.jpg',
          title: 'Happiness',
          description: 'Mouth smiling; possible laughter; crows-feet wrinkles at sides of sparking eyes; slightly raise eyebrows'
        },
        {
          image: '/emotions/man-sad.jpg',
          title: 'Sadness',
          description: 'Crying is often an indication od sadness. Dropping of boy, trembling lip, tears. Eyes cast down'
        },
        {
          image: '/emotions/man-angry.jpg',
          title: 'Anger',
          description: 'The inner muscles are relaxed. Eyes are tangent to the iris. the mouth is closed and lips are contact.'
        },
        {
          image: '/emotions/man-fear.jpg',
          title: 'Fear',
          description: 'The eyebrows are raised and pulled together. The inner eyebrows are bent upward.'
        }
      ],
     girlEmotions: [
        {
          image: '/emotions/girl-happy.jpg',
          title: 'Happiness',
          description: 'Mouth smiling; possible laughter; crows-feet wrinkles at sides of sparking eyes; slightly raise eyebrows'
        },
        {
          image: '/emotions/girl-sad.jpg',
          title: 'Sadness',
          description: 'Crying is often an indication od sadness. Dropping of boy, trembling lip, tears. Eyes cast down'
        },
        {
          image: '/emotions/girl-angry.jpg',
          title: 'Anger',
          description: 'The inner muscles are relaxed. Eyes are tangent to the iris. the mouth is closed and lips are contact.'
        },
        {
          image: '/emotions/girl-fear.jpg',
          title: 'Fear',
          description: 'The eyebrows are raised and pulled together. The inner eyebrows are bent upward.'
        }
      ]
    }
  }
}
</script>
