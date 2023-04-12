<template>
  <div>
    <DinoSVG />
  </div>
</template>

<script>
import { random } from '@/utils'
import { character } from '../character.mixin'
import DinoSVG from './DinoSVG.vue'
import { LOOP, LOOP_EASE_IN_OUT } from '../../../constants'

const SONGS = [
  // To My Youth - Bol4
  'https://open.spotify.com/track/4gMPlHHAjOQnUrhsuqHivn?si=2b3faf4d797846b2',
  // Hope Not - Blackpink
  'https://open.spotify.com/track/3eZD5DZGibwxMAOaCMBg3k?si=420d8ca4dcc14223',
  // I Wish My Heart Would Reach You
  'https://open.spotify.com/track/10GxwL6cJ79Zx3zF6m6DLZ?si=076c9527d40b41d2',
  // Blueming - IU
  'https://open.spotify.com/track/4Dr2hJ3EnVh2Aaot6fRwDO?si=4723b33259424c47',
]

export default {
  name: 'DinoCharacter',
  components: { DinoSVG },
  mixins: [character],
  data() {
    return {
      rhythm: 0.3,
      song: random(1, 4),
    }
  },
  methods: {
    init() {
      const head = document.querySelector('.dino-head')
      const leftArm = document.querySelector('.dino-l-arm')
      const rightArm = document.querySelector('.dino-r-arm')
      const leftLeg = document.querySelector('.dino-l-leg')
      const rightLeg = document.querySelector('.dino-r-leg')
      const tail = document.querySelector('.dino-tail')
      const eye = document.querySelector('.dino-eye')
      const headphone = document.querySelector('.dino-headphone')
      const bright = document.querySelector('.dino-bright')
      const teeth1 = document.querySelector('#dino .teeth1')
      const teeth2 = document.querySelector('#dino .teeth2')
      const mouthChillout = document.querySelector('#dino .mouth-chillout')
      const mouth = document.querySelector('#dino .mouth')
      let rotationZ = this.rhythm * 32

      // dance to the song rythm


      // add song link
      document.querySelector('.dino-head').addEventListener('click', () => {
        window.open(SONGS[this.song - 1])
      })

      this.loop
        .addLabel('start', 0)
        .to(
          leftLeg,
          this.rhythm,
          {
            skewX: -20,
            transformOrigin: '50% 100%',
            ...LOOP,
          },
          'start'
        )
        .to(
          rightLeg,
          this.rhythm,
          {
            skewX: 20,
            transformOrigin: '50% 100%',
            ...LOOP,
          },
          'start'
        )
        .to(
          headphone,
          this.rhythm / 2,
          {
            scale: 1.1,
            transformOrigin: '20% 20%',
            ...LOOP,
          },
          'start'
        )
        .to(
          [leftArm, rightArm],
          this.rhythm,
          {
            yPercent: 20,
            ...LOOP_EASE_IN_OUT,
          },
          'start'
        )
        .to(
          tail,
          this.rhythm,
          {
            transformOrigin: '25% 50%',
            rotationZ: 20,
            ...LOOP_EASE_IN_OUT,
          },
          'start'
        )
        .to(
          head,
          this.rhythm,
          {
            transformOrigin: '85% 100%',
            rotationZ,
            ...LOOP_EASE_IN_OUT,
          },
          'start'
        )

      if (this.song > 2) {
        this.loop
          .fromTo(
            eye,
            0.01,
            {
              scaleY: 0.1,
              transformOrigin: '50% 50%',
            },
            {
              scaleY: 1,
              transformOrigin: '50% 50%',
              repeatDelay: 3,
              ...LOOP,
            },
            'start'
          )
          .fromTo(
            bright,
            0.01,
            {
              autoAlpha: 0,
            },
            {
              autoAlpha: 1,
              repeatDelay: 3,
              ...LOOP,
            },
            'start'
          )
      } else {
        this.loop.set(
          eye,
          {
            scaleY: 0.1,
            transformOrigin: '50% 50%',
          },
          'start'
        )
      }
    },
  },
}
</script>
