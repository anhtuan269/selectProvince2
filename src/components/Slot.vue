<template>
  <div class="alo">
    <div class="title">
      <slot name="title"></slot>
      <slot name="slotdefault"> 
        <p class="default">this is slot default </p>
      </slot>
    </div>
    <div class="content">
      <slot name="content"></slot>
      <slot></slot>
    </div>
  </div>
</template>

<script>
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.alo {
    margin-top: 60px;
}
.alo .default {
  color: red;
}
</style>

