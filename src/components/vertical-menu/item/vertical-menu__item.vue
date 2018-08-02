<template>
<div class="vertical-menu__item" @click="expand">
    <div class="vertical-menu__content">
        <div class="vertical-menu__text-wrap">
            <span class="vertical-menu__hint-text hoverMoveAnim" v-if="this.desc">{{desc}}</span>
            <h3 class="vertical-menu__heading hoverMoveAnim">{{title}}</h3>
        </div>
        <div class="vertical-menu__hint">
            <div class="arrowIconHolder">
                <svg id="circleArr" width="38px" height="38px" viewBox="0 0 38 38" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
                <desc>Created with Sketch.</desc>
                <defs></defs>
                <g id="Page-1" stroke="none" stroke-width="1" fill="none" fill-rule="evenodd">
                    <g id="menu" transform="translate(-369.000000, -461.000000)">
                        <g  transform="translate(370.000000, 462.000000)">
                            <g id="circleArr__arr" transform="translate(18.500000, 18.000000) rotate(-315.000000) translate(-18.500000, -18.000000) translate(9.000000, 12.000000)" fill="#000000">
                                <polygon fill="currentColor"  id="Rectangle-6" points="13 0 19 6.0437128 13 12"></polygon>
                                <rect fill="currentColor"  id="Rectangle-5" x="0" y="5" width="18" height="2"></rect>
                            </g>
                            <circle id="Oval-2" stroke="currentColor" stroke-width="2" cx="18" cy="18" r="18"></circle>
                        </g>
                    </g>
                </g>
            </svg>
            </div>
            <span class="vertical-menu__hint-text hoverMoveAnim" v-if="!this.desc">
				Смотреть проект
			</span>
        </div>
    </div>
	<img class="vertical-menu__img" v-if="this.img" :src="this.img" alt="">
</div>
</template>

<script>
import anime from "animejs";
import Typed from "typed.js";

export default {
  props: ["title", "img", "desc"],
  name: "VerticalMenuItem",
  mounted: function() {
    const circlePaint = anime({
      targets: "#circleArr circle",
      strokeDashoffset: 0,
      easing: "easeInCubic",
      duration: 600,
      delay: function(el, i, l) {
        return i * 200;
      }
    });
    const itemsAppearing = anime({
      targets: ".vertical-menu__item",
      opacity: 1,
      duration: 500,
      easing: "easeInCubic",
      delay: function(el, i, l) {
        return i * 200;
      }
    });
    const arrowAppearing = anime({
      targets: "#circleArr #circleArr__arr",
      opacity: 1,
      delay: 700,
      duration: 300
    });
  },
  methods: {
    expand: function() {
      // console.log("expanded");
    }
  },
  data() {
    return {
      expanded: false
    };
  }
};
</script>

<style lang="scss">
#circleArr__arr {
  opacity: 0;
}
.vertical-menu {
  &__item {
    width: 20vw;
    height: 100vh;
    cursor: pointer;
    display: flex;
    justify-content: center;
    position: relative;
    opacity: 0;
    align-items: flex-end;
    &:hover {
      .vertical-menu {
        &__heading {
          transform: translate3d(2vh, 0, 0);
        }
        &__hint-text {
          transform: translate3d(2vh, 0, 0);
        }
        &__img {
          opacity: 0.5;
          transform: translate3d(0, -2vh, 0);
        }
      }
      .arrowIconHolder {
        transform: rotate(0deg) translate3d(0, 0, 0);
      }
    }
  }
  &__img {
    position: absolute;
    width: 100%;
    top: 0;
    left: 0;
    height: calc(100% + 3vh);
    object-fit: cover;
    z-index: -1;
    opacity: 0;
    transition: all 0.8s ease-in-out;
    transform: translate3d(0, 0, 0);
  }
  &__content {
    transform: rotate(-90deg);
    position: absolute;
    width: 60vh;
    display: flex;
    align-content: stretch;
    flex-direction: column;
    height: 20vw;
    bottom: 40vh;
    padding-top: 1em;
  }
  &__heading {
    font-size: 1.23em;
    margin: 0;
    transition: all 0.5s ease-in-out;
    transform: translate3d(0, 0, 0);
  }
  &__hint-text {
    display: flex;
    font-size: 0.615em;
    font-family: "CourierNew";
    font-weight: 100;
    font-style: italic;
    opacity: 0.6;
    transition: 0.5s all 0.1s ease-in-out;
    transform: translate3d(0, 0, 0);
  }
  &__hint {
    display: flex;
    align-items: center;
    flex-direction: row-reverse;
    margin-left: 2.5em;
    width: max-content;
  }
  .arrowIconHolder {
    display: flex;
    align-items: center;
    justify-content: center;
    transform: rotate(-45deg) translate3d(0, 0, 0);
    transform-origin: center center;
    transition: all 0.5s ease-in-out;
    margin-left: 5vh;
  }
  &__text-wrap {
    & + * {
      margin-top: 0.1em;
    }
  }
}
</style>