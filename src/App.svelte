<script lang="ts">
  import "twind/shim"
  import Head from "./lib/Head.svelte"
  import Kofi from "./lib/Kofi.svelte"
  import Menu from "./lib/Menu.svelte"
  import { onMount } from "svelte"
  import heatmap, { Heatmap } from "heatmap.js"
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

  let manoonchaiImageElement: HTMLElement
  let kedmaneeImageElement: HTMLElement
  let heatmapCanvasManoonchai: HTMLElement
  let heatmapCanvasKedmanee: HTMLElement

  // const keymaps = [
  //   {
  //     name: "Manoonchai",
  //     keymap: manoonchaiKeymap,
  //     heatmap: heatmapInstanceMnc,
  //     container: heatmapCanvasManoonchai,
  //     image: manoonchaiImageElement,
  //   },
  //   {
  //     name: "Kedmanee",
  //     keymap: kedmaneeKeymap,
  //     heatmap: heatmapInstanceKed,
  //     container: heatmapCanvasKedmanee,
  //     image: kedmaneeImageElement,
  //   },
  // ]

  onMount(() => {
    const configMnc = {
      container: heatmapCanvasManoonchai,
      radius: 35,
      maxOpacity: 0.6,
      minOpacity: 0,
      blur: 0.5,
      gradient: {
        0.45: "rgb(0,0,255)",
        0.55: "rgb(0,255,255)",
        0.65: "rgb(0,255,0)",
        0.95: "yellow",
        1.0: "rgb(255,0,0)",
      },
    }
    heatmapInstanceMnc = heatmap.create(configMnc)

    const configKed = {
      container: heatmapCanvasKedmanee,
      radius: 35,
      maxOpacity: 0.6,
      minOpacity: 0,
      blur: 0.5,
      gradient: {
        0.45: "rgb(0,0,255)",
        0.55: "rgb(0,255,255)",
        0.65: "rgb(0,255,0)",
        0.95: "yellow",
        1.0: "rgb(255,0,0)",
      },
    }
    heatmapInstanceKed = heatmap.create(configKed)

    redraw()
  })

  let selectedPreset
  let textPresets = [
    {
      title: "กุ้งอบวุ้นเส้น",
      text: `Credit : https://www.pangpond.com/กุ้งอบวุ้นเส้น

วิธีการทํากุ้งอบวุ้นเส้น เหมือนกินที่ร้าน ทำง่ายทานได้ในไม่กี่ขั้นตอน

เมนูกุ้งอบวุ้นเส้นคงเป็นเมนูที่แค่ฟังชื่อก็เหมือนได้กลิ่นหอม ๆ ของกุ้งอบวุ้นเส้นลอยมา เนื้อกุ้งร่วนเด้งกินร่วมกับวุ่นเส้นนุ่ม อร่อยเกินคำบรรยาย ด้วยความพิเศษของเมนูกุ้งอบวุ้นเส้นที่มีเอกลักษณ์ในตัวเองทำให้เป็นเมนูอาหารขึ้นชื่อและติดใจติดปากใครหลายคน ทั้งนี้ วิธีการทำกุ้งอบวุ้นเส้นก็ไม่ได้ยากอย่างที่คิด และวันนี้เราได้นำสูตรกุ้งอบวุ้นเส้นมาฝากกัน บอกเลยว่าเป็นวิธีการทำกุ้งอบวุ้นเส้นที่ง่ายและเหมือนกับกินที่ร้านอาหารเลยทีเดียว กุ้งอบวุ้นเส้นสูตรและขั้นตอนจะเป็นอย่างไรบ้างนั้น เราไปดูกันเลย

ส่วนผสมกุ้งอบวุ้นเส้น / เครื่องปรุงกุ้งอบวุ้นเส้น

กุ้งก้ามกรามขนาดกลาง ประมาณ 4-5 ตัว
วุ้นเส้น 1 ห่อ (ขนาดประมาณ 80 กรัม)
น้ำตาลทรายขาว 2 ช้อนโต๊ะ
ซีอิ๊วดำ 1 ช้อนโต๊ะ
ซีอิ๊วขาว 1 ½ ช้อนโต๊ะ
ซอสหอยนางรม 1½ ช้อนโต๊ะ
น้ำซุปต้มสุก 1 ถ้วย
ส่วนผสมอื่น ๆ เพิ่มเติม ได้แก่ ขิงแก่, กระเทียม, พริกไทยขาว, พริกไทยดำ, คื่นช่าย, ต้นหอม
วิธีการทํากุ้งอบวุ้นเส้น
เตรียมส่วนผสมทุกอย่างให้เรียบร้อย และล้างให้สะอาด
ทำน้ำปรุงรส โดยใส่ส่วนผสม ดังนี้ น้ำตาลทราย+ซีอิ๊วดำ+ซีอิ๊วขาว+ซอสหอยนางรม+น้ำซุปต้มสุก คนผสมจนน้ำตาลทรายละลายเข้าด้วยกัน
น้ำกุ้งล้างน้ำให้สะอาดและแช่คลุกลงไปให้น้ำปรุงรสที่ผสมไว้เมื่อสักครู่ เพื่อให้น้ำปรุงซึมเข้าเนื้อกุ้งเล็กน้อยคลุกจนถ้วนทั่วจากนั้นก็ตักออกพักไว้ก่อน
มาทำส่วนวุ้นเส้น ให้นำวุ้นเส้นแช่น้ำเปล่าสักพักเพื่อให้เส้นมีความนุ่มขึ้นเล็กน้อย จากนั้นก็นำวุ่นเส้นไปคลุกนำปรุงที่ทำไว้ให้ทั่วได้เลย
ตั้งกระทะตั้งไฟพออ่อน ฝานผัดขิง สับกระเทียม และเม็ดพริกไทยดำ นำลงไปผัดพอขึ้นกลิ่นหอมไม่ต้องให้สุกเกรียมจนเกินไป (สังเกตว่ากระเทียมเหลืองอ่อนสวยส่งกลิ่นหอม) ปิดไฟก่อน
เตรียมหม้อหรือกระทะที่ผัดเมื่อสักครู้ โดยนำส่วนผสมที่ผัดไว้ด้านล่าง นำกุ้งวางด้านล่างสัก 2 ตัว ตามด้วยวุ้นเส้นชั้นบนให้วางกุ้งที่เหลือ ใส่ผักที่เตรียมไว้ ได้แก่ คื่นช่ายและต้นหอม อาจจะโดรยพริกไทยขาวเพิ่มเติมลงไปเล็กน้อย (ตามความชอบ)
ตั้งไฟแค่พออ่อน เพื่อทำการอบ จับเวลา 5 นาที
ตักเสิร์ฟได้เลย นิยมเสิร์ฟทั้งหม้อ
เคล็ดลับความอร่อยของการทำกุ้งอบวุ้นเส้น

เคล็ดลับสำคัญคือ จะต้องเลือกกุ้งก้ามกรามเพราะกุ้งเหมือนเป็นพระเอกของงานนี้เลยทีเดียว จะต้องเลือกกุ้งก้ามกรามที่มีความสดใหม่ ขนาดพอดีหม้อ(เผื่อหดเล็กน้อย) นอกจากนี้ยังต้องเลือกส่วนผสมอื่น ๆ ที่สดใหม่ด้วยก็จะดีมาก
`,
    },
    {
      title: "Manoonchai.com",
      text: `มนูญชัย
แป้นพิมพ์ภาษาไทยทางเลือกใหม่ สร้างจากปัญญาประดิษฐ์และฐานข้อมูลขนาดใหญ่ของการพิมพ์ภาษาไทยในยุคปัจจุบัน พิมพ์ง่ายกว่าแป้นพิมพ์เกษมณีถึง 45%

ดาวน์โหลด
ทดลองพิมพ์
เข้าคอมมูนิตี้ Discord

แป้นพิมพ์มนูญชัย
สร้างจากข้อมูลขนาดใหญ่ ผ่าน Algorithm และ AI

เพื่อลดความเอนเอียง (Bias) ของข้อมูล เราใช้ฐานข้อมูลจากหลายแหล่งเพื่อเฉลี่ย และสร้างแป้นพิมพ์ด้วย Algorithm โดยใช้ AI ในการประมวลผลหาแป้นพิมพ์ที่มีประสิทธิภาพมากที่สุด
123
ใช้เลขอารบิกเป็นค่าเริ่มต้น

การใช้งานภาษาไทยในปัจจุบันแทบไม่มีการพิมพ์เลขไทยแล้ว เราจึงนำเลขอารบิกเป็นค่าเริ่มต้นแทน เมื่อต้องการพิมพ์ตัวเลข ผู้ใช้ไม่จำเป็นต้องสลับเป็นแป้นพิมพ์ภาษาอังกฤษอีกต่อไป (หากต้องการพิมพ์เลขไทยยังสามารถพิมพ์ด้วยการกด Alt ค้างเอาไว้ได้)
สมดุลย์การพิมพ์ด้วยมือซ้ายและขวา

ตัวอักษรไทยบนแป้นพิมพ์เกษมณีมีความไม่สมดุลย์ โดยหนักไปทางมือขวาถึง 70% แต่แป้นพิมพ์มนูญชัยจะมีน้ำหนักโดยสัดส่วน มือซ้าย:มือขวา อยู่ที่ 47%:53%
ไม่มีตัวอักษรไทยบนแถวตัวเลข

บนแป้นพิมพ์มนูญชัย ตัวจะไม่มีตัวอักษรไทยอยู่บนแถวตัวเลข เหมาะกับการใช้กับคีย์บอร์ดแลปทอป หรือคีย์บอร์ดขนาดเล็กที่มีความนิยมมากขึ้นในปัจจุบัน
โครงการแบบ Open-Source

โค้ดทั้งหมดเปิดเผยแบบ Open-Source ด้วยสัญญาอนุญาตแบบ MIT สามารถนำไปใช้ซ้ำ หรือต่อยอดเป็นแป้นพิมพ์รูปแบบอื่นๆ ได้ อีกทั้งยังเปิดโอกาสให้ผู้ที่สนใจมา Contribute ในโครงการได้ด้วย
`,
    },
    {
      title: "กรุงเทพมหานคร",
      text: "กรุงเทพมหานคร อมรรัตนโกสินทร์ มหินทรายุธยา มหาดิลกภพ นพรัตนราชธานีบูรีรมย์ อุดมราชนิเวศน์มหาสถาน อมรพิมานอวตารสถิต สักกะทัตติยวิษณุกรรมประสิทธิ์",
    },
    {
      title: "จริตขี้ประจบ",
      text: "ดูจากตำแหน่งปุ่มแล้วความคิดเห็นส่วนตัวผมนะทำไมเหมือนไม่ใช่ AI คิด แต่ จริตคนคิดนี่แหละจริตขี้ประจบด้วย สังเกตมั้ยของเก่าเค้าคิดมาอย่างดี วางสระไว้รวม ๆ กันเพื่อให้เข้าใจได้ง่าย ๆ แต่นี่วางตัวสะเปะสะมั่วไปหมด ถ้า AI จะโง่ขนาดนี้นะ ลบทิ้่งเหอะ และอีกข้อ กูว่าเอไอไม่น่าจะประจบคนเป็น ตรงแถวร่างสุด ไทย ผมว่ามันไม่น่าจะบังเอิญเรียงได้ขนาดนี้นะ แถมถ้านับตัวอักษรที่เหลือด้านหลัง มันเติมคำว่าจงเจริญเข้าไปได้เลย เอไอมันประจบเก่งขนาดนี้เลยเหรอ",
    },
    {
      title: "Bodyslam - ยาพิษ",
      text: `
      คำง่ายง่ายแต่ความหมายสุดลึกล้ำ
      คำง่ายง่ายที่เธอใช้ประจำ
      ซ้ำไปซ้ำมา
      คิดจะพูดแต่ก็พูดอย่างไม่คิด
      รู้ไหมว่าหนึ่งชีวิตของใคร
      ต้องเกิดปัญหา

      [Pre-Chorus]
      เจ็บช้ำปางตาย
      ชีวิตวุ่นวาย
      คิดมันไปว่าจริง
      ลุ่มหลงเชื่อใจ
      กับถ้อยคำร้ายร้าย

      [Chorus]
      เอะอะก็ว่ารัก
      เอะอะก็คิดถึง
      แต่เธอไม่เคยซึ้งไม่เคยเข้าใจ
      ไม่เคยทำให้รู้
      ไม่เคยทำให้เห็น
      ไม่ห่วงเลยว่าใครจะเป็นจะตาย
      คำพูดที่ไม่เคยคิด
      ที่จริงก็คือยาพิษ
      ทำลายชีวิตของคนงมงาย
      เธอจะรู้บ้างหรือเปล่า
      คิดหรือเปล่า
      ว่ามีใครเขาทุกข์ทน
      พิษของคำคน
      ร้ายแรงแค่ไหน

      [Bridge]
      คำง่ายง่ายที่เธอใช้บอกกับฉัน
      รู้ไว้ด้วยว่าความหมายของมัน
      สำคัญแค่ไหน

      [Pre-Chorus]
      เจ็บช้ำปางตาย
      ชีวิตวุ่นวาย
      คิดมันไปว่าจริง
      ลุ่มหลงเชื่อใจ
      กับถ้อยคำร้ายร้าย

      [Chorus]
      เอะอะก็ว่ารัก
      เอะอะก็คิดถึง
      แต่เธอไม่เคยซึ้งไม่เคยเข้าใจ
      ไม่เคยทำให้รู้
      ไม่เคยทำให้เห็น
      ไม่ห่วงเลยว่าใครจะเป็นจะตาย
      คำพูดที่ไม่เคยคิด
      ที่จริงก็คือยาพิษ
      ทำลายชีวิตของคนงมงาย
      เธอจะรู้บ้างหรือเปล่า
      คิดหรือเปล่า
      ว่ามีใครเขาทุกข์ทน
      พิษของคำคน
      ร้ายแรงแค่ไหน

      [Guitar Solo]

      [Verse 2]
      ล้านคำลวงหลอกหลอนหัวใจ
      วาดวิมานบนฟ้าแสนไกล
      ล้วนเติมแต่งจากคำของใคร
      แล้วความจริงอยู่ตรงที่ใด
      เชื่อคำลวงสุดท้ายเสียใจ
      โลกความจริงเรียนรู้หมุนไป
      ทบและทวนใตร่ตรองข้างใน
      ให้เวลาตัดสินหัวใจ

      [Chorus]
      เอะอะก็ว่ารัก
      เอะอะก็คิดถึง
      แต่เธอไม่เคยซึ้งไม่เคยเข้าใจ
      ไม่เคยทำให้รู้
      ไม่เคยทำให้เห็น
      ไม่ห่วงเลยว่าใครจะเป็นจะตาย
      คำพูดที่ไม่เคยคิด
      ที่จริงก็คือยาพิษ
      ทำลายชีวิตของคนงมงาย
      เธอจะรู้บ้างหรือเปล่า
      รู้บ้างหรือเปล่า
      คำที่เธอนั้นพร่ำบอก
      รักที่ลวงหลอก
      รักที่ลวงหลอก
      ทำให้ใครเขาทุกข์ทน
      พิษของคำคน
      `,
    },
  ]

  let input = textPresets[0].text

  let heatmapMnc: number[][] = []
  let heatmapKed: number[][] = []

  let inputChars: string[]

  let toggleAdditionalKey = false
  let mncAdditionalKey = {
    shift: 0,
    altGr: 0,
  }
  let kedAdditionalKey = {
    shift: 0,
    altGr: 0,
  }
  let enterCount = 0;
  let spaceCount = 0;

  $: {
    input
    redraw()
  }

  function redraw() {
    inputChars = input.split("")
    resetHeatmaps()

    populateHeatmap(manoonchaiKeymap, heatmapInstanceMnc, heatmapMnc, mncAdditionalKey)
    populateHeatmap(kedmaneeKeymap, heatmapInstanceKed, heatmapKed, kedAdditionalKey)
    drawHeatmap(heatmapCanvasManoonchai, manoonchaiImageElement, heatmapInstanceMnc, heatmapMnc, mncAdditionalKey)
    drawHeatmap(heatmapCanvasKedmanee, kedmaneeImageElement, heatmapInstanceKed, heatmapKed, kedAdditionalKey)
  }

  function resetHeatmaps() {
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
    mncAdditionalKey = {
      shift: 0,
      altGr: 0,
    }
    kedAdditionalKey = {
      shift: 0,
      altGr: 0,
    }
    enterCount = 0;
    spaceCount = 0;
  }

  function populateHeatmap(keymap: { keys: string[][][] }, heatmapInstance, heatmap: number[][], additionalKey: { shift: number, altGr: number }) {
    inputChars.forEach((char, _index) => {
      if (char === ' ') {
        spaceCount += 1;
        return;
      }
      if (char === '\n') {
        enterCount += 1;
        return;
      }

      // using for loop with circuit breaker to speed up iteration for a lil'bit
      // must be sure that all chars in given keymap are unique
      for(let rowIndex in keymap.keys) {
        let breakLoop = false;
        keymap.keys[rowIndex].forEach((keys, keyIndex) => {
          const tmpIndex = keys.indexOf(char);
          if (tmpIndex !== -1) {
            if (heatmapInstance) heatmap[rowIndex][keyIndex] += 1
            if (tmpIndex === 1) additionalKey.shift += 1;
            else if (tmpIndex === 2) additionalKey.altGr += 1;
            breakLoop = true;
            return;
          }
        });
        if (breakLoop) return;
      }

      // let x, y
      // keymap.keys.forEach((row, rowIndex) => {
      //   row.forEach((keys, keyIndex) => {
      //     if (keys.includes(char)) {
      //       x = rowIndex
      //       y = keyIndex
      //     }
      //   })
      // })

      // if (x != undefined && y != undefined && heatmapInstance) {
      //   heatmap[x][y] += 1
      // }
    })
  }

  function drawHeatmap(heatmapCanvas: HTMLElement, imageElement, heatmapInstance, heatmap, additionalKey: { shift: number, altGr: number }) {
    const coords = []
    const canvasWidth = imageElement?.getBoundingClientRect().width

    if (heatmapCanvas && canvasWidth) {
      heatmapCanvas.style.width = canvasWidth
      heatmapCanvas.style.height = canvasWidth
    }
    let canvasRatio = 0.7 // Default width : 700px
    if (canvasWidth) {
      canvasRatio = canvasWidth / 1000.0
    }

    heatmap.forEach((row, rowIndex) => {
      row.forEach((value, colIndex) => {
        if (value > 0) {
          coords.push({ ...indexToCoordinate(rowIndex, colIndex, canvasRatio), value })
        }
      })
    })


    const specialKeyOffset = [
      {x: 452, y: 4}, // altGr
      {x: 589, y: 2}, // enter
      {x:  20, y: 3}, // shift L
      {x: 576, y: 3}, // shift R
      {x: 282, y: 4}, // space
    ]
    const pushCoords = ({ x, y }, value) => {
      coords.push({
        x: Math.round(x + (64.5) * canvasRatio),
        y: Math.round(35 + (64.5) * y * canvasRatio),
        value,
      })
    }
    if (toggleAdditionalKey) {
      if (additionalKey.altGr > 0) pushCoords(specialKeyOffset[0], additionalKey.altGr)
      if (enterCount > 0) pushCoords(specialKeyOffset[1], enterCount)
      if (additionalKey.shift > 0) {
        pushCoords(specialKeyOffset[2], additionalKey.shift)
        pushCoords(specialKeyOffset[3], additionalKey.shift)
      }
      if (spaceCount > 0) pushCoords(specialKeyOffset[4], spaceCount)
    }

    // const radius = 60 * canvasRatio
    // console.log({ radius })
    // heatmapInstance?.configure({
    //   container: heatmapCanvas,
    //   radius,
    //   maxOpacity: 0.6,
    //   minOpacity: 0,
    //   blur: 0.5 * canvasRatio,
    //   gradient: {
    //     0.45: "rgb(0,0,255)",
    //     0.55: "rgb(0,255,255)",
    //     0.65: "rgb(0,255,0)",
    //     0.95: "yellow",
    //     1.0: "rgb(255,0,0)",
    //   },
    // })
    heatmapInstance?.setData({ max: max(heatmap), min: 0, data: coords })
  }

  function adjustCanvasSize(container: HTMLElement) {
    const canvas: HTMLCanvasElement = container?.getElementsByTagName("canvas")?.[0]
    const img: HTMLImageElement = container?.getElementsByTagName("img")?.[0]
    if (canvas) {
      canvas.width = img?.getBoundingClientRect().width
      canvas.height = img?.getBoundingClientRect().height
    }
  }

  function indexToCoordinate(row: number, col: number, widthRatio: number = 1) {
    let xStart = [48, 146, 162, 194].map((x) => x * widthRatio)

    const co = {
      x: Math.round(xStart[row] + (60 + 4.5) * col * widthRatio),
      y: Math.round(xStart[0] + (60 + 4.5) * row * widthRatio),
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

  function windowResizeHandler() {
    redraw()
  }
</script>

<svelte:window on:resize={windowResizeHandler} />

<Kofi name="narze" label="Support Me" />
<Menu items={menuItems} />
<Head {title} {description} {url} {imageUrl} {gtagId} />

<main class="w-full h-screen flex flex-col items-center p-4">
  <h1 class="text-3xl mb-2">Heatmap Analyzer</h1>

  <h2 class="text-xl">Manoonchai</h2>
  <div style="width: 700px; height: 248px;" bind:this={heatmapCanvasManoonchai}>
    <img
      src={manoonchaiSvg}
      bind:this={manoonchaiImageElement}
      alt="keymap"
      class="max-w-full max-h-full z-0"
    />
  </div>

  <h2 class="text-xl">Kedmanee</h2>
  <div style="width: 700px; height: 248px;" bind:this={heatmapCanvasKedmanee}>
    <img
      src={kedmaneeSvg}
      bind:this={kedmaneeImageElement}
      alt="keymap"
      class="max-w-full max-h-full"
    />
  </div>

  <h2 class="text-xl">Text</h2>
  <textarea class="border m-4" bind:value={input} cols="80" rows="10" />

  <span>
    แสดงheatmapของปุ่มนอกเหนือตัวอักษร &nbsp;
    <input type="checkbox" bind:checked={toggleAdditionalKey}
    on:change={() => { redraw(); }} />
  </span>
  

  เลือก Preset
  <select bind:value={selectedPreset} on:change={() => (input = selectedPreset.text)}>
    {#each textPresets as preset}
      <option value={preset}>
        {preset.title}
      </option>
    {/each}
  </select>
</main>

<style>
  :root {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen, Ubuntu, Cantarell,
      "Open Sans", "Helvetica Neue", sans-serif;
  }
</style>
