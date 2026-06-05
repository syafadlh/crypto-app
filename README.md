# 🚀 Crypto App

A mobile cryptocurrency ranking application built using **Ionic Vue**. This application retrieves real-time cryptocurrency data from the CoinLore API and displays cryptocurrency rankings in a modern mobile-friendly interface.

## 📱 Features

* Display cryptocurrency rankings
* Search cryptocurrency by name or symbol
* Refresh data from API
* Show cryptocurrency information:

  * Rank
  * Name
  * Symbol
  * Price (USD)
* Modern mobile UI with SUI Blue theme

## 🛠️ Technologies Used

* Ionic Framework
* Vue 3
* TypeScript
* Axios
* CoinLore API

## 🌐 API Source

CoinLore API:

https://api.coinlore.net/api/tickers/

## 📸 Application Preview

<img src="images/demo-crypto.gif" alt="Demo Crypto" width="400"/>

## 📦 Installation

Clone the repository:

```bash
git clone https://github.com/syafadlh/crypto-app.git
```

Enter the project directory:

```bash
cd crypto-app
```

Install dependencies:

```bash
npm install
```

## ▶️ Run Application

```bash
ionic serve
```

The application will be available at:

```text
http://localhost:8100
```

## 📂 Project Structure

```text
src/
├── services/
│   └── cryptoService.ts
│
├── views/
│   └── HomePage.vue
│
└── App.vue
```