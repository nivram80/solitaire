<section class="foundations">
  <div class="foundation diamond-foundation">A</div>
  <div class="foundation heart-foundation">A</div>
  <div class="foundation club-foundation">A</div>
  <div class="foundation spade-foundation">A</div>
</section>

<style>
  .foundations {
    grid-area: foundation;
    display: grid;
    flex-direction: column;
    justify-content: center;
    align-items: flex-start;
    padding: 8px 0;
  }

  .foundation {
    margin-bottom: 12px;
    box-sizing: border-box;
    width: 80px;
    height: 120px;
    border-radius: 4px;
    border: 4px solid rgba(0, 0, 0, 0.1);
    padding: 4px 6px;
    font-size: 80px;
    color: rgba(0, 0, 0, 0.1);
    text-align: center;
  }
</style>