<template>
  <NModal :show="isOpen">
    <NCard
      style="max-width: 600px"
      :title="songInfo.name_ja"
      :bordered="false"
      size="huge"
    >
      <template #header-extra>
        <div class="buttons">
          <NButton @click="setDifficulty(0)">初級</NButton>
          <NButton @click="setDifficulty(1)">上級</NButton>
          <NButton @click="setDifficulty(2)">超上級</NButton>
          <NButton @click="setDifficulty(3)">極上級</NButton>
        </div>
      </template>

      <div class="song-info">BPM: {{ songInfo.bpm }}</div>
      <div class="song-info">演奏時間: {{ songInfo.length }}</div>
      <div class="song-info">ノーツ数: {{ songInfo.notes[currentDif] }}</div>

      <NButton @click="handleClickNotesViewer">譜面確認</NButton>

      <template #footer>
        参考動画
        <div class="video-container">
          <iframe
            :src="`https://www.youtube.com/embed/${getYouTubeId(
              songInfo.movie[currentDif]
            )}`"
            class="video"
            frameborder="0"
            allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
            allowfullscreen
          ></iframe>
        </div>
      </template>
    </NCard>
  </NModal>
</template>

<script lang="ts">
import { ref, defineComponent, SetupContext, PropType, computed } from 'vue'
import { NButton, NModal, NCard } from 'naive-ui'
import { SongData } from '../App.vue'

export default defineComponent({
  name: 'Header',
  components: {
    NButton,
    NModal,
    NCard,
  },
  props: {
    isOpen: {
      type: Boolean as PropType<boolean>,
      default: false,
    },
    songInfo: {
      type: Object as PropType<SongData>,
      default: {},
    },
  },
  setup: (props, context: SetupContext) => {
    const currentDif = ref(1)
    const setDifficulty = (dif: number) => {
      console.log(dif)
      currentDif.value = dif
    }
    const imgSrc = computed(() => 'https://i.imgur.com/N9GiLVH.png')

    const handleClickNotesViewer = () => {
      context.emit('onClickNotesViewer', currentDif.value)
      window.open(imgSrc.value, '_blank')
    }

    const getYouTubeId = (url: string) => {
      const regExp =
        /^.*(youtu.be\/|v\/|u\/\w\/|embed\/|watch\?v=|&v=)([^#&?]*).*/
      const match = url.match(regExp)

      return match && match[2].length === 11 ? match[2] : null
    }
    return { currentDif, setDifficulty, getYouTubeId, handleClickNotesViewer }
  },
})
</script>

<style scoped>
.buttons {
  margin-top: 4px;
}
.video-container {
  position: relative;
  width: 100%;
  height: 0;
  padding-bottom: 56.25%;
}
.video {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
</style>
