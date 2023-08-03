<script setup></script>

<template>
  <div id="home">
    <div class="row">
      <div class="column image">
        <img src="@/assets/images/isotope-grid.png" alt="grid de imagens" />
      </div>
      <div class="column text">
        <div class="content">
          <h1>Lorem Ipsum</h1>
          <p>
            Lorem ipsum dolor sit amet, consectetur adipiscing elit. Ut et massa mi. Aliquam in
            hendrerit urna. Pellentesque sit amet sapien fringilla, mattis ligula consectetur,
            ultrices mauris. Maecenas vitae mattis tellus. Nullam quis imperdiet augue. Vestibulum
            auctor ornare leo, non suscipit magna interdum eu. Curabitur pellentesque nibh nibh, at
            maximus ante fermentum sit amet. Pellentesque commodo lacus at sodales sodales. Quisque
            sagittis orci ut diam condimentum, vel euismod erat placerat. In iaculis arcu eros, eget
            tempus orci facilisis id.
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

      .content {
        margin-bottom: 60px;

        h1 {
          color: $color-darken-orange;
          margin-bottom: 30px;
        }

        p {
          font-size: 18px;
          line-height: 22px;
          color: $color-blue;
        }
      }
    }
  }
}
</style>
