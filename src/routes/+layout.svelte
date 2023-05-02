<script>
  import Navbar from "$lib/components/Navbar.svelte";
    import "../app.css";
  </script>
  
  <Navbar/>
  <slot />
  <footer class="footer footer-center p-4 bg-base-300 text-base-content">
    <div>
      <p>Copyright © 2023 - All rights reserved by JAM Industries Ltd</p>
    </div>
  </footer>