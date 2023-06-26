<template>
  <div class="ground">
    <My-Header></My-Header>
    <My-Memo></My-Memo>
    <My-Footer></My-Footer>
  </div>
</template>

<script>
import MyHeader from "./MyHeader";
import MyMemo from "./MyMemo";
import MyFooter from "./MyFooter";
export default {
  components: { MyHeader, MyFooter, MyMemo },
};
</script>
