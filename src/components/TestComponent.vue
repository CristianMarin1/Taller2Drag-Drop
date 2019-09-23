<template>
    <div>
        <link rel="stylesheet" type="text/css" href="http://code.jquery.com/ui/1.9.2/themes/base/jquery-ui.css">
        <h1>{{ msg }}</h1>
        <h2>Input recibido en Componente: {{ $route.params }}</h2>
        <button @click="testFun">Test</button>
        <div id="div1" @drop="drop" @dragover="allowDrop">
            <img id="drag1" src="https://www.w3schools.com/html/img_logo.gif" draggable="true" @dragstart="drag">
        </div>
        <div id="div1" @drop="drop" @dragover="allowDrop"></div>
        <br><br><br><br><br><br>
        <div id="mydiv"></div>
        <div style="width:251px;float:left;">
          <div class="draggable">test1!</div>
          <div class="draggable">test2!</div>
          <div class="draggable">test3!</div>
          <div class="draggable">test4!</div>
          <div class="draggable">test5!</div>
          <div class="draggable">test6!</div>
          <div class="draggable">test7!</div>
        </div>
    </div>
</template>

<script>
var form = `<div class="tmpform">
          <span class="tmpspan">UserName</span>
          <input type="text" name="username" value=""><br>
          <span class="tmpspan">Password</span>
          <input type="text" name="password" value=""><br>
          <span class="tmpspan">RandomName</span>
          <input type="text" name="randomname" value=""><br>
        </div>`;

export default {
  name: 'TestComponent',
  props: {
    msg: String
  },
  methods: {
    testFun: function() {
        console.log("Hola");
    },
    allowDrop: function (ev) {
        ev.preventDefault();
    },
    drag: function (ev) {
        ev.dataTransfer.setData("text", ev.target.id);
    },
    drop: function (ev) {
        ev.preventDefault();
        var data = ev.dataTransfer.getData("text");
        ev.target.appendChild(document.getElementById(data));
    }
  },
  mounted() {
      $(".draggable").draggable({
        revert: true,
        helper: 'clone',
        start: function(event, ui) {
            $(this).fadeTo('fast', 0.5);
        },
        stop: function(event, ui) {
            $(this).fadeTo(0, 1);
        }
    });
    $("#mydiv").droppable({
        hoverClass: 'active',
        drop: function(event, ui) {
            if(event.toElement.id!="div2"){
                $( "#mydiv" ).append( ui.draggable.context.innerText + form );
                var objDiv = $("#mydiv")[0];
                objDiv.scrollTop = objDiv.scrollHeight;
            }
        }
    });
    function drag(e) {}
  }
}
</script>

<style>
    #div1, #div2{
        float:left;
        width:280px;
        height:55px;
        margin:10px;
        padding:10px;
        border:1px solid #aaaaaa;
    }
    #drag1{
        width: 100%;
    }
    body {
            font-family: Consolas;
            font-size: 11pt;
        }
        .draggable {
            width: 250px;
            height: 20px;
            background-color: #e6eaff;
            border: 2px solid #3399cc;
            margin-bottom: 1em;
            margin-left: 50px;
            padding: 4px;
            cursor: default;
        }
        .active {
            border: 2px solid #6699ff;
        }

        #mydiv
        {
            width: 800px;
            height: 500px;
            background-color: #e6eaff;
            border: 2px solid #3399cc;
            margin-bottom: 1em;
            padding: 4px;
            cursor: default;
            overflow-y: scroll;
            float: left;
        }
        .tmpspan{
          display: inline-block;
          width: 80px;
        }
        .tmpform{
          margin: 10px;
        }
</style>