<template>
  <div class="App">
    <remita
      :customerId="customerId"
      :amount="amount"
      :email="email"
      :firstName="firstName"
      :lastName="lastName"
      :remitakey="remitakey"
      :narration="narration"
      :close="close"
    >
      Make payment
    </remita>
  </div>
</template>

<script type="text/javascript">
import remita from "../../src";

export default {
  components: {
    remita,
  },
  data() {
    return {
      customerId: 140700251,
      remitakey:
        "REVNT05UR0lGVHw0MDgyNTIxNHwxZTI1NGNlNTVhMzkyYTgxYjYyNjQ2ZWIwNWU0YWE4ZTNjOTU0ZWFlODllZGEwMTUwMjYyMTk2ZmFmOGMzNWE5ZGVjYmU3Y2JkOGI5ZWI5YzFmZWMwYTI3MGI5MzA0N2FjZWEzZDhiZjUwNDY5YjVjOGY3M2NhYjQzMTg3NzI4Mg==",
      firstName: "Foo",
      lastName: "Bar",
      email: "foobar@example.com",
      amount: 1000000,
      narration: "bla bla",
    };
  },
  computed: {
    genReference() {
      let text = "";
      let possible =
        "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789";

      for (let i = 0; i < 10; i++)
        text += possible.charAt(Math.floor(Math.random() * possible.length));

      return text;
    },
  },
  methods: {
    callback: function(response) {
      console.log(response);
    },
    close: function() {
      console.log("Payment closed");
    },
  },
};
</script>
<style>
.App {
  display: grid;
  place-items: center;
  height: 100vh;
}

.payButton {
  font-size: 16px;
  background: #b74420;
  padding: 10px 25px;
  color: white;
  border-radius: 3px;
  border: 0;
}
</style>
