<script lang="ts">
  import "twind/shim"
  import Head from "./lib/Head.svelte"
  import Kofi from "./lib/Kofi.svelte"
  import Menu from "./lib/Menu.svelte"
  import Social from "./lib/Social.svelte"
  import { onMount } from "svelte"
  import heatmap from "heatmap.js"
  import keymap from "./assets/manoonchai.svg"
  import keymapData from "./lib/manoonchai"

  const url = "https://single-page-svelte.vercel.app"
  const title = "Single Page Svelte"

  const menuItems = [{ name: "Github", url: "https://github.com/narze/single-page-svelte" }]

  const description = "Build a single page app with Svelte, quickly."
  const imageUrl =
    "https://raw.githubusercontent.com/narze/timelapse/master/projects/single-page-svelte_home.png"
  const gtagId = null
  let heatmapInstance

  onMount(() => {
    const config = {
      container: document.getElementById("heatmap-container"),
      radius: 80,
      maxOpacity: 0.8,
      minOpacity: 0,
      blur: 0.75,
      // gradient: {
      //   // enter n keys between 0 and 1 here
      //   // for gradient color customization
      //   ".5": "blue",
      //   ".8": "red",
      //   ".95": "white",
      // },
    }
    heatmapInstance = heatmap.create(config)
  })

  let input = "ไทยจงเจริญ"
  let heatmapData = []
  let coords = []

  $: inputChars = input.split("") // ["ไ", "ท", "ย", "ย", "ง", "เจ", "ร", "ิ", "ญ"]
  $: {
    inputChars
    coords = []
    heatmapData = [
      [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
      [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
      [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
      [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
    ]
  }

  $: inputChars.forEach((char, _index) => {
    let x, y

    keymapData.keys.forEach((row, rowIndex) => {
      row.forEach((keys, keyIndex) => {
        if (keys.includes(char)) {
          x = rowIndex
          y = keyIndex
        }
      })
    })

    if (x != undefined && y != undefined && heatmapInstance) {
      heatmapData[x][y] += 1
      // heatmapInstance.addData({ ...indexToCoordinate(x, y), value: 100 })
      // coords.push({ ...indexToCoordinate(x, y), value: 20 })
    }
  })

  $: {
    heatmapData.forEach((row, rowIndex) => {
      row.forEach((value, colIndex) => {
        if (value > 0) {
          coords.push({ ...indexToCoordinate(rowIndex, colIndex), value })
        }
      })
    })

    console.log({ heatmapData, coords, max: max(heatmapData) })

    heatmapInstance?.setData({ max: max(heatmapData) * 1.3, min: 0, data: coords })
  }

  function indexToCoordinate(row: number, col: number) {
    let xStart = [48, 146, 162, 194]

    const co = {
      x: xStart[row] + (60 + 4.5) * col,
      y: 48 + (60 + 4.5) * row,
    }

    console.log({ co })
    return co
  }

  function max(arr: number[][]) {
    let max = 0
    arr.forEach(function (row) {
      return row.forEach(function (value) {
        if (value > max) {
          max = value
        }
      })
    })
    return max
  }

  function softmax(arr) {
    let sum = 0
    arr.forEach(function (row) {
      return row.forEach(function (value) {
        sum += Math.exp(value)
      })
    })

    return arr.map(function (row) {
      return row.map(function (value) {
        return Math.exp(value) / sum
      })
    })
  }
</script>

<Kofi name="narze" label="Support Me" />
<Menu items={menuItems} />
<Social {url} {title} />
<Head {title} {description} {url} {imageUrl} {gtagId} />

<main class="w-full h-screen flex flex-col justify-center items-center">
  <div id="heatmap-container" style="width: 1000px; height: 400px">
    <img src={keymap} alt="keymap" class="max-w-full max-h-full" />
  </div>
  <textarea class="border" bind:value={input} cols="30" rows="10" />
</main>

<style>
  :root {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen, Ubuntu, Cantarell,
      "Open Sans", "Helvetica Neue", sans-serif;
  }
</style>
