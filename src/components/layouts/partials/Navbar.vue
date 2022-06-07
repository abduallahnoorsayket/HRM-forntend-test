<template>
  <div class="app-header header-shadow">
    <div class="app-header__logo">
      <router-link :to="{ name: 'Dashboard' }">
        <div class="logo-src ml-4"></div>
      </router-link>

      <div class="header__pane ml-auto">
        <div>
          <button
            type="button"
            class="hamburger close-sidebar-btn hamburger--elastic"
            data-class="closed-sidebar"
            :class="[is_active ? 'is-active' : null]"
            @click="collapseSideBar"
          >
            <span class="hamburger-box">
              <span class="hamburger-inner"></span>
            </span>
          </button>
        </div>
      </div>
    </div>
    <div class="app-header__mobile-menu">
      <div>
        <button
          type="button"
          class="hamburger hamburger--elastic mobile-toggle-nav"
        >
          <span class="hamburger-box">
            <span class="hamburger-inner"></span>
          </span>
        </button>
      </div>
    </div>
    <div class="app-header__menu">
      <span>
        <button
          type="button"
          class="btn-icon btn-icon-only btn btn-primary btn-sm mobile-toggle-header-nav"
        >
          <span class="btn-icon-wrapper">
            <i class="fa fa-ellipsis-v fa-w-6"></i>
          </span>
        </button>
      </span>
    </div>

    <div class="app-header__content">
      <div class="app-header-left">
        <div class="search-wrapper">
          <div class="input-holder">
            <input
              type="text"
              class="search-input"
              placeholder="Type to search"
            />
          </div>
          <button class="close"></button>
        </div>
      </div>
      <!-- notification -->
      <div class="app-header-right">
        <div class="header-btn-lg pr-0">
          <div class="widget-content p-0">
            <div class="widget-content-wrapper">
              <div class="widget-content-left ml-0 header-user-info mr-1">
                <i
                  v-if="is_on"
                  class="pe-7s-micro mr-1 mt-1 opacity-8"
                  @click="VoiceModuleOff()"
                ></i>
                <i
                  v-if="!is_on"
                  class="fas fa-microphone-slash mr-0 mt-1 opacity-8"
                  @click="VoiceModuleOn()"
                ></i>
              </div>
              <div class="widget-content-left ml-3 header-user-info mr-2">
                <NotificationBell />
              </div>

              <!-- Language Shortlist dropdown -->
              <div class="widget-content-left ml-0 header-user-info mr-4">
                <div class="btn-group">
                  <!-- <a
                    data-toggle="dropdown"
                    aria-haspopup="true"
                    aria-expanded="false"
                    class="p-0 btn"
                  >
                    <div class="widget-heading">
                      <span v-if="default_language && default_language.name">
                        {{ default_language.name }}</span
                      >
                      <span v-else>English</span>
                      <i class="fa fa-angle-down ml-2 opacity-8"></i>
                    </div>
                  </a> -->
                  <button
                    class="btn btn-light dropdown-toggle"
                    type="button"
                    id="dropdownMenuButton"
                    data-toggle="dropdown"
                    aria-haspopup="true"
                    aria-expanded="false"
                  >
                    <!-- <lang-flag :iso="lang_code_value" /> -->
                    <span v-if="lang_code_value && lang_name">
                      <!-- <country-flag :country="lang_code_value" size="small" /> -->
                      <lang-flag :iso="lang_code_value" />
                      <span class="ml-2"> {{ lang_name }}</span>
                    </span>
                    <span v-else>
                      <!-- <country-flag :country="lang_code_value" size="small" /> -->
                      <lang-flag iso="en" />
                      <span class="ml-2"> English</span>
                    </span>
                  </button>
                  <div
                    tabindex="-1"
                    role="menu"
                    aria-hidden="true"
                    class="dropdown-menu dropdown-menu-right"
                    v-if="all_languages"
                  >
                    <button
                      type="button"
                      tabindex="0"
                      class="dropdown-item"
                      @click="setDefaultLanguage('en')"
                    >
                      <lang-flag iso="en" />
                      <span class="ml-2"> English</span>
                    </button>
                    <template
                      v-for="language in all_languages"
                      :key="language.id"
                      :value="language.id"
                    >
                      <button
                        type="button"
                        tabindex="0"
                        class="dropdown-item"
                        @click="setLanguage(language.id)"
                      >
                        <lang-flag :iso="language.code" />
                        <!-- <country-flag :country="language.code" size="small" /> -->
                        <span class="ml-2"> {{ language.name }}</span>
                      </button>
                    </template>
                  </div>
                </div>
              </div>

              <!-- <div class="widget-content-left">
                <div class="widget-heading" v-if="first_name && last_name">
                  {{ first_name + " " + last_name }}
                </div>
                <div class="widget-heading" v-else>Your Name</div>
              </div> -->

              <div class="widget-content-left ml-3 header-user-info">
                <div class="btn-group">
                  <a
                    data-toggle="dropdown"
                    aria-haspopup="true"
                    aria-expanded="false"
                    class="p-0 btn"
                  >
                    <span
                      v-if="first_name && last_name"
                      :title="first_name + ' ' + last_name"
                    >
                      <img
                        v-if="image"
                        :src="image"
                        alt
                        class="rounded-circle"
                        height="40"
                        width="40"
                      />
                      <img
                        v-else
                        src="./profileImage.png"
                        alt
                        class="rounded-circle"
                        height="30"
                        width="30"
                      />
                      <i class="fa fa-angle-down ml-2 opacity-8"></i>
                    </span>
                  </a>
                  <div
                    tabindex="-1"
                    role="menu"
                    aria-hidden="true"
                    class="dropdown-menu dropdown-menu-right"
                  >
                    <router-link
                      class="dropdown-item"
                      :to="{ name: 'UserProfile' }"
                      >{{ $store.getters.GET_PROFILE }}</router-link
                    >

                    <div tabindex="-1" class="dropdown-divider"></div>

                    <router-link
                      class="dropdown-item"
                      :to="{ name: 'VoiceCustomization' }"
                      >Voice Customization</router-link
                    >

                    <div tabindex="-1" class="dropdown-divider"></div>

                    <button
                      type="button"
                      tabindex="0"
                      class="dropdown-item"
                      @click="logout"
                    >
                      {{ $store.getters.GET_LOGOUT }}
                    </button>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
// import flag from "vue-flag-icon";
import LangFlag from "vue-lang-code-flags";
import NotificationBell from "../../NotificationList/NotificationBell.vue";
import Swal from "sweetalert2";
// import CountryFlag from "vue-country-flag-next";
// import $ from "jquery";

export default {
  name: "Navbar",
  props: {},
  components: {
    LangFlag,
    NotificationBell,
    // CountryFlag,
  },
  data() {
    return {
      lang_name: null,
      lang_code_value: null,
      lang_details: null,
      filtered_by_code: null,
      default_language: null,
      all_languages: null,
      form_data: null,
      first_name: null,
      last_name: null,
      image: null,
      is_on: true,
      loading: false,
      group_error_data: null,
      // image:
      //   "https://cdn.icon-icons.com/icons2/1378/PNG/512/avatardefault_92824.png",
    };
  },
  computed: {
    is_active() {
      return this.$store.state.is_active;
    },
  },

  created() {
    this.initialLoad();
    // const token = localStorage.getItem("token");
    // if (token) {
    //   this.fetchAuthenticatedUser(token);
    // }
  },
  updated() {
    // this.LanguageShortList();
  },
  methods: {
    initialLoad: function () {
      this.LanguageShortList();
      this.fetchAuthenticatedUser();
      this.loadVoiceCustomization();
      // get cookie value
      if (
        document.cookie
          .split(";")
          .some((item) => item.trim().startsWith("language_code="))
      ) {
        // set cookie
        const language_code_value = document.cookie
          .split("; ")
          .find((row) => row.startsWith("language_code="))
          .split("=")[1];
        // console.log("474", language_code_value);
        // set expires
        let date = new Date();
        date.setTime(date.getTime() + 60 * 24 * 60 * 60 * 1000);
        const expires = "expires=" + date.toUTCString();
        // set cookie
        document.cookie =
          "language_code=" + language_code_value + "; " + expires;
        this.GetLanguageList(language_code_value);
        this.lang_code_value = language_code_value;
      }
      // if(! document.cookie.split(';').some((item) => item.trim().startsWith('language_code=')))
      // {
      //   localStorage.removeItem("token");
      // localStorage.clear();
      // this.$router.push("/");
      // }
      // else{
      // localStorage.removeItem("token");
      // localStorage.clear();
      // this.$router.push("/");
      // }
      // this.default_language = language_code_value;
    },
    setDefaultLanguage(lang_code) {
      window.location.reload();
      // set expires
      let date = new Date();
      date.setTime(date.getTime() + 60 * 24 * 60 * 60 * 1000);
      const expires = "expires=" + date.toUTCString();
      // set cookie
      document.cookie = "language_code=" + lang_code + "; " + expires;
    },
    setLanguage(language_ID) {
      window.location.reload();
      let selected_lang = this.all_languages
        .filter((x) => x.id === language_ID)
        .map((x) => x.code);
      // set expires
      let date = new Date();
      date.setTime(date.getTime() + 60 * 24 * 60 * 60 * 1000);
      const expires = "expires=" + date.toUTCString();
      // set cookie
      document.cookie = "language_code=" + selected_lang + "; " + expires;
      // get cookie value
      const language_code_value = document.cookie
        .split("; ")
        .find((row) => row.startsWith("language_code="))
        .split("=")[1];
      this.GetLanguageList(language_code_value);
      // let filtered_with_lancode = this.all_languages
      // .filter((x) => x.code === language_code_value);
    },
    // set language prev.done
    // setLanguage() {
    //   let selected_lang = this.all_languages
    //     .filter((x) => x.id === this.default_language)
    //     .map((x) => x.code);
    //   // localStorage.setItem("language_code", selected_lang);
    //   // set expires
    //   let date = new Date();
    //   date.setTime(date.getTime() + 60 * 24 * 60 * 60 * 1000);
    //   // date.setTime(date.getTime() + 60);
    //   const expires = "expires=" + date.toUTCString();
    //   // set cookie
    //   document.cookie = "language_code=" + selected_lang + "; " + expires;
    //   // get cookie value
    //   const language_code_value = document.cookie
    //     .split("; ")
    //     .find((row) => row.startsWith("language_code="))
    //     .split("=")[1];
    //   // console.log("483", language_code_value);
    //   this.GetLanguageList(language_code_value);
    //   // let filtered_with_lancode = this.all_languages
    //   // .filter((x) => x.code === language_code_value);
    // },

    LanguageShortList: function () {
      axios.get("language-short-list/").then((response) => {
        this.all_languages = response.data;
      });
    },
    GetLanguageList: function (language_code_value) {
      var queryParam = { code: language_code_value };
      axios
        .get("language/", { params: queryParam })
        .then((response) => {
          this.filtered_by_code = response.data;
          if (this.filtered_by_code && this.filtered_by_code[0].id) {
            this.default_language = this.filtered_by_code[0].id;
            this.GetLanguageDetails(this.filtered_by_code[0].id);
          }
          // console.log("500", this.filtered_by_code[0].id);
        })
        .catch(function (error) {
          console.log(error);
        });
    },

    async GetLanguageDetails(language_id) {
      await axios.get("language/" + language_id + "/").then(
        (response) => {
          //  if (response.data.status == false) {
          //    this.ResetLangdetailsToStore();
          //    console.log("hello 553")
          // }
          this.lang_name = response.data.name;
          if (response.data.details) {
            this.lang_details = response.data.details;
          }

          // console.log("----512", this.lang_details["LOGIN"]);
          this.SendLangdetailsToStore();
        },
        (response) => {
          console.log("----515", response);
        }
      );
    },
    async SendLangdetailsToStore() {
      await this.$store.dispatch("set_lang_details", {
        lang_details: this.lang_details,
      });
    },
    //  async ResetLangdetailsToStore() {
    //     console.log("hello 570")
    //   await this.$store.dispatch("reset_lang_details");
    // },

    //  language detail up
    collapseSideBar() {
      this.$store.commit("collapseSideBar");
    },
    fetchAuthenticatedUser() {
      axios.get("/profiles/me/", {}).then((response) => {
        this.form_data = response.data;
        this.first_name = response.data.user.first_name;
        this.last_name = response.data.user.last_name;
        this.image = response.data.image;
      });
    },

    async logout() {
      await axios
        .get("logout/", {})
        .then((res) => {
          console.log(res.data);
        })
        .catch((error) => {
          console.error(error);
        });
      localStorage.removeItem("token");

      localStorage.clear();

      this.$router.push("/");
    },
    // voice ON /Off
    VoiceModuleOff() {
      const currentUserID = localStorage.getItem("id");
      const response = axios
        .post("voice-config/", {
          // is_on: this.is_on,
          is_on: false,
          user: currentUserID,
        })
        .then((response) => {
          localStorage.setItem("is_on", response.data.is_on);
          Swal.fire({
            icon: "success",
            // title: "Yes...",
            text: "Voice turned off",
          }).then((result) => {
            this.loadVoiceCustomization();
            console.log(result);
          });
          console.log(response);
        })
        .catch((error) => {
          this.group_error_data = error.response.data;
        });
      console.log(response);
    },
    VoiceModuleOn() {
      const currentUserID = localStorage.getItem("id");
      const response = axios
        .post("voice-config/", {
          // is_on: this.is_on,
          is_on: true,
          user: currentUserID,
        })
        .then((response) => {
          localStorage.setItem("is_on", response.data.is_on);
          Swal.fire({
            icon: "success",
            // title: "Yes...",
            text: "Voice turned on",
          }).then((result) => {
            this.loadVoiceCustomization();
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

    // end of Logout
    // markAsSeen() {
    //   console.log("415====");
    // },
  },
  // end of method
};
// $(document).ready(function () {
//   $('[data-toggle="tooltip"]').tooltip();
// });
</script>
<style scoped>
#logoLink {
  text-decoration: none;
}
/* .app-theme-white .app-footer .app-footer__inner,
.app-theme-white .app-header {
  background: #cad2da;
} */
.app-header .app-header__content {
  background: #69c5a5;
}

.fa-angle-down:before {
  content: "\f107";
  color: white;
}

.widget-content .widget-content-left .widget-heading {
  opacity: 1;
  font-weight: 400;
  font-size: 15px;
  color: #ffffff;
  text-transform: uppercase;
}
.fa-ellipsis-v:before {
  content: "\f142";
  font-size: 20px;
  color: white;
}
.btn-primary:hover {
  color: #69c5a5;
  background-color: #69c5a5;
  border-color: #ffffff;
}
/* for Notification Menu */
/* new css for notifiation */

/* ==========================Responsive style==================== */
@media only screen and (max-width: 1320px) {
  .header-user-info {
    display: flex;
  }
}
.pe-7s-micro:before {
  content: "";
  font-size: 21px;
  color: white;
  font-weight: bold;
  cursor: pointer;
}
.fa-microphone-slash:before {
  content: "\f131";
  font-size: 20px;
  color: white;
  font-weight: bold;
  cursor: pointer;
}
</style>
