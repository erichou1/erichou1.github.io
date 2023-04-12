<template>
  <SceneSection id="thanks">
    <TextBlock>
      <Potion isPlaying />

      <div class="madeof">
        <p class="-comment">// Made with</p>

        <div class="cols">
          <ul class="col">
            <li class="ico">(){&lt;/&gt;}</li>
            <li>Vue 2</li>
            <li>GSAP 2</li>
            <li>ScrollMagic</li>
            <li>Photoshop</li>
            <li>Illustrator</li>
            <li>Svgator</li>
          </ul>
          <ul class="col">
            <li class="ico">~</li>
            <li>+20 cups of coffee</li>
            <li>Too Much Stack Overflow</li>
            <li>2 easter eggs</li>
          </ul>
          <ul class="col songs">
            <li class="ico">
              <MusicIcon />
            </li>
            <li v-for="song in SONGS" :key="song.id">
              <a
                :href="SPOTIFY_TRACK + song.id"
                :title="`Listen to ${song.label}`"
                target="_blank"
                >{{ song.label }}</a
              >
            </li>
          </ul>
        </div>
      </div>
    </TextBlock>
  </SceneSection>
</template>

<script>
import MusicIcon from '../Icon/MusicIcon.vue'
import Potion from '../Characters/Potion/Potion.vue'
import TextBlock from '../TextBlock.vue'
import SceneSection from '../SceneSection.vue'

const SPOTIFY_TRACK = 'https://open.spotify.com/track/'
const SONGS = [
  {
    id: '4gMPlHHAjOQnUrhsuqHivn?si=2b3faf4d797846b2',
    label: 'To My Youth - BOL4',
  },

  {
    id: '3eZD5DZGibwxMAOaCMBg3k?si=420d8ca4dcc14223',
    label: 'Hope Not - Blackpink',
  },

  {
    id: '10GxwL6cJ79Zx3zF6m6DLZ?si=076c9527d40b41d2',
    label: 'I Wish My Heart Would Reach You - U Sung Eun',
  },

  {
    id: '4Dr2hJ3EnVh2Aaot6fRwDO?si=4723b33259424c47',
    label: 'Blueming - IU',
  },

  {
    id: '6TBJkXHPhu3EsMk1bshwuI?si=002a15c8de804b69',
    label: 'Only - Leehi',
  },

  {
    id: '3SfbB0Y3saMIQnNctxMVhj?si=5ea13172fbda41d0',
    label: 'I Miss You - SOYOU',
  },
]

export default {
  name: 'ThanksScene',
  components: { TextBlock, SceneSection, Potion, MusicIcon },
  props: {
    isPlaying: Boolean,
  },
  data() {
    return {
      SPOTIFY_TRACK,
      SONGS,
    }
  },
}
</script>

<style lang="scss">
#thanks {
  position: relative;

  &:before {
    content: '';
    display: block;
    position: absolute;
    top: 0;
    left: 0;
    z-index: -1;
    width: 100%;
    height: 100%;
    opacity: 0.3;
    mask-image: linear-gradient(to bottom, transparent 0, black 10vh);
    background: url('../../assets/goya.png') no-repeat 0 bottom;
    background-size: auto 100%;
  }

  .madeof {
    margin-bottom: 20vh;
  }

  .-big {
    a:hover {
      filter: brightness(1.4);
    }
  }

  .cols {
    display: grid;
    grid-template: 1fr / repeat(auto-fit, minmax(150px, auto));
    grid-gap: 2rem;
    color: var(--purple);
    font-size: 1rem;

    li.ico {
      min-height: 0;
      margin-bottom: 2rem;
    }

    svg {
      width: 1rem;
      height: 1rem;
      fill: var(--purple);
    }
  }

  a {
    text-decoration: none;
    display: block;
    min-height: 2rem;
  }

  ul,
  li {
    list-style: none;
    margin: 0;
    padding: 0;
    position: relative;
    line-height: 1.5em;
  }

  .songs {
    li {
      float: left;
      clear: left;
      transition: all 300ms ease-out;
      cursor: pointer;

      &.ico {
        display: block;
      }

      a {
        color: var(--purple);
      }

      a:hover {
        color: var(--light);
      }
    }
  }

  @media screen and (max-width: 768px) {
    li {
      margin-bottom: 0.5rem;
    }
  }
}
</style>
