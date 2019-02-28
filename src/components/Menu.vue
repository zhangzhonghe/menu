<template>
  <div class="container">
    <div :class="{'menu-item': true, hover: active !== option1, active: active !== option1 }"  @click.stop="onClickMenuItem(option1)">
      <span class="menu-item-title">选项一 {{ option1 }}</span>
      <img :class="{'img-active': active === option1}" src="../images/arrow.png" />
      <transition :name="animation ? 'unfold' : ''">
        <div class="submenu-container" v-if="active === option1">
          <Menu :index="active" @open="onOpen" @close="onClose" :true="animation"/>
        </div>
      </transition>
    </div>
    <div :class="{'menu-item': true, hover: active !== option2, active: active !== option2 }" @click.stop="onClickMenuItem(option2)">
      <span class="menu-item-title">选项二 {{ option2 }}</span>
      <img :class="{'img-active': active === option2}" src="../images/arrow.png" />
      <transition :name="animation ? 'unfold' : ''">
        <div class="submenu-container" v-if="active === option2">
          <Menu :index="active" @open="onOpen" @close="onClose" :animation="animation"/>
        </div>
      </transition>
    </div>
    <div :class="{'menu-item': true, hover: active !== option3, active: active !== option3 }"  @click.stop="onClickMenuItem(option3)">
      <span class="menu-item-title">选项三 {{ option3 }}</span>
      <img :class="{'img-active': active === option3}" src="../images/arrow.png" />
      <transition :name="animation ? 'unfold' : ''">
        <div class="submenu-container" v-if="active === option3">
          <Menu :index="active" @open="onOpen" @close="onClose" :animation="animation"/>
        </div>
      </transition>
    </div>
    <div :class="{'menu-item': true, hover: active !== option4, active: active !== option4 }"  @click.stop="onClickMenuItem(option4)">
      <span class="menu-item-title">选项四 {{ option4 }}</span>
      <img :class="{'img-active': active === option4}" src="../images/arrow.png" />
      <transition :name="animation ? 'unfold' : ''">
        <div class="submenu-container" v-if="active === option4">
          <Menu :index="active" @open="onOpen" @close="onClose" :animation="animation"/>
        </div>
      </transition>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Menu',
  props: {
    index: String,
    animation: Boolean
  },
  data () {
    return {
      active: ''
    }
  },
  components: {
    Menu: this
  },
  computed: {
    option1 () {
      if (this.index) {
        return this.index + '-' + '1'

      } else {
        return '1'
      }
    },
    option2 () {
      if (this.index) {
        return this.index + '-' + '2'

      } else {
        return '2'
      }
    },
    option3 () {
      if (this.index) {
        return this.index + '-' + '3'

      } else {
        return '3'
      }
    },
    option4 () {
      if (this.index) {
        return this.index + '-' + '4'

      } else {
        return '4'
      }
    },
  },
  methods: {
    onClickMenuItem (e) {
      if (this.active === e) {
        // 关闭当前选项
        this.active = ''

        this.$emit('close')

      } else {

        // 展开当前选项
        this.active = e

        this.$emit('open', { active: e })
      }

    },
    onOpen (e) {
      this.$emit('open', { active: e.active })
    },
    onClose () {
      this.$emit('close')
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  img {
    position: absolute;
    right: 0;
    width: 1.2em;
    height: 1.2em;
    vertical-align: middle;
  }

  .menu-item {
    padding: .5em 0 .5em 1em;
    background-color: #666;
    color: #eee;
    overflow: hidden;
  }

  .menu-item-title {
    cursor: pointer;
  }

  .hover:hover {
    background-color: #555;
  }

  .active:active {
    background-color: #454545;
  }

  .img-active {
    transform: rotate(90deg);
  }

  /* .submenu-container {
  } */

  /* 过渡动画 */
  .unfold-enter-active,
  .unfold-leave-active {
    transition: max-height .6s;
  }

  .unfold-enter,
  .unfold-leave-to {
    max-height: 0;
  }

  .unfold-leave,
  .unfold-enter-to {
    max-height: 200px;
  }

</style>
