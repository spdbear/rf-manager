<template>
  <Header msg="リングフィットアドベンチャー リズムゲーム まとめ" />
  <NDataTable
    class="table"
    :columns="columns"
    :data="data"
    :row-props="rowProps"
    :max-height="1000"
  />
  <Viewer />
</template>

<script lang="ts">
import { h, defineComponent, ref } from "vue";
import Header from "./components/Header.vue";
import Viewer from "./components/Viewer.vue";
import { NDataTable, NTag } from "naive-ui";

type SongData = {
  id: number;
  name_ja: string;
  name_en: string;
  length: number;
  bpm: number | string;
  notes: number[];
  movie: string[];
};

export default defineComponent({
  name: "App",
  components: {
    Header,
    Viewer,
    NDataTable,
  },
  setup: () => {
    const columns = [
      {
        title: "曲名",
        key: "name_ja",
      },
      {
        title: "演奏時間",
        key: "length",
      },
      {
        title: "ノーツ数",
        key: "notes",
        render(row: SongData) {
          const notes = row.notes.map((tagKey, i) => {
            return h(
              NTag,
              {
                style: {
                  marginRight: "6px",
                },
                type: "info",
              },
              {
                default: () => `${tagKey}`,
              }
            );
          });
          return notes;
        },
      },
    ];
    const songList = ref<SongData[]>([]);
    fetch("https://api.sssapi.app/KeQDsJSy3pn3levK3pvKz")
      .then((response) => response.json())
      .then((data) => {
        songList.value = data as SongData[];
      });
    return {
      rowProps: (row) => {
        return {
          style: "cursor: pointer;",
          onClick: () => {
            console.info(row.id);
          },
        };
      },
      columns,
      data: songList,
    };
  },
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.table {
  margin-left: auto;
  margin-right: auto;
  max-width: 800px;
}
</style>
