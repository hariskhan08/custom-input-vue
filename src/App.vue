<template>
  <Container>
    <CustomInput />
  </Container>
</template>

<script>
import { styled } from '@egoist/vue-emotion'
import CustomInput from './components/CustomInput.vue'
const Container = styled('div')`
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 90vh;
`
export default {
  name: 'App',
  components: {
    CustomInput,
    Container,
  },
}
</script>
