<template>
  <div class="cta">
    <div class="cta__con">
      <div class="cta__con--info">{{$t("message.callToAction_signUp")}}</div>
      <form class="cta__con__form" @submit="formSubmit">
        <input
          class="cta__con__form--input"
          type="text"
          placeholder="example@mail.com"
          v-model="email"
        />
        <div>
          <div v-if="sent">
            <button class="cta__con__form--button">{{$t("message.callToAction_sending")}}</button>
          </div>
          <div v-else>
            <button class="cta__con__form--button">{{$t("message.callToAction_send")}}</button>
          </div>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
const url = "https://944pr8gv2g.execute-api.us-east-1.amazonaws.com/dev/member";

export default {
  data() {
    return {
      email: "",
      sent: false
    };
  },
  methods: {
    formSubmit(e) {
      e.preventDefault();
      this.sent = true;
      let currentObj = this;
      this.axios
        .post(url, {
          emailAddress: this.email
        })
        .then(response => {
          //console.log(response);
          currentObj.output = response.data;
          this.sent = false;
        })
        .catch(error => {
          //console.log(error);
          currentObj.output = error;
          this.sent = false;
        })
        .finally(() => {
          this.sent = false;
        });
    }
  }
};
</script>

<style scoped>
.cta {
  width: 100%;
  background-color: #f958ff;
}

.cta__con {
  padding: 1em 1em;
  background-color: #f958ff;
  height: 8em;
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-direction: column;
}
.cta__con--info {
  color: white;
}
.cta__con__form {
  display: flex;
  flex-direction: row;
  align-items: center;
  transition: all 0.3s cubic-bezier(0.05, 0.03, 0.35, 1);
}

.cta__con__form--input {
  margin-top: 0.5em;
  border-top-left-radius: 7px;
  border-bottom-left-radius: 7px;
  border: none;
  text-indent: 1em;
  width: 100%;
  font-size: 1em;
  line-height: 2em;
  transition: all 0.3s cubic-bezier(0.05, 0.03, 0.35, 1);
}
.cta__con__form--button {
  margin-top: 0.5em;
  border-top-right-radius: 7px;
  border-bottom-right-radius: 7px;
  border: none;
  font-size: 1em;
  line-height: 2em;
  padding: 0em 1em;
  background-color: #edf2f7;
  color: rgb(39, 37, 37);
  transition: all 0.3s cubic-bezier(0.05, 0.03, 0.35, 1);
}

.cta__con__form--button:hover {
  background-color: #e0e3e6;
}

@media screen and (min-width: 425px) {
  .cta__con {
    height: 6em;
    flex-direction: row;
  }
}
@media screen and (min-width: 450px) {
}
@media screen and (min-width: 650px) {
  .cta__con {
    flex-direction: row;
    height: 5em;
  }
}
@media screen and (min-width: 768px) {
  .cta__con {
    padding: 1em 0em;

    width: 768px;
    margin: 0 auto;
  }
}
</style>
