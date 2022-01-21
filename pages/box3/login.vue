<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6" class="d-flex flex-column mb-6" style="text-align:center;">
        <v-dialog v-model="warnDialog" persistent max-width="290">
            <v-card color="#E53935">
                <v-card-title class="headline">警告</v-card-title>
                <v-card-text>严禁通过此功能进行盗号等不良行为</v-card-text>
                <v-card-actions>
                    <v-btn text @click="warnDialog = false">我知道了</v-btn>
                </v-card-actions>
            </v-card>
        </v-dialog>
        <h1>岛3-登录api</h1>
        <Box3Login />
    </v-col>
  </v-row>
</template>

<script>

export default {
  name: 'Box3LoginPage',
  data(){
      return{
        warnDialog:true
      }
  }
}
</script>