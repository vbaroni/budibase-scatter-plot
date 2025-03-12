<script>
  import { IconName } from "./Mappings";

  export let name;
  export let size;
</script>

{#if name === IconName.HEXAGON}
  <svg
    width={size}
    height={size}
    viewBox="0 0 24 24"
    fill="none"
    xmlns="http://www.w3.org/2000/svg"
  >
    <path
      d="M23.7139 16.5315V7.06003L17.0151 0.371826H7.55426L0.855469 7.06003V16.5315L7.55426 23.2197H17.0151L23.7139 16.5315Z"
      fill="black"
      fill-opacity="0.85"
    />
  </svg>
{/if}

{#if name === IconName.DIAMOND}
  <svg
    width={size}
    height={size}
    viewBox="0 0 27 27"
    fill="none"
    xmlns="http://www.w3.org/2000/svg"
  >
    <path
      d="M26.9117 13.1788L13.8838 0.150879L0.855834 13.1788L13.8838 26.2068L26.9117 13.1788Z"
      fill="black"
      fill-opacity="0.85"
    />
  </svg>
{/if}

{#if name === IconName.TRIANGLE}
  <svg
    width={size}
    height={size}
    viewBox="0 0 27 23"
    fill="none"
    xmlns="http://www.w3.org/2000/svg"
  >
    <path
      d="M13.9144 0.38501L26.9733 23H0.855469L13.9144 0.38501Z"
      fill="black"
      fill-opacity="0.85"
    />
  </svg>
{/if}

{#if name === IconName.STAR}
  <svg
    width={size}
    height={size}
    viewBox="0 0 29 27"
    fill="none"
    xmlns="http://www.w3.org/2000/svg"
  >
    <path
      d="M14.6975 0L17.0468 9.31268L25.7987 5.34421L19.9782 12.9954L28.5396 17.3555L18.9306 17.5777L20.8566 26.9856L14.6975 19.6201L8.53844 26.9856L10.4539 17.5777L0.855469 17.3555L9.40621 12.9954L3.59636 5.34421L12.3482 9.31268L14.6975 0Z"
      fill="black"
      fill-opacity="0.85"
    />
  </svg>
{/if}
