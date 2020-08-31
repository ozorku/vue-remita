<template>
  <button v-if="!embed" class="payButton" @click="payWithRemita">
    <slot>Make Payment</slot>
  </button>
  <div v-else id="remitaEmbedContainer" />
</template>

<script type="text/javascript">
export default {
  props: {
    remitakey: {
      type: String,
      required: true,
    },
    customerId: {
      type: Number,
      required: true,
    },
    email: {
      type: String,
      required: true,
    },
    firstName: {
      type: String,
      required: true,
    },
    lastName: {
      type: String,
      required: true,
    },
    amount: {
      type: Number,
      required: true,
    },
    narration: {
      type: String,
      required: true,
    },
    close: {
      type: Function,
      required: true,
      default: function() {},
    },
  },
  data() {
    return {
      scriptLoaded: null,
    };
  },
  created() {
    this.scriptLoaded = new Promise((resolve) => {
      this.loadScript(() => {
        resolve();
      });
    });
  },
  mounted() {
    if (this.embed) {
      this.payWithRemita();
    }
  },
  methods: {
    loadScript(callback) {
      const script = document.createElement("script");
      script.src =
        "https://remitademo.net/payment/v1/remita-pay-inline.bundle.js";
      document.getElementsByTagName("head")[0].appendChild(script);
      if (script.readyState) {
        // IE
        script.onreadystatechange = () => {
          if (
            script.readyState === "loaded" ||
            script.readyState === "complete"
          ) {
            script.onreadystatechange = null;
            callback();
          }
        };
      } else {
        // Others
        script.onload = () => {
          callback();
        };
      }
    },

    payWithRemita() {
      this.scriptLoaded &&
        this.scriptLoaded.then(() => {
          const paymentData = {
            key: this.remitakey,
            customerId: this.customerId,
            email: this.email,
            firstName: this.firstName,
            lastName: this.lastName,
            amount: this.amount,
            narration: this.narration,
            onSuccess: function(response) {
              console.log("callback Successful Response", response);
            },
            onError: function(response) {
              console.log("callback Error Response", response);
            },
            onClose: () => {
              this.close();
            },
          };

          if (this.embed) {
            paymentData.container = "remitaEmbedContainer";
          }

          const handler = RmPaymentEngine.init(paymentData);
          handler.showPaymentWidget();

          if (!this.embed) {
            handler.openIframe();
          }
        });
    },
  },
};
</script>
