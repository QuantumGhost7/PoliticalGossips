<script>
  export let brand = "Brand";
  export let links = [];
  export let sticky = true;
  
  let isOpen = false;
  
  function toggleMenu() {
    isOpen = !isOpen;
  }
  
  function closeMenu() {
    isOpen = false;
  }
</script>

<nav class:sticky class="navbar">
  <div class="navbar-container">
    <div class="brand">
      <a href="/" class="brand-link">{brand}</a>
    </div>
    
    <button class="menu-toggle" on:click={toggleMenu} aria-label="Toggle navigation menu">
      <span class="hamburger" class:active={isOpen}></span>
    </button>
    
    <div class="links" class:open={isOpen}>
      {#each links as link}
        <a 
          href={link.href} 
          class="nav-link"
          class:active={link.active} 
          on:click={closeMenu}
        >
          {link.label}
        </a>
      {/each}
    </div>
  </div>
</nav>

<style>
  .navbar {
    background: rgba(255, 255, 255, 0.1);
    backdrop-filter: blur(10px);
    -webkit-backdrop-filter: blur(10px);
    border-bottom: 1px solid rgba(255, 255, 255, 0.2);
    box-shadow: 0 4px 15px rgba(0, 0, 0, 0.05);
    padding: 0.8rem 0;
    width: 100%;
    z-index: 1000;
  }
  
  .sticky {
    position: fixed;
    top: 0;
    left: 0;
  }
  
  .navbar-container {
    display: flex;
    align-items: center;
    justify-content: space-between;
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 1.5rem;
  }
  
  .brand {
    font-size: 1.5rem;
    font-weight: 600;
    flex-shrink: 0;
  }
  
  .brand-link {
    color: rgba(0, 0, 0, 0.8);
    text-decoration: none;
    transition: color 0.3s;
  }
  
  .brand-link:hover {
    color: rgba(0, 0, 0, 1);
  }
  
  .links {
    display: flex;
    gap: 1.5rem;
    align-items: center;
  }
  
  .nav-link {
    color: rgba(0, 0, 0, 0.7);
    text-decoration: none;
    font-weight: 500;
    position: relative;
    padding: 0.2rem 0;
    transition: color 0.3s;
  }
  
  .nav-link:hover,
  .nav-link.active {
    color: rgba(0, 0, 0, 1);
  }
  
  .nav-link::after {
    content: "";
    position: absolute;
    bottom: -2px;
    left: 0;
    width: 0;
    height: 2px;
    background-color: currentColor;
    transition: width 0.3s;
  }
  
  .nav-link:hover::after,
  .nav-link.active::after {
    width: 100%;
  }
  
  .menu-toggle {
    display: none;
    background: transparent;
    border: none;
    cursor: pointer;
    padding: 0.5rem;
  }
  
  .hamburger {
    position: relative;
    display: block;
    width: 24px;
    height: 2px;
    background: rgba(0, 0, 0, 0.8);
    transition: all 0.3s;
  }
  
  .hamburger::before,
  .hamburger::after {
    content: "";
    position: absolute;
    left: 0;
    width: 24px;
    height: 2px;
    background: rgba(0, 0, 0, 0.8);
    transition: all 0.3s;
  }
  
  .hamburger::before {
    top: -7px;
  }
  
  .hamburger::after {
    top: 7px;
  }
  
  .hamburger.active {
    background: transparent;
  }
  
  .hamburger.active::before {
    transform: rotate(45deg);
    top: 0;
  }
  
  .hamburger.active::after {
    transform: rotate(-45deg);
    top: 0;
  }
  
  @media (max-width: 768px) {
    .menu-toggle {
      display: block;
      z-index: 20;
    }
    
    .links {
      position: fixed;
      top: 0;
      right: 0;
      flex-direction: column;
      background: rgba(255, 255, 255, 0.95);
      backdrop-filter: blur(10px);
      -webkit-backdrop-filter: blur(10px);
      box-shadow: -5px 0 15px rgba(0, 0, 0, 0.05);
      height: 100vh;
      width: 250px;
      padding: 5rem 2rem 2rem;
      transform: translateX(100%);
      transition: transform 0.3s ease-in-out;
      z-index: 10;
    }
    
    .links.open {
      transform: translateX(0);
    }
  }
</style>