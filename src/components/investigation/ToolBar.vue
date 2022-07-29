<template>
  <div class="toolbar">
    <button v-on:click="click">добавить карточку SVG</button>
    <button v-on:click="click1">добавить карточку div</button>
    <div>{{ val }}</div>
  </div>
</template>

<script>
import {
  SVG,
  extend as SVGextend,
  Element as SVGElement,
} from "@svgdotjs/svg.js";


//https://html5css.ru/howto/howto_js_draggable.php
// dragElement(document.getElementById(("card")));

function dragElement(elmnt) {
  var pos1 = 0, pos2 = 0, pos3 = 0, pos4 = 0;
  if (document.getElementById(elmnt.id + "header")) {
    /* if present, the header is where you move the DIV from:*/
    document.getElementById(elmnt.id + "header").onmousedown = dragMouseDown;
  } else {
    /* otherwise, move the DIV from anywhere inside the DIV:*/
    elmnt.onmousedown = dragMouseDown;
  }

  function dragMouseDown(e) {
    e = e || window.event;
    // get the mouse cursor position at startup:
    pos3 = e.clientX;
    pos4 = e.clientY;
    document.onmouseup = closeDragElement;
    // call a function whenever the cursor moves:
    document.onmousemove = elementDrag;
  }

  function elementDrag(e) {
    e = e || window.event;
    // calculate the new cursor position:
    pos1 = pos3 - e.clientX;
    pos2 = pos4 - e.clientY;
    pos3 = e.clientX;
    pos4 = e.clientY;
    // set the element's new position:
    elmnt.style.top = (elmnt.offsetTop - pos2) + "px";
    elmnt.style.left = (elmnt.offsetLeft - pos1) + "px";
  }

  function closeDragElement() {
    /* stop moving when mouse button is released:*/
    document.onmouseup = null;
    document.onmousemove = null;
  }
}

export default {
  name: "ToolBar",
  data() {
    return {
      val: 0,
    };
  },
  methods: {
    click() {
      this.val++;
      var draw = SVG().addTo("#workspace").size(300, 300);
      var rect = draw.rect(100, 100).attr({ fill: "#f06" });
      rect.attr({ id: "card" });
    },
    click1() {
      this.val++;

        let workspace = document.getElementById('workspace')
        console.log(workspace)

        let card = document.createElement('div')
        card.setAttribute('id', 'card')
        card.setAttribute('fill', '#f06')
        card.setAttribute('width', '150')
        card.setAttribute('height', '150')
        card.setAttribute('zIndex', '150')
        //   var draw = SVG().addTo("#workspace").size(300, 300);
        //   var rect = draw.rect(100, 100).attr({ fill: "#f06" });
        // card.attr({ id: "card", fill: "#f06" });
        workspace.append(card)
    },
  },
};
</script>

<style>
.toolbar {
  width: 100%;
  height: 50px;

  border: solid 2px black;
}
</style>