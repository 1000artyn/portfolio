<script>
  import TypeTitle from '/src/TypeTitle.svelte';
  import { fade } from 'svelte/transition';
  import { onMount } from 'svelte';
  const pdfFile = '/martyn_vesey_cv.pdf';

  const sites = [
    {
      name: "Whip-It UK",
      url: "https://www.whip-it.co.uk/",
      image: "whipit.png",
      description: "Automotive services platform with API and Stripe integration, booking sysems, plus user login & dashboard."
    },
    {
      name: "Helitech",
      url: "https://www.helitech.co.uk/",
      image: "helitech.jpg",
      description: "Event site emphasizing accessibility and UX"
    },
    {
      name: "Disaster Expo Europe",
      url: "https://www.disasterexpoeurope.com/",
      image: "disastereurope.png",
      description: "Event site with database integration"
    },
    {
      name: "Advanced Air Expo",
      url: "https://www.advancedairexpo.co.uk/",
      image: "advancedair.png",
      description: "Event site to run as a companion to Helitech"
    },
    {
      name: "React Scrapbook",
      url: "https://react-portfolio-blue-six.vercel.app/",
      image: "React_Logo.png",
      description: "A collection of small projects using React"
    },
    {
      name: "Space Station Trading System",
      url: "https://space-station-ui.vercel.app/",
      image: "SSTS.webp",
      description: "Design for the front end of an API simulating a video game trading system"
    }
  ];

  let current = 0;

	const boxes = [
		{ id: 0, content: "This is content for Box 1", class:"about" },
		{ id: 1, content: "This is content for Box 2", class:"work" },
		{ id: 2, content: "This is content for Box 3", class:"contact" }
	];

  function setBox(newCurrent) {
    current = newCurrent;
  }
  let show = false;
  onMount(() => {
    show = true;
  });
</script>

<style>
:global(body) {
    margin: 0;
    font-family: "Roboto Mono", monospace;
}
main {
  text-align: center;
  padding-top: 100px;
  padding-left: 6%;
  padding-right: 6%;
  @media only screen and (max-width: 500px) {
    padding-top: 50px;
  }
}
a {
  text-decoration: none;
}
.portfolio-grid {
    display: flex;
    gap: 1rem;
    justify-content: center;
    flex-flow: wrap;
    margin-top: 40px;
}
.portfolio-item {
    border: 1px solid #ccc;
    padding: 1rem;
    text-align: center;
    width: 260px;
    box-sizing: border-box;
    transition: .3s;
    h2 {
      color: #000;
    }
    p {
      color: #000;
    }
}
.portfolio-item:hover {
    transform: translateY(-5px)
}
.portfolio-imagebox {
    height: 200px;
    width: 200px;
    margin: auto;
    position: relative;
    img {
        max-width: 100%;
        height: auto;
        position: relative;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
    }
}
.page-menu {
  display: flex;
  justify-content: center;
  gap: 38px;
  font-weight: 700;
  font-size: 18px;
  p {
    cursor: pointer;
  }
}
#slider {
  width: 200px;
  cursor: pointer;
  accent-color: #8273f2b8;
}
.title-box {
  height: 100px;
  position: relative;
}
.fancy-button {
  background: linear-gradient(135deg, #ff6ec4, #7873f5);
  color: white;
  border: none;
  padding: 0.75rem 1.5rem;
  font-size: 1rem;
  border-radius: 0.75rem;
  cursor: pointer;
  box-shadow: 0 0.5rem 1rem rgba(0,0,0,0.2);
  transition: transform 0.2s ease, box-shadow 0.2s ease;
  position: relative;
  overflow: hidden;
}

.fancy-button::before {
  content: '';
  position: absolute;
  top: 0;
  left: -110%;
  width: 100%;
  height: 100%;
  background: rgba(255,255,255,0.2);
  transform: skewX(-30deg);
  transition: left 0.5s;
}

.fancy-button:hover::before {
  left: 110%;
}

.fancy-button:hover {
  transform: translateY(-3px);
  box-shadow: 0 0.75rem 1.5rem rgba(0,0,0,0.3);
}

.button-container {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
  justify-content: center;
}
.fade-section {
  position: relative;
}
.about, .work, .contact {
  position: absolute;
  top: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 100%;
  padding-bottom: 50px;
}
.about {
  max-width: 800px;
  width: 100%;
  margin: 50px auto;
  p {
    margin-bottom: 50px;
  }
}
.contact {
  a {
    color: #8273f2b8;
  }
}
</style>
<main>
  <div class="title-box">
    <TypeTitle />
  </div>

  {#if show}
  <div in:fade={{ duration: 800, delay: 2400 }} class="initial-fade-in">
    <div class="page-menu">
      <p on:click={() => setBox(0)}>about</p>
      <p on:click={() => setBox(1)}>work</p>
      <p on:click={() => setBox(2)}>contact</p>
    </div>
    <input
      id="slider"
      type="range"
      min="0"
      max="2"
      bind:value={current}
    />

    <!-- Optionally show which one is selected -->

    <h3 class="section-title">{boxes[current].class}</h3>

    <!-- Show only the selected box -->
    <div class="fade-section">
    {#each boxes as box (box.id)}
      {#if box.id === 0 && current === 0}
        <div in:fade={{ duration: 500, delay: 500 }} out:fade={{ duration: 500 }} class="{box.class}">
          <p>Creative and user-focused Front-End Web Developer with over 7 years of experience in building responsive, scalable, and performance-optimized web applications.</p>
          <div class="button-container">
            <button class="fancy-button" on:click={() => window.open(pdfFile, '_blank')}>
              View CV
            </button>
            <a href={pdfFile} download="martyn_vesey_cv.pdf">
              <button class="fancy-button">Download CV</button>
            </a>
          </div>
        </div>
      {:else if box.id === 1 && current === 1}
        <div in:fade={{ duration: 500, delay: 500 }} out:fade={{ duration: 500 }} class="{box.class}">
          <p>Here are some of the websites and projects I've worked on:</p>
          <div class="portfolio-grid">
          {#each sites as site}
              <div class="portfolio-item">
              <a href={site.url} target="_blank" rel="noopener">
                  <div class="portfolio-imagebox">
                      <img src={`/images/${site.image}`} alt={site.name} />
                  </div>
                  <h2>{site.name}</h2>
                  <p>{site.description}</p>
              </a>
              </div>
          {/each}
          </div>
        </div>
      {:else if box.id === 2 && current === 2}
        <div in:fade={{ duration: 500, delay: 500 }} out:fade={{ duration: 500 }} class="{box.class}">
          <p>Email: <a href="mailto:mvesey@hotmail.co.uk">mvesey@hotmail.co.uk</a></p>
        </div>
      {/if}
    {/each}
    </div>
  </div>
  {/if}
</main>