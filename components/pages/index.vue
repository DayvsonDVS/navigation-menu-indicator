<template>
  <div class="navigation">
    <ul ref="activeElement">
      <li
        v-for="{ icon, color } in icons"
        class="list"
        :style="`--clr: ${color}`"
      >
        <a href="#">
          <span class="icon">
            <ion-icon :name="`${icon}-outline`"></ion-icon
          ></span>
        </a>
      </li>

      <div class="indicator"></div>
    </ul>
  </div>
</template>

<script setup lang="ts">
import 'assets/scss/main.scss'
import { ref } from 'vue'

const icons = [
  { icon: 'home', color: '#f44336' },
  { icon: 'person', color: '#ffa117' },
  { icon: 'chatbubble', color: '#0fc70f' },
  { icon: 'camera', color: '#2196f3' },
  { icon: 'settings', color: '#b145e9' }
]
const activeElement = ref<HTMLElement>()

onMounted(() => {
  const list = [...activeElement.value?.children!]

  list.map((el, index) => {
    if (index == 0) {
      el.classList.add('active')
    }
    el.addEventListener('click', () => {
      classRemove()
      el.classList.add('active')
    })
  })
  function classRemove() {
    list.map((el) => {
      el.classList.remove('active')
    })
  }
})
</script>

<style scoped lang="scss">
.navigation {
  align-items: center;
  background: #fff;
  border-radius: 10px;
  display: flex;
  height: 60px;
  justify-content: center;
  position: relative;
  width: 400px;
  ul {
    display: flex;
    width: 350px;
    li {
      list-style: none;
      position: relative;
      width: 70px;
      height: 60px;
      z-index: 2;
      &.active {
        a {
          .icon {
            background: var(--clr);
            color: #fff;
            transform: translateY(-27px);
            transition-delay: 0.25s;
            &::before {
              opacity: 0.5;
              transition-delay: 0.25s;
            }
          }
        }
      }
      @each $i in 1, 2, 3, 4, 5 {
        &:nth-child(#{$i}).active ~ .indicator {
          transform: translateX(calc(70px * ($i - 1)));
        }
      }
      a {
        position: relative;
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100%;
        width: 100%;
        .icon {
          position: relative;
          display: block;
          width: 55px;
          height: 55px;
          text-align: center;
          line-height: 65px;
          border-radius: 50%;
          color: #222327;
          font-size: 1.5em;
          transition: 0.5s;
          transition-delay: 0s;
          &::before {
            content: '';
            position: absolute;
            top: 10px;
            left: 0;
            width: 100%;
            height: 100%;
            background: var(--clr);
            border-radius: 50%;
            filter: blur(5px);
            opacity: 0;
            transition: 0.5s;
            transition-delay: 0s;
          }
        }
      }
    }
    .indicator {
      position: absolute;
      top: -35px;
      width: 70px;
      height: 70px;
      background: #fff;
      border-radius: 50%;
      z-index: 1;
      transition: 0.5s;
      &::before {
        content: '';
        position: absolute;
        width: 30px;
        height: 30px;
        background: transparent;
        left: -28px;
        top: 5px;
        border-radius: 50%;
        box-shadow: 15px 18px #fff;
      }
      &::after {
        content: '';
        position: absolute;
        width: 30px;
        height: 30px;
        background: transparent;
        right: -28px;
        top: 5px;
        border-radius: 50%;
        box-shadow: -15px 18px #fff;
      }
    }
  }
}
</style>
