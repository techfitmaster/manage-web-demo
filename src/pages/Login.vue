<template>
  <v-app>
    <v-content>
      <v-container fluid fill-height>
        <v-layout align-center justify-center>
          <v-flex xs12 sm8 md2>
            <v-card class="elevation-12">
              <v-toolbar wirte color="">
                <v-spacer></v-spacer>
                <v-toolbar-title>欢迎登陆</v-toolbar-title>
                <v-spacer></v-spacer>
              </v-toolbar>
              <v-card-text>
                <v-form>
                  <v-text-field
                    prepend-icon="person"
                    v-model="username"
                    label="用户名"
                    type="text"
                    :rules="['用户名不能为空']"
                  />
                  <v-text-field
                    prepend-icon="lock"
                    v-model="password"
                    label="密码"
                    id="password"
                    :append-icon="e1 ? 'visibility' : 'visibility_off'"
                    :append-icon-cb="() => (e1 = !e1)"
                    :type="e1 ? 'text' : 'password'"
                    :rules="['密码不能为空']"
                  ></v-text-field>
                </v-form>
              </v-card-text>
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn color="primary" @click="doLogin">登录</v-btn>
                <v-spacer></v-spacer>
              </v-card-actions>
            </v-card>
          </v-flex>
        </v-layout>
      </v-container>
    </v-content>
    <v-dialog v-model="dialog" width="300px">
      <v-alert icon="warning" color="error" :value="true">
        用户名和密码不能为空
      </v-alert>
    </v-dialog>
  </v-app>
</template>

<script>
  export default {
    data: () => ({
      username: "",
      password: "",
      dialog: false,
      e1: false
    }),
    methods: {
      doLogin() {
        if (!this.username || !this.password) {
          return false;
        }
        //后台请求
        console.log(this.username + " ... " + this.password);
        this.$http().then(
          () => {
            this.$router.push("/index/dashboard");
            this.$message.success("登陆成功")
          }
        ).catch(
          () => {
            this.$router.push("/index/dashboard");
            this.$message.error("登陆失败")
          }
        )


      }
    }
  };
</script>
