<template>
    <v-ons-page>
      <v-ons-toolbar>
        <div class="center">{{ title }}</div>
        <div class="right">
          <v-ons-toolbar-button>
            <v-ons-icon icon="ion-navicon, material: md-menu"></v-ons-icon>
          </v-ons-toolbar-button>
        </div>        
      </v-ons-toolbar>

      <v-ons-button v-on:click="showDialog" modifier="large" style="margin: 6px 0">
        新規作成
      </v-ons-button>

      <v-ons-list>
        <v-ons-list-item v-for="memo in memo_list">
          <v-ons-list v-if="memo.importance">
            <v-ons-list-item style="color:red">{{ memo.date }}</v-ons-list-item>
            <v-ons-list-item style="color:red">{{ memo.content }}</v-ons-list-item>
          </v-ons-list>
          <v-ons-list v-else>
            <v-ons-list-item>{{ memo.date }}</v-ons-list-item>
            <v-ons-list-item>{{ memo.content }}</v-ons-list-item>
          </v-ons-list>
        </v-ons-list-item>
      </v-ons-list>

      <v-ons-dialog :visible.sync="dialogVisible">
        <v-ons-list>
          <v-ons-list-header>日時</v-ons-list-header>
          <v-ons-list-item>
            <v-ons-input float v-model="date"></v-ons-input>
          </v-ons-list-item>
          <v-ons-list-header>メモ</v-ons-list-header>
          <v-ons-list-item>
            <v-ons-input float v-model="content"></v-ons-input>
          </v-ons-list-item>
          <v-ons-list-header>重要</v-ons-list-header>
          <v-ons-list-item>
            <v-ons-switch v-model="importance">
            </v-ons-switch>
          </v-ons-list-item>
        </v-ons-list>

        <v-ons-button v-on:click="closeDialog" modifier="large" style="margin: 6px 0">
          保存
        </v-ons-button>
      </v-ons-dialog>

    </v-ons-page>
</template>
<script>
  export default{
    data() {
      return {
        title: "メモアプリ",
        dialogVisible: "false",
        date: "",
        content: "牛乳の購入",
        importance: "false",
        memo_list: []
      };
    },
    methods: {
      showDialog(){
        this.dialogVisible = true;
        this.date = new Date().toDateString(); 
        this.importance = false;
      },
      closeDialog(){
        this.dialogVisible = false;

        let memo = {
          "date": this.date,
          "content": this.content,
          "importance": this.importance
        }

        this.memo_list.push(memo);
      }
    }
  };
</script>
