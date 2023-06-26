<template>
  <div class="memo">
    <div class="act">
      <button class="btn btn-primary" @click="add()">+ 추가</button>
    </div>
    <ul>
      <li v-for="data in state.dataList" :key="data.id" @click="edit(data.id)">
        {{ data.content }}
      </li>
    </ul>
  </div>
</template>
<script>
import { reactive } from "vue";
import axios from "axios";
export default {
  setup() {
    // 데이터의 동적 변화를 주기 위해서 사용하는 vue 내장 함수. reactive
    const state = reactive({
      dataList: [],
    });

    // 메모 조회
    // frontend에서 backend로 url을 통해서 데이터를 요청 (HTTP request)
    axios.get("/api/memos").then((res) => {
      state.dataList = res.data;
    });

    // 메모 추가
    const add = () => {
      const content = prompt("내용을 입력해주세요");

      if (!content) {
        alert("내용을 입력해주세요");
        return add();
      }

      axios
        .post("/api/memos", { content })
        .then((res) => (state.dataList = res.data)); // axios를 통해서 데이터를 보내고 다시 받음
    };

    // 메모 수정
    const edit = (id) => {
      // 해당 id 값과 같은 데이터를 찾는다
      const content = prompt(
        "내용을 입력해주세요",
        state.dataList.find((data) => data.id === id).content
      );
      console.log(content);
      axios.put("/api/memos/" + id, { content }).then((res) => {
        state.dataList = res.data;
      });
    };

    return { state, add, edit };
  },
};
</script>
<style lang="scss" scoped>
.memo {
  .act {
    padding: 10px 10px 5px 5px;
    text-align: right;
  }

  ul {
    border-top: 1px solid #eee;
    list-style: none;
    padding: 0px;
    margin: 0px;
    li {
      padding: 15px;
      margin: 5px 0;
      border: 1px solid #eee;
    }
  }
}
</style>
