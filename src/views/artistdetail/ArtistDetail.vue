<template>
  <div class="artist-detail">
    <scroll ref="scroll" class="artist-scroll-c">
      <artist-base-info :desc="artistDesc" :base-info="artist" />
      <artist-bar :list="barlist" />
      <router-view></router-view>
    </scroll>
  </div>
</template>
<script>
import Scroll from "components/common/scroll/Scroll";

import ArtistBaseInfo from "./childComps/ArtistBaseInfo";
import ArtistBar from "./childComps/ArtistBar";
import { _getArtistDesc,} from "network/artist";
import { _getSongsDetail, songDetail } from "network/detail";
export default {
  name: "ArtistDetail",
  data() {
    return {
      artist: null,
      artistDesc: null,
      barlist: ["专辑", "歌手详情", "相似歌手"],
    };
  },
  components: {
    Scroll,
    ArtistBaseInfo,
    ArtistBar
  },
  created() {
    setTimeout(()=>{
      this.artist = this.$store.state.artist;
    if (this.artist.id != null) {
      _getArtistDesc(this.artist.id).then(res => {
        this.artistDesc = res.data.briefDesc;
      });
    }
    },200)
  },
};
</script>
<style scoped>
.artist-detail {
  width: 100%;
  height: 100%;
  overflow: hidden;
}
.artist-scroll-c {
  height: calc(100% - 59px);
}
</style>