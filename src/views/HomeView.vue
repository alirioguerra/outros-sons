<script setup></script>

<template>
  <div id="home">
    <div class="row">
      <div class="column image">
        <img src="@/assets/images/isotope-grid.png" alt="grid de imagens" />
      </div>
      <div class="column text">
        <div class="content">
          <h1>Outros Sons</h1>
          <p>
            Este é o projeto “Outros sons”, um webdocumentário que aborda a acessibilidade surda em
            quatro temas: Saúde, Esporte, Cultura e Educação. Cada um dos assuntos é explorado em um
            episódio próprio. Nesse site você pode navegar entre os conteúdos com interatividade, ao
            explorar a página. O objetivo é que você conheça as principais demandas da comunidade
            surda e não ouvinte e passe a ter conhecimento das reivindicações de demandas públicas e
            sociais provocadas pela falta de acessibilidade.
          </p>
        </div>
        <img src="@/assets/icons/arrow-down.svg" alt="seta para baixo" />
      </div>
    </div>
  </div>
</template>

<style lang="scss">
#home {
  display: flex;
  align-items: center;
  justify-content: center;

  .row {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: rem-calc(80);

    @media only screen and (max-width: 768px) {
      flex-direction: column;
      gap: rem-calc(20);
    }

    .image {
      flex: 1;

      img {
        mix-blend-mode: darken;
      }
    }

    .text {
      flex: 1;
      display: flex;
      align-items: center;
      justify-content: center;
      flex-direction: column;
      max-width: rem-calc(580);

      img {
        display: block;

        @media only screen and (max-width: 768px) {
          display: none;
        }
      }

      .content {
        margin-bottom: 60px;

        h1 {
          color: $color-darken-orange;
          margin-bottom: 30px;

          @media only screen and (max-width: 768px) {
            font-size: 36px;
            line-height: 44px;
            margin-bottom: 15px;
          }
        }

        p {
          font-size: 18px;
          line-height: 22px;
          color: $color-blue;

          @media only screen and (max-width: 768px) {
            font-size: 16px;
            line-height: 20px;
          }
        }
      }
    }
  }
}
</style>
