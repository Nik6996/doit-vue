<template>
  <div>
    <div class="teams">
      <div class="teams__top">
        <div class="teams__item center">Rank</div>
        <div class="teams__item">name</div>

        <div class="teams__item">Total (year)</div>
        <div class="teams__item">Total (OVERAl)</div>
      </div>
      <div
        class="teams__content"
        v-for="(player, index) in returnSortTeams"
        :key="player.id"
      >
        <preview-teams :rank="index" v-model="returnSortTeams[index]" />
      </div>

      <div class="teams__pagination">
        <div @click="minus()" class="teams__less"></div>
        <div
          class="teams__page"
          :class="{ 'current-page': page === pageNumber }"
          v-for="page in totalPage"
          :key="page"
          @click="changePage(page)"
        >
          {{ page }}
        </div>
        <div @click="plus()" class="teams__more"></div>
      </div>
    </div>
  </div>
</template>

<script>
import PreviewTeams from "@/components/top/PreviewTeams";
import { mapGetters } from "vuex";
export default {
  data() {
    return {
      pageNumber: 1,
      limitTeams: 10,
      totalPage: 0,
    };
  },
  components: {
    PreviewTeams,
  },
  computed: {
    ...mapGetters({
      getTeams: "team/getTeamsArr",
    }),

    returnSortTeams() {
      return this.getTeams
        .sort((a, b) => (a.totalPrizeYear < b.totalPrizeYear ? 1 : -1))
        .slice(
          (this.pageNumber - 1) * this.limitTeams,
          this.pageNumber * this.limitTeams
        );
    },
  },
  watch: {
    getTeams: {
      handler(getTeams) {
        this.totalPage = Math.ceil(getTeams.length / this.limitTeams);
      },
    },
  },
  async mounted() {
    await this.$store.dispatch("team/loadAll");
  },
  methods: {
    changePage(pageNumber) {
      this.pageNumber = pageNumber;
    },
    plus() {
      if (this.pageNumber !== this.totalPage) {
        this.pageNumber += 1;
      }
    },
    minus() {
      if (this.pageNumber !== 1) {
        this.pageNumber -= 1;
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.teams {
  border-left: 2px solid #242b33;
  border-right: 2px solid #242b33;
  border-bottom: 2px solid #242b33;
  margin-bottom: 100px;
  &__top {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr 1fr;
    border-bottom: 2px solid #242b33;
    margin-bottom: 30px;
  }
  &__item {
    display: flex;
    text-transform: uppercase;
    padding: 30px 15px 24px 15px;
    font-weight: 700;
    font-size: 16px;
    color: #e6e6e6;
  }
  &__pagination {
    display: flex;
    justify-content: center;
    padding: 20px 0px;
    border-top: 2px solid #242b33;
    align-items: center;
  }
  &__page {
    color: #ffffff;
    font-weight: 400;
    font-size: 16px;
    cursor: pointer;
    padding: 5px;
  }
  &__more {
    width: 15px;
    height: 15px;
    transform: rotate(180deg);
    cursor: pointer;
    font-size: 20px;
    color: white;
    margin: 0px 20px;
    background-image: url("../../assets/icon/arrow-top.svg");
    background-repeat: no-repeat;
  }
  &__less {
    width: 15px;
    height: 15px;
    cursor: pointer;
    font-size: 20px;
    color: white;

    margin: 0px 20px;
    background-image: url("../../assets/icon/arrow-top.svg");
    background-repeat: no-repeat;
  }
}
@media (max-width: 1060px) {
  .teams {
    &__item {
      padding: 25px 15px 0px 15px;
      font-weight: 500;
      font-size: 10px;
    }
    &__top {
      grid-template-columns: 1fr 1fr 1fr 1fr;
      border-bottom: 0;
      margin-bottom: 30px;
    }
  }
}
.center {
  justify-content: center;
}
.current-page {
  color: #2787f6;
  font-weight: 500;
  transform: scale(1.2);
  transition: all 0.3s;
}
</style>