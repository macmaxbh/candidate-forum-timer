<template>
  <header class="is-primary is-bold container">
    <div class="hero-body">
      <div class="our-header container">
        <div class="logo-img">
          <img src="../assets/just_homes_logo.png" alt="MVMHA logo" />
        </div>
        <div class="header-text">
          <h1 class="title">
            2020
            <span>Mountain View</span>
            <span>City Council</span>
            <span>Candidate Forum</span>
          </h1>
          <h2 class="subtitle">
            Hosted by the
            <span>Mountain View Mobile Home Alliance</span>
          </h2>
        </div>
        <div class="buttons box">
          <div>
            <a href="#" class="btn" @click.prevent="shuffleCandidates()">
              Shuffle
              <i class="material-icons right">shuffle</i>
            </a>
            <div class="switch">
              <label>
                <input type="checkbox" v-model="galleryMode" @click="updateGalleryMode()" />
                <span class="lever"></span>
                Show All
              </label>
            </div>
          </div>

          <div class="time-setters-global">
            <a href="#" class="btn" @click.prevent="setTime(30)">
              30
              <i class="material-icons left">timer</i>
            </a>
            <a href="#" class="btn" @click.prevent="setTime(60)">
              60
              <i class="material-icons left">timer</i>
            </a>
            <a href="#" class="btn" @click.prevent="setTime(90)">
              90
              <i class="material-icons left">timer</i>
            </a>
          </div>
          <div>
            <a href="#" class="btn" @click.prevent="focusChange(-1)">
              Prev
              <i class="material-icons left">navigate_before</i>
            </a>
            <span>{{focusedCandidate}}</span>
            <a href="#" class="btn" @click.prevent="focusChange(1)">
              Next
              <i class="material-icons right">navigate_next</i>
            </a>
          </div>
        </div>
      </div>
    </div>
  </header>
</template>
<script lang="ts">
import { Component, Vue, Prop, Emit } from "vue-property-decorator";
import moment from "moment";
import { Candidate } from "./candidates";

@Component({})
export default class Header extends Vue {
  @Prop()
  candidatesList?: Candidate[];

  @Prop()
  galleryMode?: boolean;

  @Prop()
  focusedCandidate?: number;

  @Emit()
  shuffleCandidates() {}

  @Emit()
  focusChange(num: -1 | 1) {
    return num;
  }

  @Emit("update:galleryMode")
  updateGalleryMode() {
      return !this.galleryMode;
  }

  setTime(time: number) {
    this.candidatesList
      ?.map((candidate) => candidate.timer)
      .forEach((timer) => {
        timer.setTime(time, "s");
      });
  }
}
</script>
<style lang="scss" scoped>
.our-header {
  display: flex;
  > div {
    flex: 1;
  }
  > div.logo-img {
    flex: 0 1 auto;
    margin-right: 2em;
    img {
      height: 5em;
      width: auto;
    }
  }
  .header-text {
    padding-right: 1em;
  }
  .buttons {
    display: flex;
    flex-direction: column;
    align-items: flex-end;
    flex: 0 1 auto;
    width: fit-content;
    > div {
      flex: 0 1 auto;
      margin-bottom: 8px;
      display: flex;
      justify-content: space-between;
      width: 100%;
      > * {
        flex: 0 1 auto;
        margin-right: 4px;
      }
    }
  }
  .title span,
  .subtitle span {
    display: inline-block;
  }
}
</style>