# Vue-Remita

A Vue package for Remita payment gateway.

## Installation

```
npm install vue vue-remita --save
# OR
yarn add vue-remita
```

### Example

```vue
<template>
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
    Make Payment
  </remita>
</template>

<script type="text/javascript">
import remita from "vue-remita";
export default {
  components: {
    remita,
  },
  data() {
    return {
      customerId: 140700251,
      remitakey: "PUBIC_KEY",
      firstName: "Foo",
      lastName: "Bar",
      email: "foobar@example.com",
      amount: 100000,
      narration: "bla bla",
    };
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
```

Please checkout [Remita Documentation](https://www.remita.net/developers/documentation/accept-payments#) for other available options you can add to the tag

## How to contribute ✨

1. Fork it!
2. Create your feature branch: `git checkout -b feature-name`
3. Commit your changes: `git commit -am 'Some commit message'`
4. Push to the branch: `git push origin feature-name`
5. Submit a pull request 😉😉

[follow me on twitter](https://twitter.com/ozorku)!

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE) file for details
