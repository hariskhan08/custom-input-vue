<template>
  <Container>
    <ConditionalDiv>
      <span class="popuptext show" v-show="hoverShow" id="myPopup">
        <Icon
          @onClick="setCurrentField"
          :iconName="'envelope'"
          :text="'Link To Email'"
          :value="'email'"
        />
        <Icon
          @onClick="setCurrentField"
          :iconName="'file'"
          :text="'Link To Page'"
          :value="'page'"
        />
        <Icon
          @onClick="setCurrentField"
          :iconName="'mobile'"
          :text="'Link To Phone'"
          :value="'phone'"
        />
      </span>

      <Button
        @setState="setHoverState"
        v-show="!focus"
        class="btn-left"
        :class="hoverShow ? 'btn-active' : ''"
        :iconName="currentIcon"
      />

      <input
        @focus="toggleFocus(true)"
        @keyup="checkField"
        class="input-field"
        v-model="inputValue"
        :type="type"
        placeholder="URL"
      />

      <Button
        @setState="validator ? resetFocus() : null"
        class="btn-center"
        :class="validator ? 'validated' : null"
        :iconName="'check'"
        v-show="focus"
      />
      <Button
        @setState="resetState"
        class="btn-center"
        :class="validator ? 'validated' : null"
        :iconName="'trash'"
        v-show="!focus && validator"
      />
      <Button
        @setState="setActiveState"
        v-show="!focus"
        class="btn-right"
        :class="active ? 'btn-active' : ''"
        :iconName="'external-link-alt'"
      />
      <Button
        @setState="resetState"
        v-show="focus"
        class="btn-right"
        :iconName="'times'"
      />
    </ConditionalDiv>
  </Container>
</template>
<script lang="ts">
import { styled } from '@egoist/vue-emotion'
import Icon from './Icon.vue'
import Button from './Button.vue'

const Container = styled('div')`
  border: 1px solid black;
  border-radius: 2px;
`
const ConditionalDiv = styled('div')`
  position: relative;
  display: inline-block;
  cursor: pointer;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;

  & .popuptext {
    width: 160px;
    background-color: #555;
    color: #fff;
    text-align: center;
    border-radius: 6px;
    padding: 8px 0;
    position: absolute;
    z-index: 1;
    top: -164%;
    left: -40%;
    margin-left: -80px;

    &::after {
      content: '';
      position: absolute;
      top: 40%;
      left: 103%;
      margin-left: -5px;
      border-width: 5px;
      border-style: solid;
      border-color: #555 transparent transparent transparent;
      transform: rotate(-90deg);
    }
  }
`

export default {
  name: 'CustomInput',
  props: {
    type: String,
  },
  components: {
    Button,
    Icon,
    Container,
    ConditionalDiv,
  },
  data() {
    return {
      inputValue: '' as string,
      validator: false as boolean,
      focus: false as boolean,
      hoverShow: false as boolean,
      active: false as boolean,
      defaultInput: 'page' as string,
      currentIcon: 'paperclip' as string,
      validation: {
        email: /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/,
        phone: /0[0-9]{10}/,
        page: /(https?:\/\/(?:www\.|(?!www))[a-zA-Z0-9][a-zA-Z0-9-]+[a-zA-Z0-9]\.[^\s]{2,}|www\.[a-zA-Z0-9][a-zA-Z0-9-]+[a-zA-Z0-9]\.[^\s]{2,}|https?:\/\/(?:www\.|(?!www))[a-zA-Z0-9]+\.[^\s]{2,}|www\.[a-zA-Z0-9]+\.[^\s]{2,})/,
      },
    }
  },
  methods: {
    toggleFocus(value: boolean) {
      this.focus = value
      this.checkField()
    },
    setHoverState() {
      this.hoverShow = !this.hoverShow
    },
    setActiveState() {
      this.active = !this.active
    },
    setCurrentField(value: string, icon: string) {
      this.currentIcon = icon
      this.defaultInput = value
      this.hoverShow = !this.hoverShow
    },
    checkField() {
      if (this.validation[this.defaultInput].test(this.inputValue)) {
        this.validator = true
        return
      }
      this.validator = false
    },
    resetState() {
      this.resetValue()
      this.resetFocus()
      this.resetValidator()
    },
    resetFocus() {
      this.focus = false
    },
    resetValue() {
      this.inputValue = ''
    },
    resetValidator() {
      this.validator = false
    },
  },
}
</script>

<style scoped>
.btn-left {
  border: 0;
  background-color: whitesmoke;
  padding-top: 0.2rem;
  padding-bottom: 0.2rem;
}
.btn-right {
  border: 0;
  background-color: whitesmoke;
  padding-top: 0.2rem;
  padding-bottom: 0.2rem;
}
.btn-center {
  border: 0;
  background-color: orangered;
  padding-top: 0.2rem;
  padding-bottom: 0.2rem;
}

.validated {
  background-color: transparent;
}

.btn-active {
  background-color: darkred;
}

.btn-right:hover {
  background-color: lightgray;
  cursor: pointer;
  transition: ease-in-out;
  transform: 0.3s;
}
.btn-left:hover {
  background-color: lightgray;
  cursor: pointer;
  transition: ease-in-out;
  transform: 0.3s;
}

.input-field {
  border: 0;
  outline: 0;
  height: 30px;
}

/* Add animation (fade in the popup) */
@-webkit-keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
</style>
