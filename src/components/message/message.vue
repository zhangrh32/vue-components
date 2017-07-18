<template>
  <div class="showMessageBox" v-show="visible">
    <div class="mb"></div>
    <div class="showMessage flex lineC downC">
     <p class="flex downC">{{ message }}</p>
    </div>
  </div>
</template>

<script>
  export default {
    data () {
      return {
        visible: false,
        message: '',
        duration: 2000,
        type: 'info',
        closed: false,
        onClose: null,
        timer: null
      }
    },
    watch: {
      closed (newVal) {
        if (newVal) {
          this.visible = false
        }
      }
    },
    mounted () {
      this.startTimer()
    },
    methods: {
      close () {
        this.closed = true
        if (typeof this.onClose === 'function') {
          this.onClose(this)
        }
        this.$destroy(true)
        this.$el.parentNode.removeChild(this.$el)
      },

      startTimer () {
        this.visible = true
        if (this.duration > 0) {
          this.timer = setTimeout(() => {
            if (!this.closed) {
              this.close()
            }
          }, this.duration)
        }
      }
    }
  }
</script>
<style>
  .showMessage{
    position: absolute;
    top: 50%;
    left: 50%;
    margin-left: -124px;
    background: rgba(0, 0, 0, .5);
    box-shadow: 0 3px 24px 0 rgba(0,0,0,0.25);
    border-radius: 8px;
    width: 228px;
    height: 68px;
    padding: 0 10px;
    font-family: PingFangSC-light;
    font-size: 18px;
    color: #FFFFFF;
    letter-spacing: 0px;
    z-index: 9999;
    text-align: center;
    margin-top: -34px;
  }
  .showMessageBox, .showMessageBox .mb {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: 9999;
  }
  .showMessageBox .mb {
    background: #000000;
    opacity: 0.3;
  }
</style>
