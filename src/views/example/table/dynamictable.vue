<template>
  <div class="app-container">
    <div style='margin:0 0 5px 20px'>固定表头 按照表头顺序排序</div>
    <fixed-thead/>

  </div>
</template>

<script>
  import fixedThead from './dynamictable/animationtable'
  import unfixedThead from './dynamictable/unfixedThead'

  export default {
    components: { fixedThead, unfixedThead }
  };
</script>

