<template>
  <div class="schedule">
    <loading v-if="mostrar"></loading>
    <div class="item" v-else>
      <div
        class="lol"
        :class="{ 'change-style': item.today == true }"
        v-for="(item, index) in schedules"
        :key="index"
      >
        <div class="shudleCourses">
          <p style="z-index:5;" v-html="item.day"></p>
          <p class="shudleCourses-number" v-html="item.number"></p>
        </div>
        <div class="hideBubble">
          <bubble
            class="shudleCourses-Courses"
            v-for="(item, index) in item.courses"
            :key="index"
            :item="item"
          >
          </bubble>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mapState } from "vuex";
import bubble from "@/components/bubble";
import loading from "@/components/loading";
export default {
  name: "Cursos",
  components: {
    bubble,
    loading
  },
  data() {
    return {
      circles: [],
      number: null,
      showBubble: true
    };
  },
  mounted() {
    this.$store.dispatch("getSchedule");
  },
  computed: {
    ...mapState(["schedules"]),
    ...mapState(["mostrar"])
  },
  methods: {}
};
</script>
<style>
.lol {
  height: calc(100vh - 70px);
}
.dessaperce-loading {
  display: none;
}
.schedule {
  display: flex;
  justify-content: center;
}
.shudleCourses {
  display: flex;
  -webkit-box-pack: center;
  justify-content: center;
  -webkit-box-align: center;
  align-items: center;
  height: 66px;
  position: relative;
}
.shudleCourses:nth-child(1) {
  font-size: 18px;
  font-weight: 700;
  z-index: 10;
}
.shudleCourses p {
  margin-bottom: 0px !important;
}
.shudleCourses-number {
  position: absolute;
  font-size: 73px;
  color: rgba(222, 222, 222, 0.74118);
}
.change-style {
  background: #f1f0f0;
}

.item {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  grid-gap: 8px;
  justify-content: center;
  width: 100%;
  max-width: 1290px;
}
.shudleCourses-Courses {
  align-items: center;
  position: relative;
  margin-top: 8px;
  margin-left: 5px;
  margin-right: 5px;
  margin-bottom: 13px;
  color: white;
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  border-radius: 27px;
  padding: 20px;
  min-height: 210px;
  color: #504d4d;
  border: 1px solid #c7c7c7;
}
.shudleCourses-CoursesStyle {
  position: absolute;
  transform: rotate(180deg);
  right: 12px;
  bottom: 14px;
  width: 14px;
  height: 14px;
  border-radius: 32px;
}
.shudleCourses-Courses p:nth-child(1) {
  font-size: 12px;
  color: #e2dada;
  font-weight: 400;
}
.shudleCourses-Courses p:nth-child(2) {
  font-size: 12px;
  font-weight: 600;
}
.shudleCourses-Courses p:nth-child(3) {
  font-size: 12px;
}
.shudleCourses-Courses p:nth-child(4) {
  font-size: 12px;
}
.shudleCourses-Courses p:nth-child(5) {
  font-size: 12px;
}

@media (max-width: 730px) {
  .shudleCourses-number {
    font-size: 55px;
  }
  .item {
    grid-template-columns: repeat(1, 1fr);
    grid-gap: 0px;
  }

  .lol {
    height: auto;
    border-bottom: 0.5px solid #c5c1c1;
    padding: 10px 0;
  }
  .shudleCourses:nth-child(1) {
    z-index: 5;
  }
}
@media (max-width: 570px) {
}
@media (max-width: 400px) {
}
</style>
