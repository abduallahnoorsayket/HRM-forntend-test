<template>
  <Master>
    <template v-slot:content>
      <div class="app-main__inner" id="axiosForm">
        <div class="app-page-title">
          <div class="page-title-wrapper">
            <div class="page-title-heading">
              <div class="page-title-icon">
                <i class="fas fa fa-cog icon-gradient bg-tempting-azure"></i>
              </div>
              Voice Customization
            </div>
          </div>
        </div>
        <div class="loader" v-if="loading"></div>
        <!-- v-if="permissions" -->
        <!-- -->
        <div class="main-card card" v-if="form_data">
          <div class="card-body">
            <form @submit.prevent="submitVoiceCustomization" autocomplete="off">
              <div class="form-group row mt-4">
                <label class="col-md-12 col-lg-2 col-form-label"
                  >Voice Accent preference
                  <span class="asterisk">*</span></label
                >
                <div class="col-md-12 col-lg-4">
                  <select
                    name="select"
                    id="month"
                    v-model="accent"
                    class="form-control"
                  >
                    <!-- <option value disabled>
                      {{
                        $store.getters.GET_SELECT +
                        " " +
                        $store.getters.GET_LANGUAGE +
                        " " +
                        $store.getters.GET_CODE
                      }}
                    </option> -->
                    <option
                      v-for="(voice, index) in voiceList"
                      :key="index"
                      :value="index"
                    >
                      {{ voice.name }} ({{ voice.lang }})
                    </option>
                  </select>
                  <!-- <div
                    :class="{
                      'invalid-feedback':
                        error_add_holiday && error_add_holiday.type,
                    }"
                    v-if="error_add_holiday && error_add_holiday.type"
                  >
                    {{ error_add_holiday.type[0] }}
                  </div> -->
                </div>
                <label class="col-md-12 col-lg-2 col-form-label"
                  >Voice Type <span class="asterisk">*</span></label
                >
                <div class="col-md-12 col-lg-4">
                  <p class="mt-2 ml-2">
                    <span class="mr-3">
                      <input
                        type="radio"
                        id="test1"
                        name="radio-group"
                        v-model="is_male"
                        value="true"
                        class="form-control"
                      />
                      <!-- :class="{'is-invalid':sprint_error && sprint_error.is_current}"
                            <span
                            :class="{'invalid-feedback':sprint_error && sprint_error.is_current}"
                            v-if="sprint_error && sprint_error.is_current"
                          >{{sprint_error.is_current[0] }}</span>-->
                      <label for="test1">Male</label>
                    </span>
                    <input
                      type="radio"
                      id="test2"
                      name="radio-group"
                      v-model="is_male"
                      value="false"
                      class="form-control"
                    />
                    <!--:class="{'is-invalid':sprint_error && sprint_error.is_current}"
                           <span
                          :class="{'invalid-feedback':sprint_error && sprint_error.is_current}"
                          v-if="sprint_error && sprint_error.is_current"
                        >{{sprint_error.is_current[0] }}</span>-->
                    <label for="test2">Female</label>
                  </p>
                </div>
              </div>
              <!--  new permission ui -->
              <div class="form-group row mt-3">
                <label class="col-md-12 col-lg-2 col-form-label"
                  >Voice Mode preference <span class="asterisk">*</span></label
                >
                <div class="col-md-12 col-lg-8">
                  <p class="mt-2 ml-0">
                    <span class="mr-3">
                      <input
                        type="radio"
                        id="test3"
                        name="radio-group-mode"
                        v-model="voice_mode"
                        value="FR"
                        class="form-control"
                      />
                      <!-- :class="{'is-invalid':sprint_error && sprint_error.is_current}"
                            <span
                            :class="{'invalid-feedback':sprint_error && sprint_error.is_current}"
                            v-if="sprint_error && sprint_error.is_current"
                          >{{sprint_error.is_current[0] }}</span>-->
                      <label for="test3">Friendly </label>
                    </span>
                    <span class="mr-3">
                      <input
                        type="radio"
                        id="test4"
                        name="radio-group-mode"
                        v-model="voice_mode"
                        value="FO"
                        class="form-control"
                      />
                      <!-- :class="{'is-invalid':sprint_error && sprint_error.is_current}"
                            <span
                            :class="{'invalid-feedback':sprint_error && sprint_error.is_current}"
                            v-if="sprint_error && sprint_error.is_current"
                          >{{sprint_error.is_current[0] }}</span>-->
                      <label for="test4">Formal</label>
                    </span>

                    <!--:class="{'is-invalid':sprint_error && sprint_error.is_current}"
                           <span
                          :class="{'invalid-feedback':sprint_error && sprint_error.is_current}"
                          v-if="sprint_error && sprint_error.is_current"
                        >{{sprint_error.is_current[0] }}</span>-->

                    <input
                      type="radio"
                      id="test5"
                      name="radio-group-mode"
                      v-model="voice_mode"
                      value="CO"
                      class="form-control"
                    />
                    <!--:class="{'is-invalid':sprint_error && sprint_error.is_current}"
                           <span
                          :class="{'invalid-feedback':sprint_error && sprint_error.is_current}"
                          v-if="sprint_error && sprint_error.is_current"
                        >{{sprint_error.is_current[0] }}</span>-->
                    <label for="test5">Corporate</label>
                  </p>
                </div>
              </div>
              <div class="form-group row mt-3">
                <label class="col-md-12 col-lg-2 col-form-label"
                  >Voice Volume <span class="asterisk">*</span></label
                >
                <div class="col-md-12 col-lg-4">
                  <input
                    type="range"
                    v-model="volume"
                    min="0"
                    max="1"
                    step="0.01"
                  />
                  <!-- oninput="this.nextElementSibling.value = this.value" -->
                  <!-- :class="{ 'is-invalid': SubTask_error_data && SubTask_error_data.progress }"
                      <div
                      :class="{ 'invalid-feedback': SubTask_error_data && SubTask_error_data.progress }"
                      v-if="SubTask_error_data && SubTask_error_data.progress"
                    >{{ SubTask_error_data.progress[0] }}</div>-->

                  <output class="float-right">{{ volume }}</output>
                  <!-- <div
                    v-if="SubTask_error_data && SubTask_error_data.progress"
                    class="alert alert-danger mt-4"
                    role="alert"
                  >
                    <strong>No progress given</strong>
                  </div> -->
                </div>
                <label class="col-md-12 col-lg-2 col-form-label"
                  >Voice Rate <span class="asterisk">*</span></label
                >
                <div class="col-md-12 col-lg-4">
                  <input
                    type="range"
                    v-model="speed"
                    min="0"
                    max="1"
                    step="0.01"
                  />
                  <!--  oninput="this.nextElementSibling.value = this.value" -->
                  <!-- :class="{ 'is-invalid': SubTask_error_data && SubTask_error_data.progress }"
                      <div
                      :class="{ 'invalid-feedback': SubTask_error_data && SubTask_error_data.progress }"
                      v-if="SubTask_error_data && SubTask_error_data.progress"
                    >{{ SubTask_error_data.progress[0] }}</div>-->

                  <output class="float-right">{{ speed }}</output>
                  <!-- <div
                    v-if="SubTask_error_data && SubTask_error_data.progress"
                    class="alert alert-danger mt-4"
                    role="alert"
                  >
                    <strong>No progress given</strong>
                  </div> -->
                </div>
              </div>
              <div class="form-group row mt-4">
                <label class="col-md-12 col-lg-2 col-form-label">Voice ON/OFF </label>
                <div class="col-md-12 col-lg-10">
                  <label class="switch">
                    <input type="checkbox" v-model="is_on" />
                    <span class="slider round"></span>
                  </label>
                </div>
              </div>
              <div class="form-group">
                <button
                  @submit.prevent="submitVoiceCustomization"
                  class="mt-2 btn btn-successs btn-lg float-right"
                >
                  {{ $store.getters.GET_SUBMIT }}
                </button>
              </div>
            </form>
          </div>
        </div>
      </div>
    </template>
  </Master>
</template>

<script>
import Master from "../layouts/Master";
import axios from "axios";
import Swal from "sweetalert2";

export default {
  name: "VoiceCustomization",
  components: { Master },
  data() {
    return {
      loading: false,
      name: null,
      selectedPermissions: [],
      permissions: null,
      all_permission: null,
      searchQuery: null,
      // new props
      // module_list:[],
      // model_list:[],

      group_error_data: {
        name: null,
      },
      // voice set up data
      form_data: null,
      synth: window.speechSynthesis,
      voiceList: [],
      accent: null,
      is_male: null,
      voice_mode: null,
      volume: null,
      speed: null,
      is_on: true,
    };
  },
  mounted() {
    // wait for voices to load
    // I can't get FF to work without calling this first
    // Chrome works on the onvoiceschanged function
    this.voiceList = this.synth.getVoices();
    this.synth.onvoiceschanged = () => {
      this.voiceList = this.synth.getVoices();
      // give a bit of delay to show loading screen
      // just for the sake of it, I suppose. Not the best reason
      // setTimeout(() => {
      //   this.isLoading = false;
      // }, 800);
    };

    // this.listenForSpeechEvents();
  },

  methods: {
    async submitVoiceCustomization() {
      const currentUserID = localStorage.getItem("id");
      const response = await axios
        .post("voice-config/", {
          accent: this.accent,
          is_male: this.is_male,
          voice_mode: this.voice_mode,
          // volume: this.volume / 100,
          // speed: this.speed / 10,
          volume: this.volume,
          speed: this.speed,
          is_on: this.is_on,
          user: currentUserID,
        })
        .then((response) => {
          // voicec config data start
          // if(){}
          localStorage.setItem("voice_config", JSON.stringify(response.data));
          localStorage.setItem("accent", response.data.accent);
          localStorage.setItem("voice_mode", response.data.voice_mode);
          localStorage.setItem("volume", response.data.volume);
          localStorage.setItem("speed", response.data.speed);
          localStorage.setItem("is_male", response.data.is_male);
          localStorage.setItem("is_on", response.data.is_on);
          Swal.fire({
            icon: "success",
            // title: "Yes...",
            text:
              this.$store.getters.GET_UPDATED +
              " " +
              this.$store.getters.GET_SUCCESSFULLY +
              "...",
          }).then((result) => {
            this.$router.push("voice-customization");
            this.$router.go();
            console.log(result);
          });
          console.log(response);
        })
        .catch((error) => {
          this.group_error_data = error.response.data;
        });
      console.log(response);
    },

    loadVoiceCustomization() {
      const currentUserID = localStorage.getItem("id");
      this.loading = true;
      axios
        .get("voice-config/", {})
        .then((response) => {
          this.form_data = response.data;
          // filter by user
          this.form_data.filter((element) => {
            if (element.user == currentUserID) {
              this.accent = element.accent;
              this.is_male = element.is_male;
              this.voice_mode = element.voice_mode;
              this.volume = element.volume;
              this.speed = element.speed;
              this.is_on = element.is_on;
            }
          });
        })
        .catch(function (error) {
          console.log(error);
        })
        .finally(() => {
          this.loading = false;
        });
    },
  },

  created() {
    this.loadVoiceCustomization();
  },

  computed: {},
};
</script>

<style scoped>
/* for toggle button */
.switch {
  position: relative;
  display: inline-block;
  width: 60px;
  height: 34px;
}

.switch input {
  opacity: 0;
  width: 0;
  height: 0;
}

.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #ccc;
  -webkit-transition: 0.4s;
  transition: 0.4s;
}

.slider:before {
  position: absolute;
  content: "";
  height: 26px;
  width: 26px;
  left: 4px;
  bottom: 4px;
  background-color: white;
  -webkit-transition: 0.4s;
  transition: 0.4s;
}

input:checked + .slider {
  background-color: #69c5a5;
}

input:focus + .slider {
  box-shadow: 0 0 1px #69c5a5;
}

input:checked + .slider:before {
  -webkit-transform: translateX(26px);
  -ms-transform: translateX(26px);
  transform: translateX(26px);
}

/* Rounded sliders */
.slider.round {
  border-radius: 34px;
}

.slider.round:before {
  border-radius: 50%;
}
/* range input */
input[type="range"] {
  -webkit-appearance: none;
  width: 100%;
  margin-top: 14px;
  /* background: red; */
}
input[type="range"]:focus {
  outline: none;
}
input[type="range"]::-webkit-slider-runnable-track {
  width: 100%;
  height: 8.4px;
  cursor: pointer;
  background: #69c5a5;
  border-radius: 5px;
}
input[type="range"]::-webkit-slider-thumb {
  border: 1px solid #69c5a5;
  height: 36px;
  width: 16px;
  border-radius: 5px;
  background: #ffffff;
  cursor: pointer;
  -webkit-appearance: none;
  margin-top: -14px;
}
input[type="range"]:focus::-webkit-slider-runnable-track {
  background: #69c5a5;
  border: none !important;
}
input[type="range"]:focus {
  border: none !important;
}
input[type="range"]::-moz-range-track {
  width: 100%;
  height: 8.4px;
  cursor: pointer;

  background: #69c5a5;
  border-radius: 5px;
}
input[type="range"]::-moz-range-thumb {
  border: 1px solid #69c5a5;
  height: 36px;
  width: 16px;
  border-radius: 5px;
  background: #ffffff;
  cursor: pointer;
  -webkit-appearance: none;
  margin-top: -14px;
}
input[type="range"]::-ms-track {
  width: 100%;
  height: 8.4px;
  cursor: pointer;
  background: transparent;
  border-color: transparent;
  border-width: 16px 0;
  color: transparent;
}
input[type="range"]::-ms-fill-lower {
  background: #69c5a5;
  border: 0.2px solid #010101;
  border-radius: 2.6px;
  box-shadow: 1px 1px 1px #000000, 0px 0px 1px #0d0d0d;
}
input[type="range"]::-ms-fill-upper {
  background: #69c5a5;
  border: 0.2px solid #010101;
  border-radius: 2.6px;
  box-shadow: 1px 1px 1px #000000, 0px 0px 1px #0d0d0d;
}
input[type="range"]::-ms-thumb {
  box-shadow: 1px 1px 1px #000000, 0px 0px 1px #0d0d0d;
  border: 1px solid #000000;
  height: 36px;
  width: 16px;
  border-radius: 3px;
  background: #ffffff;
  cursor: pointer;
}
input[type="range"]:focus::-ms-fill-lower {
  background: #69c5a5;
}
input[type="range"]:focus::-ms-fill-upper {
  background: #69c5a5;
}
</style>
