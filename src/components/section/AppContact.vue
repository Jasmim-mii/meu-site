<template>
  <div id="contact-home">
    <div class="contact-info">
      <img class="img" src="@/assets/contact/contact.png" alt="contatolloudtech" />
    </div>
    <div class="container">
      <form
        @submit.prevent="submitForm"
        action="https://api.staticforms.xyz/submit"
        method="post"
      >
        <!-- <input type="hidden" name="redirectTo" value="https://lloudtech.com.br/" /> -->
        <input
          type="hidden"
          name="accessKey"
          value="90fb5fea-dea9-4d04-ac9d-224e0caa08d6"
        />
        <div class="form-group">
          <label for="first_name">Nome:</label>
          <input
            type="text"
            id="first_name"
            name="first_name"
            v-model="first_name"
            required
          />
          <p v-if="errorFullname" class="text-info">
            Deve conter no minino 4 caracteres!
          </p>
        </div>
        <div class="form-group">
          <label for="last_name">Sobrenome:</label>
          <input
            type="text"
            id="last_name"
            name="last_name"
            v-model="last_name"
            required
          />
          <p v-if="errorFullname" class="text-info">
            Deve conter no minino 4 caracteres!
          </p>
        </div>
        <div class="form-group">
          <label for="email">Email:</label>
          <input type="email" id="email" name="email" v-model="email" />
        </div>

        <div class="form-group">
          <label for="massage">Mensagem:</label>
          <textarea
            id="massage"
            rows="5"
            cols="50"
            name="message"
            v-model="message"
            required
          ></textarea>
          <p v-if="errorMessage" class="text-info">
            Deve conter no minino 25 caracteres!
          </p>
        </div>

        <button type="submit">Enviar</button>
        <p v-if="messageSuccess" class="msgSuccess">{{ msgsuccess }}</p>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  components: {},
  data() {
    return {
      action: "https://api.staticforms.xyz/submit",
      first_name: "",
      last_name: "",
      email: "",
      message: "",
      isSent: false,
      errorFullname: false,
      errorMessage: false,
      messageSuccess: false,
      msgsuccess: "Mensagem enviado com sucesso!",
    };
  },
  methods: {
    submitForm() {
      // Lógica de envio do formulário
      this.isSent = true;

      if (this.first_name.length < 4) {
        this.errorFullname = true;
      } else {
        this.errorFullname = false;
      }

      //validação message
      if (this.message.length < 25) {
        this.errorMessage = true;
      } else {
        this.errorMessage = false;
      }

      // se não tiver erros
      if (!this.errorFullname && !this.errorMessage) {
        this.messageSuccess = true;
        this.first_name = "";
        this.last_name = "";
        this.email = "";
        this.message = "";
      }

      setTimeout(() => {
        this.messageSuccess = false;
      }, 10000);
    },
  },
};
</script>

<style scoped>
.msgSuccess {
  color: green;
  padding-top: 1rem;
}
.text-info {
  font-size: 0.8rem;
  transition: 0.2s;
  color: #ff0000;
}
#contact-home {
  display: grid;
  grid-template-columns: 1fr 1fr;
  @media screen and (max-width: 954px) {
    display: block;
  }
}
.contact-info {
  height: 100%;
  width: 100%;
  @media screen and (max-width: 954px) {
    padding: 5rem;
  }
}
.img {
  margin-top: 4rem;
  width: 80%;
  height: 40%;
}

.contact-container {
  padding: 2rem 2rem;

  @media screen and (max-width: 954px) {
    width: 85%;
  }
}
.container {
  padding: 20px;
  box-shadow: 0px 0px 20px #00000033;
  border-radius: 8px;
}
.form-group {
  margin-top: 20px;
  font-size: 1rem;
  color: #232323;
}
.form-group input,
.form-group textarea {
  width: 95%;
  display: block;
  padding: 5px;
  font-size: 18px;
  border: 1px solid rgba(128, 128, 128, 0.199);
  margin-top: 5px;
}
textarea {
  resize: none;
}
button {
  width: 30%;
  display: inline-block;
  border: none;
  padding: 20px;
  font-size: 1.2rem;
  border-radius: 0.2rem;
  cursor: pointer;
  margin-top: 10px;
  background: #000;
  color: #eee;
  @media screen and (max-width: 954px) {
    width: 100%;
  }
}
.card-contact {
  display: flex;
  padding-bottom: 0.8rem;
  align-items: center;
  gap: 1rem;
}
span .icon {
  font-size: 2.3rem;
  color: #074d66;
}
</style>
