<template>
  <form
    name="degustation"
    action="/merci.html"
    method="post"
    netlify
    data-netlify-honeypot="bot-field"
    class="w-full max-w-md center"
  >
    <input type="hidden" name="form-name" value="degustation" />
    <div class="flex flex-wrap -mx-3 mb-5 mt-4">
      <div class="w-full md:w-1/2 px-3 mb-5 md:mb-0">
        <label
          for="user-email"
          class="block uppercase tracking-wide text-grey-darker text-xs font-bold mb-2"
          >Quelle est votre adresse mail ?</label
        >
      </div>
      <div class="md:w-2/3 px-3 mb-5 md:mb-0">
        <input
          id="user-email"
          v-model="userEmail"
          name="user-email"
          class="appearance-none block w-full bg-grey-lighter text-grey-darker border border-grey-lighter rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white focus:border-purple"
          type="email"
          placeholder="nom.prenom@gmail.com"
          autofocus="true"
        />
      </div>
    </div>

    <div class="flex flex-wrap -mx-3 mb-5">
      <div class="w-full md:w-1/2 px-3 mb-5 md:mb-0">
        <label
          for="whisky-distillery"
          class="block uppercase tracking-wide text-grey-darker text-xs font-bold mb-2"
          >De quelle distillerie est l'alcool ?</label
        >
        <input
          id="whisky-distillery"
          v-model="whiskyDistillery"
          name="whisky-distillery"
          class="appearance-none block w-full bg-grey-lighter text-grey-darker border rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white focus:border-purple"
          type="text"
          placeholder="Birmingham"
        />
      </div>

      <div class="w-full md:w-1/2 px-3">
        <label
          for="whisky-name"
          class="block uppercase tracking-wide text-grey-darker text-xs font-bold mb-2"
          >Quel est le nom du breuvage ?</label
        >
        <input
          id="whisky-name"
          v-model="whiskyName"
          name="whisky-name"
          class="appearance-none block w-full bg-grey-lighter text-grey-darker border rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white focus:border-purple"
          type="text"
          placeholder="Hakushu"
        />
      </div>
    </div>

    <div class="flex flex-wrap -mx-3 mb-2">
      <div class="w-full md:w-1/2 px-3 mb-5 md:mb-0">
        <label
          class="block uppercase tracking-wide text-grey-darker text-xs font-bold mb-2"
          for="whisky-type"
          >Type du whisky</label
        >
        <div class="relative">
          <select
            id="whisky-type"
            v-model="whiskyType"
            name="whisky-type"
            class="block appearance-none w-full bg-grey-lighter border border-grey-lighter text-grey-darker py-3 px-4 pr-8 rounded leading-tight focus:outline-none focus:bg-white focus:border-purple"
          >
            <option
              v-for="whiskyTypeOption in whiskyTypeOptions"
              :key="whiskyTypeOption.id"
              :value="whiskyTypeOption"
              >{{ whiskyTypeOption }}</option
            >
          </select>
          <div
            class="pointer-events-none absolute pin-y pin-r flex items-center px-2 text-grey-darker"
          >
            <svg
              class="fill-current h-4 w-4"
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 20 20"
            >
              <path
                d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z"
              ></path>
            </svg>
          </div>
        </div>
      </div>

      <div class="w-full md:w-1/2 px-3 mb-5 md:mb-0">
        <label
          class="block uppercase tracking-wide text-grey-darker text-xs font-bold mb-2"
          for="whisky-origin"
          >Origine du whisky</label
        >
        <div class="relative">
          <select
            id="whisky-origin"
            v-model="whiskyOrigin"
            name="whisky-origin"
            class="block appearance-none w-full bg-grey-lighter border border-grey-lighter text-grey-darker py-3 px-4 pr-8 rounded leading-tight focus:outline-none focus:bg-white focus:border-purple"
          >
            <option
              v-for="whiskyOriginOption in whiskyOriginOptions"
              :key="whiskyOriginOption.id"
              :value="whiskyOriginOption"
              >{{ whiskyOriginOption }}</option
            >
          </select>
          <div
            class="pointer-events-none absolute pin-y pin-r flex items-center px-2 text-grey-darker"
          >
            <svg
              class="fill-current h-4 w-4"
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 20 20"
            >
              <path
                d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z"
              ></path>
            </svg>
          </div>
        </div>
      </div>
    </div>

    <!-- <div class="md:flex md:items-center mb-6">
      <div class="md:w-1/3">
        <label
          class="block text-grey font-bold md:text-right mb-1 md:mb-0 pr-4"
          for="parfums-choisis"
        >Parfums choisis</label>
      </div>
      <div class="md:w-2/3">
        <input
          v-model="chosenFlavorsToSubmit"
          name="parfums-choisis"
          class="bg-grey-lighter appearance-none border-2 border-grey-lighter rounded w-full py-2 px-4 text-grey-darker leading-tight focus:outline-none focus:bg-white focus:border-purple"
          id="parfums-choisis"
          type="text"
          value="Jane Doe"
        >
      </div>
    </div>-->

    <label for="selected-flavors" hidden>Saveurs choisies</label>
    <textarea
      id="selected-flavors"
      v-model="selectedFlavors"
      name="selected-flavors"
      hidden
    ></textarea>

    <button
      type="submit"
      class="bg-purple mt-3 hover:bg-purple-dark text-white font-bold py-2 px-4 rounded-full"
    >
      Finir ma dégustation
    </button>
  </form>
</template>

<script>
import whiskyOrigin from '@/assets/data/whiskyOrigin.json'
import whiskyType from '@/assets/data/whiskyType.json'

export default {
  props: {
    selectedFlavors: {
      type: Array,
      default() {
        return []
      }
    }
  },
  data() {
    return {
      userEmail: '',
      whiskyDistillery: '',
      whiskyName: '',
      whiskyType: '',
      whiskyTypeOptions: whiskyType,
      whiskyOrigin: '',
      whiskyOriginOptions: whiskyOrigin
    }
  }
}
</script>

<style lang="sass" scoped>
.center
  width: 80%
  margin: 0 auto
</style>
