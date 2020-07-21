<template>
  <div id="app" :class="{ marginStepOne: step === 1 }">
    <transition name="slide">
      <DarkLogo v-if="step === 1" @backToZero="backHome" />
    </transition>
    <transition name="fade">
      <HeroImage v-if="step === 0" />
    </transition>
    <Claim v-if="step === 0" />
    <SearchInput 
      v-model="searchValue" 
			@input="handleInput"
      :dark="step === 1"  
    />
    <Error v-if="error && step === 1" />
    <div class="resultsContainer" v-if="step === 1 && !isLoading && results">
      <Item
        v-for="item in results" 
        :item="item"
        :key="item.imdbID"
        @click.native="handleModalOpen(item)" 
      />
    </div>
    <div class="loader" v-if="isLoading && step === 1" />
    <Modal 
      v-if="modalOpen"
      :item="modalItem"
      @closeModal="modalOpen = false" 
    />
    <transition name="fade">
      <button 
        :class="[{ buttonModalAboutTop: step === 1 }, { buttonModalAboutBottom: step === 0 }, 'buttonAbout']" 
        @click="aboutOpen = true">
          About
      </button>
    </transition>
    <ModalAbout v-if="aboutOpen" @closeAbout="aboutOpen = false" />
  </div>
</template>

<script>
import DarkLogo from './components/DarkLogo.vue';
import HeroImage from './components/HeroImage.vue';
import Claim from './components/Claim.vue';
import SearchInput from './components/SearchInput.vue';
import Item from './components/Item.vue';
import Modal from './components/Modal.vue';
import ModalAbout from './components/ModalAbout.vue';
import Error from './components/Error.vue';

import axios from 'axios';
import debounce from 'lodash.debounce';

const API = 'https://www.omdbapi.com/?apikey=becf1f46&s=';

export default {
  name: 'App',
  components: {
    HeroImage,
    Claim,
    SearchInput,
    DarkLogo,
    Item,
    Modal,
    ModalAbout,
    Error,
  },
  data() {
      return {
        searchValue: '',
        results: [],
        step: 0,
        isLoading: false,
        modalOpen: false,
        modalItem: null,
        aboutOpen: false,
        error: false,
    };
  },
  methods: {
    handleInput: debounce(function() {
      this.isLoading = true;
      this.step = 1;
			axios.get(`${API}${this.searchValue}`)
				.then((response) => {
          this.results = response.data.Search;
          this.isLoading = false;
          if (!this.results) {
            this.error = true;
          } else {
            this.error = false;
          }
				})
				.catch((error) => {
          console.log(error);
        });
    }, 500),
    handleModalOpen(item) {
      this.modalOpen = true;
      this.modalItem = item;
    },
    backHome() {
      this.step = 0;
      this.searchValue = '';
    },
  },
}
</script>

<style lang="scss">
  
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  #app {
    font-family: Montserrat, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    display: flex;
    flex-direction: column;
    align-items: center;

    &.marginStepOne {
      margin-top: 100px;
    }
  }

  .slide-enter-active, .slide-leave-active {
    transition: margin-top .5s ease;
  }

  .slide-enter, .slide-leave-to {
    margin-top: -50px;
  }

  .fade-enter-active, .fade-leave-active {
    transition: opacity .3s ease;
  }

  .fade-enter, .fade-leave-to {
    opacity: 0;
  }

  .buttonAbout {
    font-family: Montserrat, sans-serif;
    position: absolute;
    left: 0;
    padding: 10px 20px;
    margin: 5px;
    border: none;
    background: transparent;
    cursor: pointer;
    font-size: 20px;
    color: rgb(150, 150, 150);
    z-index: 1;

    @media (min-width: 768px) {
      font-size: 26px;
      margin: 15px;
    }
  }

  .buttonModalAboutBottom {
    bottom: 0;
    border: 2px solid rgb(150, 150, 150);
    background-color: rgba(0, 0, 0, 0.6);
    border-radius: 5px;
    transition: all .3s ease;
  }

  .buttonModalAboutBottom:hover {
    background-color: black;
    border: 2px solid #64d389;
    box-shadow: 0 0 20px 2px #50C878;
  }

  .buttonModalAboutBottom:focus {
    color: #50C878;
    border: 2px solid #64d389;
    outline: none;
  }

  .buttonModalAboutTop {
    top: 0;
    font-size: 20px;
    transition: all .3s ease;
    color: #64d389;
    
    @media (min-width: 768px) {
      font-size: 32px;
      margin: 15px;
    }
  }

  .buttonModalAboutTop:hover {
    text-decoration: underline;
  }

  .loader {
    margin-top: 100px;
    display: inline-block;
    width: 80px;
    height: 80px;

    @media (min-width: 768px) {
      width: 90px;
      height: 90px;
    }
  }

  .loader:after {
    content: " ";
    display: block;
    width: 64px;
    height: 64px;
    margin: 8px;
    border-radius: 50%;
    border: 6px solid #1e3d4a;
    border-color: #1e3d4a transparent #1e3d4a transparent;
    animation: loading 1.2s linear infinite;
  }

  @keyframes loading {
    0% {
      transform: rotate(0deg);
    }
    100% {
      transform: rotate(360deg);
    }
  }

  .resultsContainer {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 20px;
    margin: 50px 0;

    @media (min-width: 768px) {
			grid-template-columns: 1fr 1fr 1fr;
      grid-gap: 30px;
		}
  }

</style>
