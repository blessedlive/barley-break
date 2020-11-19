<template>
  <div class="container">
      <div class="column">
        <Game/>
      </div>
      <div class="column">
        <Game/>
      </div>
  </div>
</template>

<style lang="scss">
    .container {
        display: flex;
        width: 100%;
        justify-content: space-between;

        @media screen and (max-width: 768px) {
            flex-direction: column;
            justify-content: center;
        }

        .column {
            width: 50%;        
            
            @media screen and (max-width: 768px) {
                width: 100%;
                margin: 20px 0;
            }
        }
    }
</style>

<script>
import Game from '@/components/Game';

export default {
    components: { Game }
}
</script>