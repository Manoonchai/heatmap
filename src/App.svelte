<script lang="ts">
  import "twind/shim"
  import Head from "./lib/Head.svelte"
  import Kofi from "./lib/Kofi.svelte"
  import Menu from "./lib/Menu.svelte"
  import Social from "./lib/Social.svelte"
  import { onMount } from "svelte"
  import heatmap from "heatmap.js"
  import manoonchaiSvg from "./assets/manoonchai.svg"
  import manoonchaiKeymap from "./lib/manoonchai"
  import kedmaneeSvg from "./assets/kedmanee.svg"
  import kedmaneeKeymap from "./lib/kedmanee"

  const url = "https://manoonchai-heatmap.vercel.app"
  const title = "Manoonchai Heatmap"

  const menuItems = [{ name: "Github", url: "https://github.com/manoonchai/heatmap" }]

  const description = "See heatmap of Thai keyboard layouts"
  const imageUrl =
    "https://raw.githubusercontent.com/narze/timelapse/master/projects/heatmap_home.png"
  const gtagId = null
  let heatmapInstanceMnc, heatmapInstanceKed

  onMount(() => {
    const configMnc = {
      container: document.getElementById("heatmap-container-manoonchai"),
      radius: 60,
      maxOpacity: 0.6,
      minOpacity: 0,
      blur: 0.5,
      gradient: { 0.45: "rgb(0,0,255)", 0.55: "rgb(0,255,255)", 0.65: "rgb(0,255,0)", 0.95: "yellow", 1.0: "rgb(255,0,0)"},
    }
    heatmapInstanceMnc = heatmap.create(configMnc)

    const configKed = {
      container: document.getElementById("heatmap-container-kedmanee"),
      radius: 60,
      maxOpacity: 0.6,
      minOpacity: 0,
      blur: 0.5,
      gradient: { 0.45: "rgb(0,0,255)", 0.55: "rgb(0,255,255)", 0.65: "rgb(0,255,0)", 0.95: "yellow", 1.0: "rgb(255,0,0)"},
    }
    heatmapInstanceKed = heatmap.create(configKed)
  })

  let input = `หรือนี่จะล้มตำนาน ฟหกด่าสว เมื่อ ‘มนูญชัย’ แป้นพิมพ์ภาษาไทยยุคใหม่ที่สร้างจากฐานข้อมูลขนาดใหญ่ (Big data) ของการพิมพ์ภาษาไทยในปัจจุบัน และประมวลผลด้วยปัญญาประดิษฐ์ (AI) กับอัลกอริทึม เพื่อเฟ้นหาแป้นพิมพ์ที่มีประสิทธิภาพมากที่สุด จะช่วยให้เราบาลานซ์การใช้งานมือทั้งสองข้างให้เท่าๆ กัน และพิมพ์ง่ายขึ้นถึง 45% เลยทีเดียว!
รู้หรือไม่ว่าผังแป้นพิมพ์ไทยที่เราคุ้นชินและนิยมใช้มากที่สุดคือ ‘Kedmanee’ (เกษมณี) หรือรู้จักกันในตำนาน ‘ฟหกด่าสว’ ซึ่งผลการวิจัยพบว่าแป้นพิมพ์ไทยแบบเกษมณี ใช้งานหนักไปทางมือขวามากถึง 70% ทำให้เวลาเราพิมพ์งานนานๆ จะรู้สึกเมื่อยมือขวามากกว่า และพิมพ์ช้าลง เพราะตัวอักษรที่เราใช้บ่อยถูกจัดให้อยู่ฝั่งขวามากกว่านั่นเอง อีกทั้งเกษมณีถูกสร้างขึ้นมานานกว่า 50 ปี ทำให้การใช้งานตัวอักษรหรือเลขไทยบางตัวไม่ได้ถูกนำมาใช้อีกต่อไป
ผู้สร้างแป้นพิมพ์มนูญชัยจึงหยิบตัวอักษรมาจัดวางใหม่ เพื่อให้เหมาะกับการใช้งานภาษาไทยในปัจจุบัน เช่น การนำพยัญชนะที่ใช้งานน้อยนำไปอยู่แถวบนของแป้นพิมพ์ จัดกลุ่มตัวอักษรที่ใกล้เคียงกันให้อยู่ใกล้กัน หรือใช้เลขอารบิกเป็นค่าเริ่มต้นโดยไม่ต้องกดสลับเป็นภาษาอังกฤษ รวมถึงการวางตัวอักษรที่ใช้บ่อยให้กระจายตัวเพื่อลดการใช้นิ้วซ้ำซ้อนกัน ทำให้มนูญชัยมีสัดส่วนการพิมพ์ระหว่างมือซ้ายกับมือขวาอยู่ที่ 47% ต่อ 53%
สำหรับใครที่สนใจอยากลองใช้งานสามารถดาวน์โหลดได้ที่ https://manoonchai.com หรือเข้าไปที่ https://manoontype.web.app เพื่อทดลองพิมพ์โดยไม่ต้องติดตั้งลงบนตัวเครื่อง แถมยังสามารถฝึกพิมพ์คำตามโหมดต่างๆ ได้ตามต้องการเลย!
Source : https://manoonchai.com
อ่านในรูปแบบเว็บไซต์ได้ที่ : https://urbancreature.co/manoonchai
อ่านเรื่องราวที่เกี่ยวข้องได้ที่ : urbancreature.co/category/whats-up
#UrbanCreature #WhatsUp #ReinventTheWayWeLive #Manoonchai
`
  let heatmapMnc = []
  let heatmapKed = []
  let coordsMnc = []
  let coordsKed = []

  $: inputChars = input.split("")
  $: {
    inputChars
    coordsMnc = []
    coordsKed = []
    heatmapMnc = [
      [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
      [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
      [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
      [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
    ]
    heatmapKed = [
      [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
      [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
      [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
      [0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
    ]
  }

  $: inputChars.forEach((char, _index) => {
    let x, y

    manoonchaiKeymap.keys.forEach((row, rowIndex) => {
      row.forEach((keys, keyIndex) => {
        if (keys.includes(char)) {
          x = rowIndex
          y = keyIndex
        }
      })
    })

    if (x != undefined && y != undefined && heatmapInstanceMnc) {
      heatmapMnc[x][y] += 1
    }
  })

  $: inputChars.forEach((char, _index) => {
    let x, y

    kedmaneeKeymap.keys.forEach((row, rowIndex) => {
      row.forEach((keys, keyIndex) => {
        if (keys.includes(char)) {
          x = rowIndex
          y = keyIndex
        }
      })
    })

    if (x != undefined && y != undefined && heatmapInstanceKed) {
      heatmapKed[x][y] += 1
    }
  })

  $: {
    heatmapMnc.forEach((row, rowIndex) => {
      row.forEach((value, colIndex) => {
        if (value > 0) {
          coordsMnc.push({ ...indexToCoordinate(rowIndex, colIndex), value })
        }
      })
    })

    heatmapInstanceMnc?.setData({ max: max(heatmapMnc), min: 0, data: coordsMnc })
  }

  $: {
    heatmapKed.forEach((row, rowIndex) => {
      row.forEach((value, colIndex) => {
        if (value > 0) {
          coordsKed.push({ ...indexToCoordinate(rowIndex, colIndex), value })
        }
      })
    })

    heatmapInstanceKed?.setData({ max: max(heatmapKed), min: 0, data: coordsKed })
  }

  function indexToCoordinate(row: number, col: number) {
    let xStart = [48, 146, 162, 194]

    const co = {
      x: xStart[row] + (60 + 4.5) * col,
      y: 48 + (60 + 4.5) * row,
    }

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

  // function softmax(arr) {
  //   let sum = 0
  //   arr.forEach(function (row) {
  //     return row.forEach(function (value) {
  //       sum += Math.exp(value)
  //     })
  //   })

  //   return arr.map(function (row) {
  //     return row.map(function (value) {
  //       return Math.exp(value) / sum
  //     })
  //   })
  // }
</script>

<Kofi name="narze" label="Support Me" />
<Menu items={menuItems} />
<Social {url} {title} />
<Head {title} {description} {url} {imageUrl} {gtagId} />

<main class="w-full h-screen flex flex-col justify-center items-center">
  <center>Manoonchai</center>
  <div id="heatmap-container-manoonchai" style="width: 1000px; height: 400px">
    <img src={manoonchaiSvg} alt="keymap" class="max-w-full max-h-full" />
  </div>

  <center>Kedmanee</center>
  <div id="heatmap-container-kedmanee" style="width: 1000px; height: 400px">
    <img src={kedmaneeSvg} alt="keymap" class="max-w-full max-h-full" />
  </div>
  <textarea class="border" bind:value={input} cols="80" rows="10" />
</main>

<style>
  :root {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen, Ubuntu, Cantarell,
      "Open Sans", "Helvetica Neue", sans-serif;
  }
</style>
