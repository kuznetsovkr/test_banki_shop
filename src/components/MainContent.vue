<template>
  <main class="main">
    <div class="wrapper">
      <h1 class="main-title">Картины эпохи Возрождения</h1>
      <div class="cards">
        <div
            class="card"
            :class="{ 'card-sold': card.isSold }"
            v-for="card in filteredCards"
            :key="card.id"
        >
          <img
              :src="card.image"
              :alt="card.name"
              class="card-image"
              @click="openModal(card)"
          />
          <p class="card-name" @click="openModal(card)">{{ card.name }}<br>{{ card.author }}</p>
          <div class="container-price-button">
            <p v-if="card.isSold" class="card-sold-text">Продана на аукционе</p>
            <div v-else class="card-price">
              <span
                  :class="{'price-discount': card.discountPrice}"
                  class="price-current"
              >
                {{ card.discountPrice || card.price }} $
              </span>
              <span v-if="card.discountPrice" class="price-old">
                {{ card.price }} $
              </span>
            </div>
            <p v-if="filteredCards.length === 0">Ничего не найдено</p>
            <button
                :class="['buy-button', buyState[card.id]]"
                v-if="!card.isSold"
                @click="handleBuy(card.id)"
                :disabled="buyState[card.id] === 'in-cart'"
            >
              <span v-if="buyState[card.id] === 'loading'" class="icon-loader"></span>
              <span v-if="buyState[card.id] === 'in-cart'" class="icon-cart">В корзине</span>
              <span v-else>Купить</span>
            </button>
          </div>
        </div>
      </div>

      <modal v-if="selectedCard" @close="closeModal">
        <div class="modal-content">
          <h1 class="main-title">{{ selectedCard.name }}</h1>
          <div class="slider">
            <button class="prev-button" @click="prevSlide">‹</button>
            <img
                :src="selectedCard.sliderImages[currentSlide]"
                :alt="`Image ${currentSlide}`"
                class="slider-image"
            />
            <button class="next-button" @click="nextSlide">›</button>
          </div>
          <div class="slider-indicators">
      <span
          v-for="(img, index) in selectedCard.sliderImages"
          :key="index"
          class="indicator"
          :class="{ active: index === currentSlide }"
          @click="goToSlide(index)"
      ></span>
          </div>
          <p>{{ selectedCard.description }}</p>
          <div class="modal-price">
            {{ selectedCard.discountPrice || selectedCard.price }} $
          </div>
        </div>
      </modal>

    </div>
  </main>
</template>

<script>
import Modal from "./Modal.vue";
import Header from "./Header.vue";
import adam from "../assets/images/adam.svg";
import born from "../assets/images/born.svg";
import leo from "../assets/images/leo.svg";
import lesson from "../assets/images/lesson.svg";
import card11 from "../assets/images/car11.jpg"
import card12 from "../assets/images/car12.jpg"
import hands from "../assets/images/Hands_of_God_and_Adam.jpg"
import jesus from "../assets/images/Jesús_en_La_Última_Cena,_de_Leonardo_da_Vinci.jpg"
import leo_detail1 from "../assets/images/Leonardo_da_Vinci_004.jpg"
import leo_detail2 from "../assets/images/Leonardo_da_Vinci_006.jpg"
import leo_self from "../assets/images/Leonardo_self.jpg"
import miguel from "../assets/images/Miguel_Ángel,_por_Daniele_da_Volterra_(detalle).jpg"
import sb from "../assets/images/sb.png"

export default {
  name: "MainComponent",
  props: {
    searchQuery: {
      type: String,
      default: "",
    },
  },
  components: { Header, Modal },
  data() {
    return {
      cards: [
        {
          id: 1,
          name: "«Рождение Венеры»",
          author: "Сандро Боттичелли",
          price: "2 000 000",
          discountPrice: "1 000 000",
          image: born,
          description: "Картина «Рождение Венеры» Сандро Боттичелли, написанная около 1484–1486 годов, изображает" +
              " мифологическую сцену рождения Венеры, древнегреческой богини любви и красоты. Согласно мифу, " +
              "Венера появляется из морской пены, когда ее доставляет на землю раковина. На картине она стоит " +
              "на раковине, олицетворяя красоту и гармонию. Вокруг нее изображены мифологические персонажи: на одной " +
              "стороне ветры, которые несут Венеру на землю, а с другой – Нимфа, готовая укрыть богиню пеленой. " +
              "Картина известна своей утонченной грацией, мягкостью линий и гармонией композиции, а также ярким символизмом.",
          sliderImages: [card11, card12, sb],
          isSold: false,
        },
        {
          id: 2,
          name: "«Тайная вечеря»",
          author: "Леонардо да Винчи",
          price: "3 000 000",
          image: leo,
          description: "«Тайная вечеря» — фреска Леонардо да Винчи, написанная между 1495 и 1498 годами. Она изображает" +
              " момент, когда Иисус Христос сообщает своим ученикам, что один из них предаст его. Картина показывает " +
              "эмоциональные реакции апостолов, каждый из которых выражает разные чувства: удивление, гнев, сомнение " +
              "и скорбь. Центральной фигурой является Христос, который спокойно и уверенно принимает известие о " +
              "предательстве. Картина известна своей революционной техникой композиции, глубиной эмоций и вниманием " +
              "к человеческим выражениям, а также использованию перспективы для создания эффекта пространства.",
          sliderImages: [jesus, leo_detail1, leo_detail2,leo_self],
          isSold: false,
        },
        {
          id: 3,
          name: "«Сотворение Адама»",
          author: "Микеланджело",
          price: "6 000 000",
          discountPrice: "5 000 000",
          image: adam,
          description: "«Сотворение Адама» — фреска Микеланджело, созданная около 1512 года и расположенная на потолке " +
              "Сикстинской капеллы в Ватикане. На картине изображен момент библейского мифа, когда Бог дает жизнь " +
              "первому человеку, Адаму. Бог и Адам тянутся друг к другу, их руки почти касаются, что символизирует" +
              " передачу жизненной силы. Картина знаменита своей мощной символикой и мастерским изображением " +
              "человеческой фигуры, а также динамичным, почти напряженным взаимодействием между двумя персонажами. " +
              "Она является одним из самых известных произведений искусства эпохи Ренессанса.",
          sliderImages: [hands,miguel],
          isSold: false,
        },
        {
          id: 4,
          name: "«Урок анатомии»",
          author: "Рембрандт",
          price: "Продана на аукционе",
          image: lesson,
          description: "«Урок анатомии» Рембрандта, написанный в 1632 году, изображает сцену анатомического урока, " +
              "который проводит доктор Николас Тульп для группы студентов в Амстердаме. На картине показан момент, " +
              "когда Тульп демонстрирует своим ученикам вскрытие тела преступника, казненного за преступление. " +
              "Основное внимание уделено фигуре умершего, а также выражениям учеников, которые внимательно " +
              "наблюдают за процессом. Картина известна своей реалистичностью, детализированными изображениями " +
              "человеческого тела и психологической глубиной, передающей эмоции участников сцены. Это произведение " +
              "демонстрирует мастерство Рембрандта в передаче света, тени и человеческой драмы.",
          sliderImages: ["last-supper.jpg", "last-supper-detail.jpg"],
          isSold: true,
        }
      ],
      buyState: {},
      selectedCard: null,
      currentSlide: 0,
    };
  },
  computed: {
    filteredCards() {
      const query = this.searchQuery.toLowerCase();
      return this.cards.filter((card) =>
          card.name.toLowerCase().includes(query)
      );
    },
  },
  methods: {
    handleBuy(cardId) {
      if (this.buyState[cardId] === "in-cart") return;
      this.$set(this.buyState, cardId, "loading");
      setTimeout(() => {
        this.$set(this.buyState, cardId, "in-cart");
        localStorage.setItem(
            "buyState",
            JSON.stringify(this.buyState)
        );
      }, 2000);
    },
    handleSearchUpdate(query) {
      this.searchQuery = query;
      console.log("Search query:", this.searchQuery);
    },
    openModal(card) {
      this.selectedCard = card;
    },
    closeModal() {
      this.selectedCard = null;
    },
    loadState() {
      const savedState = JSON.parse(localStorage.getItem("buyState"));
      if (savedState) {
        this.buyState = savedState;
      }
    },
    prevSlide() {
      this.currentSlide =
          (this.currentSlide - 1 + this.selectedCard.sliderImages.length) %
          this.selectedCard.sliderImages.length;
    },
    nextSlide() {
      this.currentSlide =
          (this.currentSlide + 1) % this.selectedCard.sliderImages.length;
    },
    goToSlide(index) {
      this.currentSlide = index;
    },
  },
  watch: {
    "$root.searchQuery"(newQuery) {
      this.searchQuery = newQuery;
    },
  },
  created() {
    this.loadState();
  },
};
</script>
