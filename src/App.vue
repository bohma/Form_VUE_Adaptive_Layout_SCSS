<template>
  <div id="app">
    <div class="main">
      <div class="container">
        <div class="main__container">
          <div class="main__content">
            <h1 class="main__title"></h1>
            <div class="main__text">
              <div class="main__info">
                <p class="main__info_big">&nbsp;</p>
                <p></p>
              </div>
              <div class="main__data">
                <p class="main__data-head"></p>
                <p class="main__data-body"></p>
              </div>
            </div>
            <div class="main__form">
              <botoInput />
            </div>
          </div>
          <div class="main__figure">
            <div class="main__images">
              <div class="main__img">
                <img src="./assets/img/Iphone.png" alt />
              </div>
              <div class="main__img main__img2">
                <img src="./assets/img/iPad Pro.png" alt />
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import botoInput from "./components/boto-input";
export default {
  name: "App",
  components: {
    botoInput,
  },
};
</script>
<style lang="scss">
@import url("assets/fonts/Gilroy/stylesheet.css");
@import url("assets/fonts/GothamPro/stylesheet.css");

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  line-height: 1;
}
.container {
  max-width: 1440px;
  padding: 0 15px;
  margin: 0 auto;
}
img {
}

.main {
  overflow: hidden;
  background: #ffffff;

  &__container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    height: 100vh;
    position: relative;
    &::after {
      content: "";
      position: absolute;
      top: 0;
      right: 400px;
      width: 100vw;
      height: 100%;
      background: #fdde00;
    }
  }
  &__content {
    position: relative;
    z-index: 1;
    flex: 0 0 910px;
  }
  &__title {
    font-family: "GothamPro", sans-serif;
    font-weight: 900;
    font-size: 64px;
    margin-bottom: 36px;
    &_ttu {
      text-transform: uppercase;
    }
  }
  &__text {
    display: flex;
    align-items: center;
    margin-bottom: 54px;
  }
  &__info {
    font-family: "GothamPro", sans-serif;
    font-weight: 900;
    font-size: 36px;
    border-right: 6px solid #000;
    padding-right: 15px;
    margin-right: 15px;
    &_big {
      font-size: 75px;
    }
  }
  &__data {
    width: 530px;
    max-width: 100%;
    &-head {
      font-family: "GothamPro", sans-serif;
      font-weight: 900;
      font-size: 34px;
      margin-bottom: 15px;
    }
    &-body {
      font-family: "GothamPro", sans-serif;
      font-weight: 500;
      font-size: 20px;
    }
  }
  &__figure {
    flex: 0 1 100%;
    height: 700px;
    max-height: 100%;
    position: relative;
  }
  &__images {
    height: 100%;
    display: flex;
    position: absolute;
    top: 50%;
    left: 0;
    transform: translateY(-50%);
    z-index: 1;
  }

  &__img {
    height: 100%;

    img {
      height: 100%;
    }
  }
}

@media screen and (max-width: 1440px) {
  .container {
    max-width: 1024px;
  }

  .main {
    &__container {
      &::after {
        right: 260px;
      }
    }
    &__title {
      font-size: 40px;
    }
    &__content {
      flex: 0 0 600px;
    }
    &__info {
      font-size: 28px;
      &_big {
        font-size: 60px;
      }
    }
    &__data {
      width: 400px;
      &-head {
        font-size: 24px;
      }
      &-body {
        font-size: 18px;
      }
    }
    &__figure {
      height: 500px;
    }
  }
}
@media screen and (max-width: 1023px) {
  .container {
    max-width: 768px;
  }

  .main {
    &__container {
      flex-direction: column;
      justify-content: center;
      height: auto;
      padding: 30px 0;
      &::after {
        right: auto;
        left: 50%;
        transform: translateX(-50%);
      }
    }
    &__content {
      flex: none;
    }
    &__figure {
      flex: none;
      height: auto;
      position: relative;
      z-index: 1;
    }
    &__images {
      position: static;
      transform: none;
    }

    &__img {
      img {
        height: auto;
        max-width: 100%;
      }
    }
  }
}
@media screen and (max-width: 767px) {
  .container {
    max-width: 375px;
  }

  .main {
    &__container {
      text-align: center;
      display: block;
    }
    &__title {
      font-size: 20px;
      margin-bottom: 20px;
    }
    &__text {
      display: block;
      margin-bottom: 20px;
    }
    &__info {
      padding: 0;
      margin: 0;
      padding-bottom: 15px;
      margin-bottom: 15px;
      border-right: none;
      border-bottom: 6px solid #000;
      font-size: 24px;
      &_big {
        font-size: 24px;
      }
      p {
        display: inline;
      }
    }
    &__data {
      &-head {
        font-size: 18px;
      }
      &-body {
        font-size: 16px;
      }
    }
    &__images {
      display: block;
    }
  }
}
</style>
