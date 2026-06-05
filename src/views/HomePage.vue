<template>
  <ion-page>

    <ion-header class="custom-header">
      <div class="header-content">

        <div class="top-bar">
          <ion-icon :icon="menuOutline"></ion-icon>

          <h1>CRYPTO RANKING</h1>

          <ion-icon
            :icon="refreshOutline"
            @click="loadData"
          ></ion-icon>
        </div>

        <div
          v-if="filteredCoins.length"
          class="top-coin"
        >
          <div class="coin-avatar">
            🪙
          </div>

          <div class="top-rank">
            NO.{{ filteredCoins[0].rank }}
          </div>
        </div>

      </div>
    </ion-header>

    <ion-content>

      <ion-searchbar
        placeholder="Cari Coin..."
        v-model="searchQuery"
        @ionInput="handleSearch"
      />

      <!-- Coin Peringkat 1 -->
      <div
        v-if="filteredCoins.length"
        class="winner-card"
      >
        <div>
          <h2>{{ filteredCoins[0].name }}</h2>
          <p>{{ filteredCoins[0].symbol }}</p>
        </div>

        <div class="winner-price">
          ${{ filteredCoins[0].price_usd }}
        </div>

        <div class="trophy">
          🏆
        </div>
      </div>

      <!-- Ranking Coin -->
      <ion-card
        v-for="coin in filteredCoins.slice(1,20)"
        :key="coin.id"
        class="rank-card"
      >
        <ion-card-content>

          <div class="rank-row">

            <div class="rank-number">
              {{ coin.rank }}
            </div>

            <div class="rank-info">
              <h3>{{ coin.name }}</h3>
              <p>{{ coin.symbol }}</p>
            </div>

            <div class="rank-price">
              ${{ coin.price_usd }}
            </div>

          </div>

        </ion-card-content>
      </ion-card>

    </ion-content>

  </ion-page>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

import {
  IonPage,
  IonHeader,
  IonContent,
  IonCard,
  IonCardContent,
  IonSearchbar,
  IonIcon
} from '@ionic/vue';

import {
  menuOutline,
  refreshOutline
} from 'ionicons/icons';

import { getCoins } from '@/services/cryptoService';

export default defineComponent({
  name: 'HomePage',

  components: {
    IonPage,
    IonHeader,
    IonContent,
    IonCard,
    IonCardContent,
    IonSearchbar,
    IonIcon
  },

  setup() {
    return {
      menuOutline,
      refreshOutline
    };
  },

  data() {
    return {
      coins: [] as any[],
      filteredCoins: [] as any[],
      searchQuery: ''
    };
  },

  methods: {
    async loadData() {
      try {
        this.coins = await getCoins();
        this.filteredCoins = this.coins.slice(0, 20);
      } catch (error) {
        console.error(error);
      }
    },

    handleSearch() {
      const term = this.searchQuery.toLowerCase();

      if (!term) {
        this.filteredCoins = this.coins.slice(0, 20);
        return;
      }

      this.filteredCoins = this.coins.filter(
        coin =>
          coin.name.toLowerCase().includes(term) ||
          coin.symbol.toLowerCase().includes(term)
      );
    }
  },

  mounted() {
    this.loadData();
  }
});
</script>

<style scoped>

ion-content {
  --background: #f5f9ff;
}

/* HEADER */

.custom-header {
  background: linear-gradient(
    135deg,
    #4DA2FF 0%,
    #2E7FE8 100%
  );

  padding: 20px;
  border-radius: 0 0 30px 30px;
}

.top-bar {
  display: flex;
  justify-content: space-between;
  align-items: center;

  color: white;
}

.top-bar h1 {
  margin: 0;
  font-size: 22px;
  font-weight: 700;
}

.top-bar ion-icon {
  font-size: 28px;
  cursor: pointer;
}

.top-coin {
  margin-top: 20px;
  text-align: center;
}

.coin-avatar {
  width: 90px;
  height: 90px;

  background: white;

  border-radius: 50%;

  display: flex;
  justify-content: center;
  align-items: center;

  margin: auto;

  font-size: 40px;

  box-shadow: 0 4px 12px rgba(0,0,0,.2);
}

.top-rank {
  margin-top: 10px;
  color: white;
  font-weight: bold;
}

/* SEARCH */

ion-searchbar {
  padding: 10px;
}

/* TOP 1 */

.winner-card {
  background: #4DA2FF;
  color: white;

  margin: 15px;
  padding: 20px;

  border-radius: 20px;

  display: flex;
  justify-content: space-between;
  align-items: center;

  box-shadow: 0 6px 16px rgba(0,0,0,.15);
}

.winner-card h2 {
  margin: 0;
  font-size: 20px;
}

.winner-card p {
  margin: 0;
  opacity: 0.9;
}

.winner-price {
  font-size: 22px;
  font-weight: bold;
}

.trophy {
  font-size: 35px;
}

/* LIST */

.rank-card {
  margin: 12px;
  border-radius: 18px;

  box-shadow: 0 3px 12px rgba(0,0,0,.08);
}

.rank-row {
  display: flex;
  align-items: center;
}

.rank-number {
  width: 50px;

  font-size: 24px;
  font-weight: bold;

  color: #4DA2FF;
}

.rank-info {
  flex: 1;
}

.rank-info h3 {
  margin: 0;
  font-size: 16px;
}

.rank-info p {
  margin: 0;
  color: #888;
}

.rank-price {
  font-weight: bold;
  color: #4DA2FF;
  font-size: 15px;
}

</style>