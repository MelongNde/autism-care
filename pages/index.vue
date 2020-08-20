<template>
  <div>
    <v-parallax
      dark
      src="/aut.png"
      width="100%"
    >
      <v-row
        align="center"
        justify="center"
      >
        <v-col class="text-center" cols="6">
          <h1 class="display-1 font-weight-thin mb-4">
            AutismCare a numerical tool for helping people (Kids) with autism for achieving normal discussion
          </h1>
          <!-- <h4 class="subheading">Build your application today!</h4> -->
          <div class="font-weight-thin mb-4">
            Get start now! 👇🏾
          </div>
          <v-btn color="error" dark large>
            Start by learning
          </v-btn>
        </v-col>
        <v-col align="center"
               justify="center" class="text-center" cols="6"
        >
          <img src="/bg-autism.png" width="450">
        </v-col>
      </v-row>
    </v-parallax>

    <v-container class="my-5" grid-list-xs>
      <v-layout row>
        <v-flex xs12 md3 class="justify-center">
          <v-card
            ml-10
            light
            :loading="loading"
            class="pa-2 justify-center"
            max-width="374"
          >
            <v-img
              height="250"
              src="/backgrounds/chatbot.png"
            />

            <v-card-title>Chatbot</v-card-title>

            <v-card-text>
              <v-row
                align="center"
                class="mx-0"
              >
                <v-btn width="100%" outlined color="primary" dark>
                  Get start now
                </v-btn>
              </v-row>
            </v-card-text>
          </v-card>
        </v-flex>
        <v-flex xs12 md3 class="justify-center">
          <v-card
            ml-10
            light
            :loading="loading"
            class="pa-2 justify-center"
            max-width="374"
          >
            <v-img
              height="250"
              src="/backgrounds/facial_recognition.png"
            />

            <v-card-title>Capture emotions</v-card-title>

            <v-card-text>
              <v-row
                align="center"
                class="mx-0"
              >
                <v-btn width="100%" outlined color="primary" dark>
                  Get start now
                </v-btn>
              </v-row>
            </v-card-text>
          </v-card>
        </v-flex>
        <v-flex xs12 md3 class="justify-center">
          <v-card
            ml-10
            light
            :loading="loading"
            class="pa-2 justify-center"
            max-width="374"
          >
            <v-img
              height="250"
              src="/backgrounds/learn.png"
            />

            <v-card-title>Emotion learning</v-card-title>

            <v-card-text>
              <v-row
                align="center"
                class="mx-0"
              >
                <v-btn width="100%" outlined color="primary" dark>
                  Get start now
                </v-btn>
              </v-row>
            </v-card-text>
          </v-card>
        </v-flex>
        <v-flex xs12 md3 class="justify-center">
          <v-card
            ml-10
            light
            :loading="loading"
            class="pa-2 justify-center"
            max-width="374"
          >
            <v-img
              height="250"
              src="/backgrounds/find.png"
            />

            <v-card-title>Find the pairs</v-card-title>

            <v-card-text>
              <v-row
                align="center"
                class="mx-0"
              >
                <v-btn width="100%" outlined color="primary" dark>
                  Get start now
                </v-btn>
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
    return {
      loading: false,
    }
  }
}
</script>
