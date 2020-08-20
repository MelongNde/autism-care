<template>
  <div id="app">
    <div class="info">
      <div><span class="label">Time:</span><span class="value">{{ time }}</span></div>
      <div><span class="label">Turns:</span><span class="value">{{ turns }}</span></div>
    </div>
    <div class="cards">
      <div v-for="(card, i ) in cards" :key="i" :class="{ flipped: card.flipped, found: card.found }" class="card" @click="flipCard(card)">
        <div class="back" />
        <div :style="{ backgroundImage: 'url(' + card.image + ')' }" class="front" />
      </div>
    </div>
    <div v-if="showSplash" class="splash">
      <div class="overlay" />
      <div class="content">
        <div class="title">
          You won!
        </div>
        <div class="score">
          Score: {{ score }}
        </div>
        <button class="newGame" @click="resetGame()">
          New game
        </button>
      </div>
    </div>
  </div>
</template>

<script>
/* eslint-disable */
import _ from 'lodash'

const CardTypes = [
  { name: 'vue', image: 'https://vuejs.org/images/logo.png' },
  { name: 'express', image: 'https://coligo.io/images/express.svg' },
  { name: 'mongo', image: 'https://upload.wikimedia.org/wikipedia/en/thumb/4/45/MongoDB-Logo.svg/527px-MongoDB-Logo.svg.png' },
  { name: 'nodejs', image: 'https://worldvectorlogo.com/logos/nodejs-icon.svg' },
  { name: 'webpack', image: 'https://camo.githubusercontent.com/66747a6e05a799aec9c6e04a3e721ca567748e8b/68747470733a2f2f662e636c6f75642e6769746875622e636f6d2f6173736574732f313336353838312f313931383337332f32653035373166612d376462632d313165332d383436352d3839356632393164343366652e706e67' },
  { name: 'babel', image: 'https://babeljs.io/images/logo.svg' }
]

const shuffleCards = () => {
  const cards = [].concat(_.cloneDeep(CardTypes), _.cloneDeep(CardTypes));
  return _.shuffle(cards);
}
  export default {
    data () {
      return {
        showSplash: false,
        cards: [],
        started: false,
        startTime: 0,
        turns: 0,
        flipBackTimer: null,
        timer: null,
        time: "--:--",
        score: 0
      }
    },
    created (){
      /* eslint-disable */
      this.resetGame();
      // if (process.client) {
      //   require('vue-lodash')
      // }
    },
    methods: {
      resetGame()
      {
        this.showSplash = false;
        let cards = shuffleCards();
        this.turns = 0;
        this.score = 0;
        this.started = false;
        this.startTime = 0;

        _.each(cards, card => {
          card.flipped = false;
          card.found = false;
        });

        this.cards = cards;
      },

    flippedCards()
      {
        return _.filter(this.cards, card => card.flipped);
      },

    sameFlippedCard()
    {
      let flippedCards = this.flippedCards();
      if (flippedCards.length == 2) {
        if (flippedCards[0].name == flippedCards[1].name)
        return true;
      }
    },

    setCardFounds()
    {
      _.each(this.cards, card => {
        if (card.flipped)
        card.found = true;
      });
    },

    checkAllFound()
    {
      let foundCards = _.filter(this.cards, card => card.found);
      if (foundCards.length == this.cards.length)
      return true;
    },

    startGame()
    {
      this.started = true;
      this.startTime = moment();

      this.timer = setInterval(() => {
        this.time = moment(moment().diff(this.startTime)).format("mm:ss");
      }, 1000);
    },

    finishGame()
    {
      this.started = false;
      clearInterval(this.timer);
      let score = 1000 - (moment().diff(this.startTime, 'seconds') - CardTypes.length * 5) * 3 - (this.turns - CardTypes.length) * 5;
      this.score = Math.max(score, 0);
      this.showSplash = true;
    },

    flipCard(card)
     {
      if (card.found || card.flipped) return;

      if (!this.started) {
        this.startGame();
      }

      let flipCount = this.flippedCards().length;
      if (flipCount == 0) {
        card.flipped = !card.flipped;
      } else
      if (flipCount == 1) {
        card.flipped = !card.flipped;
        this.turns += 1;

        if (this.sameFlippedCard()) {
          // Match!
          this.flipBackTimer = setTimeout(() => {
            this.clearFlipBackTimer();
            this.setCardFounds();
            this.clearFlips();

            if (this.checkAllFound()) {
              this.finishGame();
            }

          }, 200);
        } else
        {
          // Wrong match
          this.flipBackTimer = setTimeout(() => {
            this.clearFlipBackTimer();
            this.clearFlips();
          }, 1000);
        }
      }
    },

    clearFlips()
    {
      _.map(this.cards, card => card.flipped = false);
    },


    clearFlipBackTimer()
    {
      clearTimeout(this.flipBackTimer);
      this.flipBackTimer = null;
    }
    }
  }
  </script>
  <style>
    * {
    -moz-box-sizing: border-box;
    -webkit-box-sizing: border-box;
    box-sizing: border-box;
  }

  html {
    background-color: #292C33;
    color: White;
    font-size: 16px;
    font-family: 'Open Sans', 'Helvetica', 'Arial', sans-serif;
    font-weight: 400;
    font-smoothing: antialiased;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  #app {
    margin: 2em;
  }

  .info {
    text-align: center;
    padding-bottom: 1em;
    border-bottom: 1px solid #555;
  }
  .info > div {
    display: inline-block;
    width: 200px;
  }
  .info > div .label {
    margin-right: 5px;
  }
  .info > div .value {
    font-weight: bold;
  }

  .cards .card {
    position: relative;
    display: inline-block;
    width: 100px;
    height: 150px;
    margin: 1em 2em;
    -moz-transition: opacity 0.5s;
    -o-transition: opacity 0.5s;
    -webkit-transition: opacity 0.5s;
    transition: opacity 0.5s;
  }
  .cards .card .front, .cards .card .back {
    border-radius: 5px;
    position: absolute;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    width: 100%;
    height: 100%;
    background-color: White;
    -moz-backface-visibility: hidden;
    -webkit-backface-visibility: hidden;
    backface-visibility: hidden;
    -moz-transform: translateZ(0);
    -ms-transform: translateZ(0);
    -webkit-transform: translateZ(0);
    transform: translateZ(0);
    -moz-transition: -moz-transform 0.6s;
    -o-transition: -o-transform 0.6s;
    -webkit-transition: -webkit-transform 0.6s;
    transition: transform 0.6s;
    -moz-transform-style: preserve-3d;
    -webkit-transform-style: preserve-3d;
    transform-style: preserve-3d;
  }
  .cards .card .back {
    background-image: url("https://s3-us-west-2.amazonaws.com/s.cdpn.io/102308/card_backside.jpg");
    background-size: 90%;
    background-position: center;
    background-repeat: no-repeat;
    font-size: 12px;
  }
  .cards .card .front {
    -moz-transform: rotateY(-180deg);
    -ms-transform: rotateY(-180deg);
    -webkit-transform: rotateY(-180deg);
    transform: rotateY(-180deg);
    background-size: 90%;
    background-repeat: no-repeat;
    background-position: center;
  }
  .cards .card.flipped .back, .cards .card.found .back {
    -moz-transform: rotateY(180deg);
    -ms-transform: rotateY(180deg);
    -webkit-transform: rotateY(180deg);
    transform: rotateY(180deg);
  }
  .cards .card.flipped .front, .cards .card.found .front {
    -moz-transform: rotateY(0deg);
    -ms-transform: rotateY(0deg);
    -webkit-transform: rotateY(0deg);
    transform: rotateY(0deg);
  }
  .cards .card.found {
    opacity: 0.3;
  }

  .splash {
    position: absolute;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
  }
  .splash .overlay {
    position: absolute;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    background-color: rgba(0, 0, 0, 0.6);
  }
  .splash .content {
    position: absolute;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    width: 400px;
    height: 200px;
    margin: auto;
    text-align: center;
    background-color: rgba(51, 51, 51, 0.9);
    -moz-border-radius: 10px;
    -webkit-border-radius: 10px;
    border-radius: 10px;
    -moz-box-shadow: 5px 5px 20px rgba(0, 0, 0, 0.8);
    -webkit-box-shadow: 5px 5px 20px rgba(0, 0, 0, 0.8);
    box-shadow: 5px 5px 20px rgba(0, 0, 0, 0.8);
    padding: 1em;
  }
  .splash .content .title {
    font-size: 1.8em;
    padding: 0.5em;
  }
  .splash .content .score {
    padding: 0.5em;
  }
  .splash .content button {
    margin-top: 1.0em;
    background-color: #444;
    padding: 5px 20px;
    -moz-border-radius: 4px;
    -webkit-border-radius: 4px;
    border-radius: 4px;
    border: 1px solid #555;
    color: White;
    font-size: 1.4em;
  }

</style>
