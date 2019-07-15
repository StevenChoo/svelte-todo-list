<script>
  export let checked = false;
</script>

<style lang="scss">
  $toggle-size: 16px;
  $toggle-indent: 2px;
  $toggle-border-width: 2px;
  $toggle-color: #2196f3;
  $toggle-disabled-color: #868e96;
  $toggle-background-color: #FFFFFF;
  $toggle-arrow-width: 2px;
  $toggle-arrow-color: #ffffff;

  .checkbox-wrapper {
    display: inline-block;
    position: relative;

    input {
      position: absolute;
      left: -99999px;

      &:disabled + .label:before {
        border-color: $toggle-disabled-color;
      }

      &:focus + .label:before,
      &:not(:disabled):checked:focus + .label:after {
        box-shadow: 0 0 0 2px $toggle-background-color,
          0 0 0px 4px $toggle-color;
      }

      &:not(:disabled) + .label:before,
      &:not(:disabled) + .label:after {
        opacity: 1;
        transform-origin: center center;
        will-change: transform;
        transition: transform 0.2s ease-out;
      }

      &:not(:disabled) + .label:before {
        transform: rotateY(0deg);
        transition-delay: 0.2s;
      }

      &:not(:disabled) + .label:after {
        opacity: 1;
        background-color: $toggle-color;
        transform: rotateY(90deg);
      }

      &:not(:disabled):checked + .label:before {
        transform: rotateY(-90deg);
        transition-delay: 0s;
      }

      &:not(:disabled):checked + .label:after {
        opacity: 1;
        transform: rotateY(0deg);
        transition-delay: 0.2s;
      }

      &:not(:disabled):checked + .label {
        &:after {
          opacity: 1;
        }

        .text:before {
          width: 0.5em;
          height: 0.25em;
          border-left-width: $toggle-arrow-width;
          border-bottom-width: $toggle-arrow-width;
          will-change: width, height;
          transition: width 0.1s ease-out 0.2s, height 0.2s ease-out;

          opacity: 1;
          transition: opacity 0.1s ease-out 0.3s, width 0.1s ease-out 0.5s,
            height 0.2s ease-out 0.3s;
        }
      }
    }

    .label {
      display: inline-flex;
      cursor: pointer;
      min-height: $toggle-size;
      min-width: $toggle-size;

      &:before,
      &:after {
        content: "";
        box-sizing: border-box;
        width: 1em;
        height: 1em;
        font-size: $toggle-size;
        position: absolute;
        left: 0;
        top: 0;
      }

      &:before {
        border: $toggle-border-width solid $toggle-color;
        z-index: 2;
      }

      .text {
        margin-top: auto;
        margin-bottom: auto;

        &:before {
          content: "";
          box-sizing: border-box;
          width: 0;
          height: 0;
          font-size: $toggle-size;

          border-left-width: 0;
          border-bottom-width: 0;
          border-left-style: solid;
          border-bottom-style: solid;
          border-color: $toggle-arrow-color;

          position: absolute;
          top: 0.5428em;
          left: 0.2em;
          z-index: 3;

          opacity: 0;

          transform-origin: left top;
          transform: rotate(-40deg) skew(10deg);
        }
      }
    }
  }
</style>

<label class="checkbox-wrapper">
  <input type="checkbox" bind:checked={checked}/>
  <span class="label">
    <span class="text" />
  </span>
</label>
