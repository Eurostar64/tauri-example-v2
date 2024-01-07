<script lang="ts">
  import Greet from './lib/Greet.svelte'
  import Tab1 from "./lib/Tab1.svelte";
	import Tab2 from "./lib/Tab2.svelte";
	import Tab3 from "./lib/Tab3.svelte";
  import Tabs from "./lib/Tabs.svelte";

  import { open } from '@tauri-apps/plugin-dialog';

  import { Command } from "@tauri-apps/plugin-shell";

  async function opendia(){
    // Open a dialog
    const file = await open({
      multiple: false,
      directory: true,
    });
    console.log(file);
  }

  async function startProcess(){
    // Start a process
    
    let cmd = Command.create("python", ["--version"]);
    // const child = await cmd.spawn();
    let output = await cmd.execute();
    console.log('stdout:', output.stdout);
    // const child = await cmd.spawn();
    // cmd.execute().then((result) => {
    //   console.log(result);
    // });
  }
// Prints file path and name to the console


// List of tab items with labels, values and assigned components
let items = [
    { label: "Content",
		 value: 1,
		 component: Tab1
		},
    { label: "Interactions",
		 value: 2,
		 component: Tab2
		},
    { label: "Tab 3",
		 value: 3,
		 component: Tab3
		}
  ];

</script>

<main class="container">
  <h1>Welcome to Tauri!</h1>

  <div class="row">
    <a href="https://vitejs.dev" target="_blank">
      <img src="/vite.svg" class="logo vite" alt="Vite Logo" />
    </a>
    <a href="https://tauri.app" target="_blank">
      <img src="/tauri.svg" class="logo tauri" alt="Tauri Logo" />
    </a>
    <a href="https://svelte.dev" target="_blank">
      <img src="/svelte.svg" class="logo svelte" alt="Svelte Logo" />
    </a>
  </div>

  <p on:click={() => opendia()}>
    Click on the Tauri, Vite, and Svelte logos to learn more.
  </p>

  <div class="row">
    <Greet />
  </div>

  <button on:click={() => startProcess()}>Start External Process</button>

  <Tabs {items} />


</main>

<style>
  .logo.vite:hover {
    filter: drop-shadow(0 0 2em #747bff);
  }

  .logo.svelte:hover {
    filter: drop-shadow(0 0 2em #ff3e00);
  }
</style>