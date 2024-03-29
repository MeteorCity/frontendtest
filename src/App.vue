<script setup>
  import { ref } from 'vue';

  const baseSizes = { 
    boardWidth: 800,
    boardHeight: 800,
    fontSize: 20,
    sidebarWidth: window.innerWidth > 768 ? 250 : 800, /* Check which configuration */
    sidebarHeight: window.innerWidth > 768 ? 800 : 250
  };

  const boardWidth = ref(baseSizes.boardWidth * Math.min(window.innerWidth / 1440, window.innerHeight / 900));
  const boardHeight = ref(baseSizes.boardHeight * Math.min(window.innerWidth / 1440, window.innerHeight / 900));
  const fontSize = ref(baseSizes.fontSize * Math.min(window.innerWidth / 1440, window.innerHeight / 900));
  const sidebarWidth = ref(baseSizes.sidebarWidth * Math.min(window.innerWidth / 1440, window.innerHeight / 900));
  const sidebarHeight = ref(baseSizes.sidebarHeight * Math.min(window.innerWidth / 1440, window.innerHeight / 900));

  const clickedList = ref([]);

  const handleResize = () => {
    const widthRatio = window.innerWidth / 1440;
    const heightRatio = window.innerHeight / 900;
    const resizeRatio = Math.min(widthRatio, heightRatio);

    // Check if the window is mobile or desktop
    if (window.innerWidth <= 768) {
      baseSizes.sidebarWidth = 800;
      baseSizes.sidebarHeight = 250;
    } else {
      baseSizes.sidebarWidth = 250;
      baseSizes.sidebarHeight = 800;
    }

    // Update sizes
    boardWidth.value = baseSizes.boardWidth * resizeRatio;
    boardHeight.value = baseSizes.boardHeight * resizeRatio;
    fontSize.value = baseSizes.fontSize * resizeRatio;
    sidebarWidth.value = baseSizes.sidebarWidth * resizeRatio;
    sidebarHeight.value = baseSizes.sidebarHeight * resizeRatio;
  }

  const handleClick = (e) => {
    const target = e.target;
    
    // Check if the square was clicked or whether it was something else
    if (target.id) {
      target.classList.toggle("highlight");

      // Check if the square is already in the list
      if (!clickedList.value.includes(target.id)) {
        clickedList.value.push(target.id);
      } else {
        const idIndex = clickedList.value.indexOf(target.id);
        clickedList.value.splice(idIndex, 1);
      }
    } else {
      // Check if the target clicked was the inner number or letter
      if (target.parentNode.id) {
        target.parentNode.classList.toggle("highlight");

        if (!clickedList.value.includes(target.parentNode.id)) {
          clickedList.value.push(target.parentNode.id);
        } else {
          const idIndex = clickedList.value.indexOf(target.parentNode.id);
          clickedList.value.splice(idIndex, 1);
        }
      }
    }
  }

  window.addEventListener('resize', handleResize);
</script>

<template>
  <div class="content">
    <main
      :style="{width: `${boardWidth}px`, height: `${boardHeight}px`}"
      class="board"
      @click="handleClick"
    >
      <!-- Could use nested for loops to set up the board's squares but this is much 
           simpler and more readable since I'm including inner content for some -->
      <!-- 8th Row -->
      <div class="light-square" id="a8">
        <div :style="{fontSize: `${fontSize}px`}" class="dark-number">8</div>
      </div>
      <div class="dark-square" id="b8"></div>
      <div class="light-square" id="c8"></div>
      <div class="dark-square" id="d8"></div>
      <div class="light-square" id="e8"></div>
      <div class="dark-square" id="f8"></div>
      <div class="light-square" id="g8"></div>
      <div class="dark-square" id="h8"></div>
      <!-- 7th Row -->
      <div class="dark-square" id="a7">
        <div :style="{fontSize: `${fontSize}px`}" class="light-number">7</div>
      </div>
      <div class="light-square" id="b7"></div>
      <div class="dark-square" id="c7"></div>
      <div class="light-square" id="d7"></div>
      <div class="dark-square" id="e7"></div>
      <div class="light-square" id="f7"></div>
      <div class="dark-square" id="g7"></div>
      <div class="light-square" id="h7"></div>
      <!-- 6th Row -->
      <div class="light-square" id="a6">
        <div :style="{fontSize: `${fontSize}px`}" class="dark-number">6</div>
      </div>
      <div class="dark-square" id="b6"></div>
      <div class="light-square" id="c6"></div>
      <div class="dark-square" id="d6"></div>
      <div class="light-square" id="e6"></div>
      <div class="dark-square" id="f6"></div>
      <div class="light-square" id="g6"></div>
      <div class="dark-square" id="h6"></div>
      <!-- 5th Row -->
      <div class="dark-square" id="a5">
        <div :style="{fontSize: `${fontSize}px`}" class="light-number">5</div>
      </div>
      <div class="light-square" id="b5"></div>
      <div class="dark-square" id="c5"></div>
      <div class="light-square" id="d5"></div>
      <div class="dark-square" id="e5"></div>
      <div class="light-square" id="f5"></div>
      <div class="dark-square" id="g5"></div>
      <div class="light-square" id="h5"></div>
      <!-- 4th Row -->
      <div class="light-square" id="a4">
        <div :style="{fontSize: `${fontSize}px`}" class="dark-number">4</div>
      </div>
      <div class="dark-square" id="b4"></div>
      <div class="light-square" id="c4"></div>
      <div class="dark-square" id="d4"></div>
      <div class="light-square" id="e4"></div>
      <div class="dark-square" id="f4"></div>
      <div class="light-square" id="g4"></div>
      <div class="dark-square" id="h4"></div>
      <!-- 3rd Row -->
      <div class="dark-square" id="a3">
        <div :style="{fontSize: `${fontSize}px`}" class="light-number">3</div>
      </div>
      <div class="light-square" id="b3"></div>
      <div class="dark-square" id="c3"></div>
      <div class="light-square" id="d3"></div>
      <div class="dark-square" id="e3"></div>
      <div class="light-square" id="f3"></div>
      <div class="dark-square" id="g3"></div>
      <div class="light-square" id="h3"></div>
      <!-- 2nd Row -->
      <div class="light-square" id="a2">
        <div :style="{fontSize: `${fontSize}px`}" class="dark-number">2</div>
      </div>
      <div class="dark-square" id="b2"></div>
      <div class="light-square" id="c2"></div>
      <div class="dark-square" id="d2"></div>
      <div class="light-square" id="e2"></div>
      <div class="dark-square" id="f2"></div>
      <div class="light-square" id="g2"></div>
      <div class="dark-square" id="h2"></div>
      <!-- 1st Row -->
      <div class="dark-square" id="a1">
        <div :style="{fontSize: `${fontSize}px`}" class="light-number">1</div>
        <div :style="{fontSize: `${fontSize}px`}" class="light-letter">a</div>
      </div>
      <div class="light-square" id="b1">
        <div :style="{fontSize: `${fontSize}px`}" class="dark-letter">b</div>
      </div>
      <div class="dark-square" id="c1">
        <div :style="{fontSize: `${fontSize}px`}" class="light-letter">c</div>
      </div>
      <div class="light-square" id="d1">
        <div :style="{fontSize: `${fontSize}px`}" class="dark-letter">d</div>
      </div>
      <div class="dark-square" id="e1">
        <div :style="{fontSize: `${fontSize}px`}" class="light-letter">e</div>
      </div>
      <div class="light-square" id="f1">
        <div :style="{fontSize: `${fontSize}px`}" class="dark-letter">f</div>
      </div>
      <div class="dark-square" id="g1">
        <div :style="{fontSize: `${fontSize}px`}" class="light-letter">g</div>
      </div>
      <div class="light-square" id="h1">
        <div :style="{fontSize: `${fontSize}px`}" class="dark-letter">h</div>
      </div>
    </main>

    <div 
      :style="{width: `${sidebarWidth}px`, height: `${sidebarHeight}px`}" 
      class="sidebar"
    >
      <div :style="{fontSize: '20px'}" v-for="(clickedID, idx) in clickedList" :key="idx">
        {{ idx + 1 }}. {{ clickedID }}
      </div>
    </div>
  </div>
</template>
