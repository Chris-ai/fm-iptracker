<template>
  <div class="wrapper">
    <div class="container">
      <h2>IP Address Tracker</h2>

      <div class="input-field">
        <input
          id="ip_input"
          type="text"
          placeholder="Search for any IP address or domain"
        />
        <button v-on:click="search">
          <img src="../assets/icon-arrow.svg" alt="icon" />
        </button>
      </div>

      <div class="ip-container">
        <LocationComponent label="ip address" v-bind:info="ip_address" />
        <LocationComponent
          class="border-left"
          label="location"
          v-bind:info="location"
        />
        <LocationComponent
          class="border-left"
          label="timezone"
          v-bind:info="timezone"
        />
        <LocationComponent class="border-left" label="isp" v-bind:info="isp" />
      </div>
    </div>
  </div>
</template>

<script>
import LocationComponent from "@/components/LocationComponent";
// import axios from "axios";
// import API_KEY from "../../.env.local";

export default {
  components: { LocationComponent },
  data() {
    return {
      ip_address: "",
      location: "",
      timezone: "",
      isp: "",
    };
  },
  methods: {
    searchForIP(ip = "8.8.8.8") {
      fetch(
        `https://geo.ipify.org/api/v2/country,city,vpn?apiKey=${process.env.VUE_APP_API_KEY}&ipAddress=${ip}`
      )
        .then((response) => response.json())
        .then((json) => {
          // console.log(json);
          this.ip_address = json.ip;
          this.location = `${json.location.city}, ${json.location.country} ${json.as.asn}`;
          this.timezone = `UTC ${json.location.timezone}`;
          this.isp = json.isp;

          this.$emit("latLng", [json.location.lat, json.location.lng]);
        })
        .catch(() => {
          alert("Ups, something went wrong. Please, try again :/");
        });
    },
    search() {
      let input_value = document.getElementById("ip_input").value;

      this.searchForIP(input_value);
    },
  },
  mounted() {
    this.searchForIP();
  },
};
</script>

<style lang="scss">
.wrapper {
  width: 100%;
  height: 250px;
  background-image: url("../assets/pattern-bg.png");
  background-repeat: no-repeat;
  background-size: cover;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
  position: relative;
  padding: 1.5rem;
  transition: 0.3s ease all;

  h2 {
    color: #fff;
    font-weight: var(--fw-medium);
  }

  .input-field {
    width: 100%;
    max-width: 560px;
    position: relative;
    margin: 1.2rem 0;

    input {
      width: 100%;
      font-size: 12px;
      padding: 20px 18px;
      border-radius: 12px;
      border: none;
      outline: none;
      background: #fff;
    }

    button {
      position: absolute;
      top: 0;
      right: 0;
      bottom: 0;
      margin: auto;
      background: black;
      border-radius: 0 12px 12px 0;
      width: 55px;
      height: 100%;
      border: none;
      outline: none;
      cursor: pointer;
      transition: 0.3s ease all;
    }

    button:hover,
    button:focus {
      background: hsl(0, 0, 17%);
    }
  }

  .container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    position: absolute;
    z-index: 5;
    width: 100%;
    text-align: center;
    padding: 0 1.2rem;
  }

  .ip-container {
    width: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    max-width: 350px;
    background: #fff;
    border-radius: 12px;
  }

  @media (min-width: 650px) {
    .ip-container {
      margin-top: 2.6rem;
      display: flex;
      flex-direction: row;
      align-items: center;
      justify-content: space-around;
      max-width: 1000px;
      padding-top: 1.2rem;
    }

    .input-field {
      input {
        font-size: 18px;
      }
    }

    .border-left {
      position: relative;
    }

    .border-left::after {
      content: "";
      position: absolute;
      background: var(--dark-gray);
      opacity: 0.2;
      width: 1px;
      height: 70px;
      max-height: 70px;
      top: 0;
      left: -25px;
      bottom: 0;
      // right: 0;
      margin: auto;
    }
  }
}
</style>