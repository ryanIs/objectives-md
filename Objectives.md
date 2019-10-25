<script type="text/javascript">
/**
 * Displays objectives across a number of different disciplines.
 * 
 * Note: to get markdown features - use HTML and CSS to manually add the task.
 * 
 * @version: 0.8.0
 */

  // Whether or not to load the our 'SAVED_FILTERS'
  const LOAD_FILTERS = false

  // Content of our 'saved file.' Paste your SAVED_FILTERS string here.
  var SAVED_FILTERS = `
  
  `

  // During runtime, this object stores the 'saved file.'
  var objSavedFilters

  // List of links to all available icon files
  const ICONS = {
    JS: "img/icons/js.png",
    HYPER_CUBE: "img/icons/hypercube.ico",
    ART: "img/icons/art.ico",
    BULLETS: "img/icons/bullets.ico",
    CLOUDS: "img/icons/cloud.ico",
    COLORCLOUDS: "img/icons/colorclouds_ESI_icon.ico",
    DOUBLE_PAGE: "img/icons/double-page.ico",
    DYSON_SPHERE: "img/icons/dyson-sphere.ico",
    EAX: "img/icons/eax.ico",
    GAMING: "img/icons/gaming.ico",
    GREEN: "img/icons/green.ico",
    JAPAN: "img/icons/japan.ico",
    LINESPIN: "img/icons/linespin.ico",
    MONEY: "img/icons/money.ico",
    MUSIC: "img/icons/music.ico",
    NUMBER_0: "img/icons/number-0.ico",
    NUMBER_1: "img/icons/number-1.ico",
    NUMBER_9: "img/icons/number-10.ico",
    NUMBER_9: "img/icons/number-11.ico",
    NUMBER_9: "img/icons/number-12.ico",
    NUMBER_9: "img/icons/number-2.ico",
    NUMBER_9: "img/icons/number-3.ico",
    NUMBER_9: "img/icons/number-4.ico",
    NUMBER_9: "img/icons/number-5.ico",
    NUMBER_9: "img/icons/number-6.ico",
    NUMBER_9: "img/icons/number-7.ico",
    NUMBER_9: "img/icons/number-8.ico",
    NUMBER_9: "img/icons/number-9.ico",
    PENCIL: "img/icons/pencil.ico",
    PIXI_P: "img/icons/pixi-p.ico",
    REDSWORD: "img/icons/redsword.ico",
    RESUME: "img/icons/resume.ico",
    SINGLE_PAGE: "img/icons/single-page.ico",
    SUN: "img/icons/sun.ico",
    VUE: "img/icons/vue.ico",
    DUMBELL: "img/icons/dumbell.png",
    WEBDEV: "img/icons/webdev.png",
  }

  // This is the default styling for task_images
  const DEFAULT_TASK_IMAGE_STYLE = [
    ["width", "auto"],
    ["height", "40px"],
    ["marginRight", "10px"],
    ["marginTop", "2px"]
  ]

  // Template string shorthand expressions to be used in the task description string
  const TABA = "&emsp;&emsp;", // Single tab
        TABB = "&emsp;&emsp;&emsp;&emsp;", // Double tab
        TABC = "&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;", // Triple tab
        X = "<x></x>", // Completed checkbox
        O = "<o></o>", // Incompleted checkbox
        TOG = function(hiddenContent) { // Dynamic toggle option
          return `
            <span style="display: inline-block; margin: 0; padding: 0; "><input type="button" style="float: left; width: 13px; height: 13px; margin: 0; padding: 0; opacity: 0.6; margin-right: 7px; font-size: 0.6em; transition: height 0.5s; " value="+" onclick="c=this.parentNode.getElementsByTagName('con')[0]; c.style.display = (c.style.display == 'block') ? ((this.value='+',this.style.height='13px'), ('none')) : ((this.value='',this.style.height='20px'), ('block')); "><con style="display: none; float: left; margin: 0; padding: 0; ">${hiddenContent}</con></span>
          `
        },
        ICO = function(iconImage) { // Insert icon
          return `
            <img src="${ICONS[iconImage]}" style="width: 20px; height: 20px; display: inline-block; ">
          `
        }

  // The main projects object. This object contains all project information in your 'Objectives.md' file.
  var MY_PROJECTS = [

  // Project: General
  {
    projectName: "General",
    projectId: "general",
    projectDescription: "General tasks to complete",
    projectProgress: -1,
    projectHidden: false,
    projectImage: {
      src: "img/general-header.png",
      style: []
    },

    tasks: [

    // Task 1
    {
      name: "Complete a general task",
      taskName: "General Task",
      taskId: "gen-task",
      status: "",
      inProgress: false,
      description: `
        <span left>I am a task!</span> <br> <br>

        Here is my list: <br>
        <ul>
          <li>Simple list item # 1</li>
          <li>Simple list item # 2</li>
          <li>Simple list item # 3</li>
        </ul>
      `,
      taskImage: {
        src: ICONS.ART
      } 
    },

    // Task 2
    {
      name: "Complete a general task # 2",
      taskName: "General Task 2",
      taskId: "gen-task2",
      status: "MEDIUM",
      inProgress: false,
      description: `
        I am aother task! I will look at the clouds.
      `,
      taskImage: {
        src: ICONS.CLOUDS,
        style: [
          ["width", "55px"],
          ["height", "auto"],
          ["marginRight", "10px"]
        ]
      } 
    }],
  },
  
  // Project: Create a box project
  {
    projectName: "Create a box",
    projectId: "box",
    projectDescription: "I will create a box for this project",
    projectProgress: 50,
    projectProgressTitle: "50%:   Get the materials(5)\n\n100%: Assemble the box",
    projectHidden: false,
    projectImage: null,
    tasks: [

      // Task 1
      {
        name: "Get the materials required to assemble this box",
        taskName: "box-mats",
        taskId: "box-mats",
        status: "DONE",
        inProgress: false,
        description: `
          Look for vendors and then purchase items from the vendors.<br>
          <name done>
            Talk to vendors
          </name>
          <name done>
            Purchase the items
          </name>
        `,
        taskImage: {
          src: ICONS.MONEY
        }
      },

      // Task 2
      {
        name: "Assemble the box",
        taskName: "boxes-assemble",
        taskId: "boxes-assemble",
        status: "HIGH",
        inProgress: true,
        taskProgress: 45,
        description: `
          Refer to the building manual and build the box. <br>
          Try to make the box perfectly square! Or else it won't be a box. <br> <br>

          <name done> Measure all sides </name>
          <name> Boxes ... Assemble! </name>

          I love to assemble: ${TOG(`boxes!`)}<br> 
        `,
        taskImage: {
          src: ICONS.CLOUDS
        },
      },
      
      // Insert your new task here

    ]
  },
  
  // Insert your new project here

  ]

</script>

<!-- Navigation -->
<nav id="nav-projects">
  <section class="filter-checkbox-container" title="Show/hide (default, progress, done, low, medium, high) tasks.">
    <input type="checkbox" id="default-filter" class="filter-checkbox" checked />
    <input type="checkbox" id="low-filter" class="filter-checkbox" checked />
    <input type="checkbox" id="medium-filter" class="filter-checkbox" checked />
    <input type="checkbox" id="high-filter" class="filter-checkbox" checked />
    <input type="checkbox" id="progress-filter" class="filter-checkbox" checked />
    <input type="checkbox" id="done-filter" class="filter-checkbox" checked />
    <textarea id="save-filter" class="clipboard-textarea-plain"  onclick="clipboardCopy(this)" title="Copy SAVED_FILTERS string data to clipboard." readonly></textarea>
  </section>
  
  <section class="minimize-checkbox-container" title="Show/hide (default, progress, done, low, medium, high) descriptions (minizimize).">
    <input type="checkbox" id="default-minimize" class="filter-checkbox" checked />
    <input type="checkbox" id="low-minimize" class="filter-checkbox" checked />
    <input type="checkbox" id="medium-minimize" class="filter-checkbox" checked />
    <input type="checkbox" id="high-minimize" class="filter-checkbox" checked />
    <input type="checkbox" id="progress-minimize" class="filter-checkbox" checked />
    <input type="checkbox" id="done-minimize" class="filter-checkbox" checked />
  </section>
<!--
  <span class="nav-project">
  <a href="#general" onclick="hide('job-batch')">
  General
  </a>
  <span id="bbb">
  <a href="#job-batch" high-priority title="This is a hover-state example">
  Job batches
  </a>
  </span>
  </span>
-->
</nav>

<!--
<img src="img/general-header.png" alt="General" id="general" class="project-image"/>

<div id="job-batch"  class="task">

  <name>
  Batch some jobs together<span right><img style="width: 55px; height: auto; margin-right: 10px;" src="task-img/job-batch.png"></span>
  </name>

  <description>
  
  <span left>My description is super awesome!</span>
  <span right style="font-size: 0.8em; opacity: 0.7; ">I like turtles.</span>
  <br>

  - List item A
  - List item B
  - List item C
  </description>

</div>
-->

<div id='projects'></div>

<style type="text/css">

  /* Global */
  * {
    
  }

  body {
    padding-top: 30px;
    /* background-image: url('https://i.imgur.com/ZOcLM7h.jpg'); */
    background-image: url('img/background.png'); /* If you want to customize your background image, do so here! */

    animation: moveBackground 50s ease 2s infinite alternate;
  }

  @keyframes moveBackground {
      0% { background-color: #fff; background-position: left top; }
      100% { background-color: #eee; background-position: right 500px; } 
  }

  /* Navigation header */
  .nav-task-image {
    display: inline-block;
    width: 10px;
    height: 10px;
    float: left;
    margin: 5px 5px 0 0;
    padding: 0;
  }

  .gray-dot {
    width: 6px;
    height: 6px;
    margin-left: 4px;
    border-radius: 3px;
    background: rgba(120, 120, 120, 0.2);
  }

  .gray-dot:nth-child(even) {
    background: rgba(120, 255, 120, 0.2);
  }
  
  .minimize-checkbox-container {
    position: relative;
    display: block;
    width: 34px;
    height: 30px;
    margin: 0;
    padding: 0;
    float: right;
  }

  .filter-checkbox-container {
    display: block;
    width: 50px;
    height: 30px;
    margin: 0;
    padding: 0;
    float: left;
  }

  .filter-checkbox {
    position: absolute;
    padding: 0;
    margin: 1px 2px 0;
  }

  .filter-checkbox:before {
    content: "";

    display: inline-block;
    width: 10px;
    height: 10px;
    margin: 0 0 5px 0;
  }

  #low-filter, #low-minimize {
    left: 0;
    top: 10px;
  }
  
  #low-filter:before, #low-minimize:before {
    border-color: #c8efff;
    background: rgba(0, 0, 255, 0.3);
  }

  #medium-filter, #medium-minimize {
    left: 10px;
    top: 10px;
  }
  
  #medium-filter:before, #medium-minimize:before {
    border-color: #dfa917;
    background: rgba(150, 40, 0, 0.3);
  }

  #high-filter, #high-minimize {
    left: 20px;
    top: 10px;
  }
  
  #high-filter:before, #high-minimize:before {
    border-color: #ffcac8;
    background: rgba(255, 0, 0, 0.3);
  }
  
  #done-filter, #done-minimize {
    left: 20px;
  }
  
  #done-filter:before, #done-minimize:before {
    border-color: #aaa;
    background: rgba(122, 122, 122, 0.5);
  }
  
  #progress-filter, #progress-minimize {
    left: 10px;
  }
  
  #progress-filter:before, #progress-minimize:before {
    border-color: #ffc;
    background: rgba(255, 200, 122, 0.3);
  }

  nav {
    position: fixed;
    width: 100%;
    height: 20px;
    top: 0;
    left: 0;
    font-family: Arial;
    font-size: 0.9em;
    background: #fff;
    box-shadow: 0 5px 15px 1px rgba(255, 255, 255, 1);

    z-index: 10;
  }

  .nav-project { 
    display: inline-block;
    float: left;
    width: auto;
    height: auto;
    min-width: 100px;
    max-height: 10px;
    background: #fff;
    padding: 5px;

    overflow: hidden;

    box-shadow: 0 0 0 0 rgba(0, 0, 0, 0);
    transition: max-height 0.5s ease-out, box-shadow 1s ease-out;
  }

  .nav-project:hover {
    max-height: 500px;
    height: auto;
    box-shadow: 1px 20px 30px 1px rgba(0, 0, 0, 0.1);
  }

  .nav-project a {
    padding: 0 3px;
  }

  .nav-project > a {
    display: inline-block;
    width: auto;
    text-decoration: none;
    color: #666;

    cursor: pointer;
  }

  .nav-project > a:hover {
    color: #888;
    background-color: #ECECEC;
  }

  .nav-project > span > a {
    display: block;
    margin: 0;
    padding: 3px 3px;
    width: inherit;
    height: 15px;
    border: 1px solid transparent;
    border-color: transparent;

    text-decoration: none;

    transition: opacity 0.3s, border-color 0.3s;
  }

  .nav-project > span > a:hover {
    opacity: 0.7;
    border-color: #f2f2f2;
  }

  nav input {
    display: inline;
    width: 10px;
    height: 10px;
  }

  /* Description classes, themes and ids */

  
  red {
    color: #d00;
  }

  yellow {
    color: #dd0;
  }

  due {
    font-family: "Courier New";
    color: #800;
    background: #ff3;
    padding: 0 20px;
    border-radius: 20px;
    box-shadow: 1px 1px 3px 1px rgba(0, 0, 0, 0.2);
    animation: dueBG 1s infinite;
  }
  
  span[left=""] {
    float: left;
  }

  span[right=""] {
    float: right;
  }
  
  gray {
    color: #666;
  }

  lgray {
    color: #aaa;
  }

  trans {
    opacity: 0.6;
  }
  @keyframes dueBG {
      0% { 
        background-color: #ff3; 
        color: #800;
      }
      50% { 
        background-color: #ffa; 
        color: #a11;
      } 
  }

  /* Objective lines */

  .codeResearch a {
    padding: 0;
    margin: 0;
  }

  name {
    display: block;
    position: relative;
    margin-bottom: 10px;
    padding-left: 10px;
    width: 98%;
    color: #444;
    letter-spacing: 2px;
    font-weight: bold;
    font-size: 2em;
    background-color: #f0f0f0;
    background-image: url('img/1.png');
    background-size: 100% 100%;
    border-radius: 30px;
  }

  name:before {
    content: "";
    display: inline-block;
    width: 15px;
    height: 15px;
    margin: 0 9px 0 15px;
    border: 2px solid black;
    background: #777;
  }

  .task-image {
  }

  description > name:before {
    margin-right: 0;
  }

  .task[done=""] > name:before, name[done=""]:before {
    background: #0f0;
    background-image: url('img/check.png');
    background-size: 100% 100%;
    color: black;
    font-size: 0.8em;
  }

  description name {
    width: 60%;
    margin-top: 4px;
    font-size: 1.4em;
    border: 2px solid transparent;
    border-color: transparent;
    transition: opacity 0.5s, border-color 0.5s;
  }

  description name:hover {
    opacity: 0.8;
    border-color: #0f0;
  }

  description name[done=""]:hover {
    opacity: 0.8;
    border-color: #bbb;
  }
  
  .task[low-priority=""] {
    background-color: #c8efff;
  }

  .task[low-priority=""] > name, name[low-priority=""], .nav-project a[low-priority=""] {
    background-color: #add8e6;
    color: darkblue;
  }
  
  .task[medium-priority=""] {
    background-color: #ffecc8;
  }
  
  .task[medium-priority=""] > name, name[medium-priority=""], .nav-project a[medium-priority=""] {
    background-color: orange;
    color: #000;
  }
  
  .task[high-priority=""] {
    background-color: #ffcac8;
  }
  
  .task[high-priority=""] > name, name[high-priority=""], .nav-project a[high-priority=""] {
    background-color: red;
    color: #fff;
  }

  .task[progress=""] > name, description name[progress=""] {
    border: 2px dotted #acaf00;
  }

  .task[progress=""], .nav-project a[progress=""] {
    background-color: #feffc5;
    box-shadow: 2px 2px 3px 1px rgba(0,0,0,0.1),
                0px 0px 7px 2px rgba(251, 255, 7, 0.4),
                inset 0px 0px 12px 2px rgba(255, 230, 160, 0.2);
    animation: progressBg 1s ease 2s infinite alternate;
  }

  @keyframes progressBg {
      0% { background-color: #feffc5; }
      100% { background-color: #ffffea; } 
  }
  .task[progress=""] > name::after, description name[progress=""]::after {
    content: " (PROGRESS)";
    font-size: 0.8em;
    opacity: 0.4;
  }

  .task[done=""] {
    background-color: #eee;
    color: #888;
  }

  .task[done=""] > name, name[done=""], .nav-project a[done=""] {
    background-color: #ddd;
    color: #888;
  }

  .task[done=""] description {
    color: #999 !important;
  }

  .hide-task {
    position: absolute;
    display: block;
    right: 4px;
    top: 4px;
    width: 12px;
    height: 12px;
    background: rgba(0, 0, 0, 0.2);
    border-radius: 3px;

    cursor: pointer;
  }

  .hide-task:hover {
    background: rgba(255, 255, 255, 0.6);
  }

  .hide-task:before {
    position: absolute;
    content: "-";
    left: 2px;
    top: -10px;
    font-size: 1.3em;
    
    width: 15px;
    height: 15px;

    color: #999;
  }

  description {
    display: block;
    clear: both;
  }

  /* Project progess bar */
  .project-progress-bar {
    position: relative;
    display: block;

    width: 97%;
    height: 30px;
    margin: 0 auto 20px;

    font-weight: bold;
    font-size: 1.2em;

    background: rgba(0, 0, 0, 0.2);

    text-shadow: 1px 1px 3px rgba(0, 0, 0, 0.2);
    color: #000;
    text-align: center;
    border: 3px groove #585;
    clear: both;
    opacity: 1;

    box-shadow: 1px 1px 3px 1px rgba(0, 0, 0, 0.1);

    transition: opacity 1s;
  }

  .project-progress-bar:hover {
    opacity: 0.5;
  }

  .project-progress-bar-bar {
    position: absolute;
    top: 0;
    left: 0;
    height: 100%;
    width: 0px;
    
    background: #0f0;
    background: linear-gradient(#0f0, #0c0);

    z-index: -10;
    transition: width 8s;

    box-shadow: inset 2px 2px 4px 2px rgba(0, 0, 0, 0.3),
                1px 0 2px 2px rgba(0, 0, 0, 0.2);
  }

  .project-complete {
    border: 3px groove #ff0;
    color: #3f3;
  }

  /* Task progess bar */
  .task-progress-bar {
    position: relative;
    display: block;

    width: 95%;
    height: 8px;
    margin: 0 auto 10px;

    font-weight: bold;
    font-size: 0.6em;
    padding: 0;
    line-height: 7px;

    background: rgba(95, 95, 95, 0.2);

    color: #000;
    letter-spacing: 4px;
    text-align: center;
    clear: both;
    opacity: 1.0;

    box-shadow: 1px 1px 3px 1px rgba(0, 0, 0, 0.1);

    transition: opacity 1s;
    overflow: hidden;
  }

  .task-progress-bar:hover {
    opacity: 0.8;
  }

  .task-progress-bar-bar {
    position: absolute;
    top: 0;
    left: 0;
    height: 100%;
    width: 0px;
    opacity: 1.0;
    
    z-index: -1;
    background: #9f9;
    background: linear-gradient(#9f9, #0f0);

    transition: width 8s;

    box-shadow: inset 2px 2px 2px 2px rgba(0, 0, 0, 0.2),
                1px 0 1px 1px rgba(0, 0, 0, 0.1);
  }

  .task-complete {
    border: 2px groove #ff0;
    color: #00f;
    box-shadow: 0 0 5px 2px rgba(255, 255, 70, 0.4),
  }

  .task {
    position: relative;
    padding: 10px;
    width: 97%;
    height: auto;
    margin: 0 auto 20px;
    background: rgba(255, 255, 255, 0.8);
    background-image: url('img/1.png');
    background-size: 100% 100%;
    border: 3px solid transparent;
    border-color: transparent;
    border-radius: 0 0 20px 20px;
    clear: both;

    box-shadow: 2px 2px 3px 1px rgba(0,0,0,0.1);

    transition: opacity 0.5s, border-color 0.5s;
  }

  .task:hover {
    opacity: 0.8;
    border-color: #bfb;
  }

  .task[done=""]:hover {
    opacity: 0.8;
    border-color: #aaa;
  }

  .task checkbox {
    display: inline;
    width: 20px;
    height: 20px;
    background: red;
    border: 1px solid black;
  }

  .project-image {

  }

  /* Misc */

  .nav-project-h1 {
    display: block;
    margin-top: 70px;
  }

  o, x {
    content: "";
    display: inline-block;
    width: 10px;
    height: 10px;
    margin: 5px 2px 0 0;
    border: 2px solid black;
    background: #777;
  }
  
  x {
    
    background: #0f0;
    background-image: url('img/check.png');
    background-size: 100% 100%;
    color: black;
    font-size: 0.8em;
  }


  .clipboard-textarea {
    width: 100%;
    max-width: 60%;
    height: 10px;
    font-size: 0.7em;
    background: rgba(0, 0, 0, 0.1);
    outline: none !important;
    border: 1px outset #eee;
    border-radius: 20px;
    padding: 5px 0 5px 15px;
    overflow: hidden;
    resize: none;
  }

  .clipboard-textarea:active {
    border: 1px inset #eee;
    background: rgba(0, 0, 0, 0.3);
  }

  .clipboard-textarea-plain {
    font-family: inherit;
    width: auto;
    height: auto;
    background: none !important;
    outline: none !important;
    border: none !important;
    overflow: hidden;
    resize: none;
  }

  #save-filter {
    position: absolute;
    display: inline-block; 
    top: 2px;
    left: 34px;
    width: 11px; 
    height: 11px; 
    padding: 2px; 
    margin-right: 5px;
    font-size: 0.3em; 
    opacity: 0.7; 
    overflow: hidden;
    resize: none;
    background: rgba(0, 0, 0, 0.2) !important;
    border: 1px outset #ddd !important;
    border-radius: 2px;

    cursor: pointer;
  }

  #save-filter:hover {
    background: rgba(200, 200, 200, 0.5) !important;
    border: 1px outset #eee !important;
  }

</style>

<script>

// In debug mode
const DEBUG_MODE = 1

// Contains all tasks of the following (suffix) status types
var taskLows = [], taskMeds = [], taskHighs = [], taskProgresses = [], taskDones = [], taskDefaults = []

// Identification for checkboxes in the header
const CB_SAVE_DEFAULT = 0,
      CB_SAVE_PROGRESS = 1,
      CB_SAVE_DONE = 2,
      CB_SAVE_LOW = 3,
      CB_SAVE_MEDIUM = 4,
      CB_SAVE_HIGH = 5,
      CB_SAVE_RIGHT_DEFAULT = 6,
      CB_SAVE_RIGHT_PROGRESS = 7,
      CB_SAVE_RIGHT_DONE = 8,
      CB_SAVE_RIGHT_LOW = 9,
      CB_SAVE_RIGHT_MEDIUM = 10,
      CB_SAVE_RIGHT_HIGH = 11

// Keyboard shortcut key codes
const KEYS = {
  Q: 81,
  W: 87,
  E: 69,
  R: 82,
  T: 84,
  Y: 89,
}

// Once the internal 'save file' updates, the clickable save box flashes. This is the set 'flash' opacity
const SAVE_NOTICE_STYLE = "0.4"

/**
 * Gets checkbox DOM object for requested checkbox order id
 * 
 * @param {Number} cbOrderId - checkbox order id (see CB_SAVE_DEFAULT ...)
 */
function getCBDOMObjectForId(cbOrderId) {
  if(cbOrderId == CB_SAVE_DEFAULT) return cbDefault
  else if(cbOrderId == CB_SAVE_PROGRESS) return cbProgress
  else if(cbOrderId == CB_SAVE_DONE) return cbDone
  else if(cbOrderId == CB_SAVE_LOW) return cbLow
  else if(cbOrderId == CB_SAVE_MEDIUM) return cbMed
  else if(cbOrderId == CB_SAVE_HIGH) return cbHigh
  else if(cbOrderId == CB_SAVE_RIGHT_DEFAULT) return cbDefaultMin
  else if(cbOrderId == CB_SAVE_RIGHT_PROGRESS) return cbProgressMin
  else if(cbOrderId == CB_SAVE_RIGHT_DONE) return cbDoneMin
  else if(cbOrderId == CB_SAVE_RIGHT_LOW) return cbLowMin
  else if(cbOrderId == CB_SAVE_RIGHT_MEDIUM ) return cbMedMin
  else if(cbOrderId == CB_SAVE_RIGHT_HIGH) return cbHighMin
  return cbLow
}

// checkbox DOM object global variables
var cbDefault;
var cbProgress;
var cbDone;
var cbLow;
var cbMed;
var cbHigh;
var cbDefaultMin;
var cbProgressMin;
var cbDoneMin;
var cbLowMin;
var cbMedMin;
var cbHighMin;

/**
 * Hide a DOM object
 * 
 * @param {String} - id of the requested DOM object to hide.
 * @returns {String} - resulting display of the display state for the requested DOM object.
 */
function hide(DOMId) {
  const obj = document.getElementById(DOMId)
  const objDisplay = obj.style.display
  if(objDisplay != 'none') {
    obj.style.display = "none"
  } else {
    obj.style.display = "block"
  }
  
  updateSavedFilters({
    id: DOMId,
    d: obj.style.display
  })

  return obj.style.display
}

/**
 * Hide a DOM object
 * 
 * @param {HTMLDOMObject} DOMObject - the requested DOM object to hide.
 */
function hideDOMObject(DOMObject) {
  const obj = DOMObject
  const objDisplay = obj.style.display
  if(objDisplay != 'none') {
    obj.style.display = "none"
  } else {
    obj.style.display = "block"
  }

  if(obj.tagName != "DESCRIPTION") {
    updateSavedFilters({
      id: DOMObject.id,
      d: obj.style.display
    })
  }
  else {
    updateSavedFilters({
      id: DOMObject.parentNode.id,
      dd: obj.style.display
    })
  }
}

/**
 * Minimize a task. Minimizing a task will remove the description from its container 
 * which reduces the required height.
 * 
 * @param {HTMLDOMObject} DOMObjectTask - the requested DOM object to minimize.
 */
function minimizeTask(DOMObjectTask) {
  const descObj = DOMObjectTask.getElementsByTagName("description")[0]
  hideDOMObject(descObj)
}

/**
 * Minimize a task and uniquely update the 'save file'
 * 
 * @param {HTMLDOMObject} DOMObjectTask - the requested DOM object to minimize.
 */
function minimizeTaskB(DOMObjectTask) {
  const descObj = DOMObjectTask.getElementsByTagName("description")[0]
  descObj.style.display = "none"
  
  updateSavedFilters({
    id: DOMObjectTask.id,
    dd: descObj.style.display
  })
}

/**
 * Maximize a task. (Show the hidden description)
 * 
 * @param {HTMLDOMObject} DOMObjectTask - the requested DOM object to mazimize.
 */
function maximizeTaskB(DOMObjectTask) {
  const descObj = DOMObjectTask.getElementsByTagName("description")[0]
  descObj.style.display = "block"
  
  updateSavedFilters({
    id: DOMObjectTask.id,
    dd: descObj.style.display
  })
}

/**
 * Copy the contents of a textarea's contents.
 * 
 * @param {HTMLDOMObject} targetElement - the requested DOM object (textarea) to copy.
 */
function clipboardCopyDiv(targetElement) {
  
  // Highlight node text
  let range = document.createRange();
  range.selectNode(targetElement);
  window.getSelection().removeAllRanges();
  window.getSelection().addRange(range);

  document.execCommand("copy")
  
}

/**
 * Copy the contents of an element's innerHTML.
 * 
 * @param {HTMLDOMObject} e - the requested DOM object to copy.
 */
function clipboardCopy(e) {
  e.select()
  document.execCommand("copy")
}

/**
 * Log a message to the top of the window (red).
 * 
 * @param {String} message - message to show
 */
function cl(message) {
    if(DEBUG_MODE > 0) {
    var sss = document.createElement("p");
    sss.style.color = "red";
    sss.innerHTML = message;
    document.getElementsByTagName("body")[0].insertBefore(sss, document.getElementsByTagName("body")[0].firstChild);
  }
}

/**
 * Log a message to the top of the window (dark-red).
 * 
 * @param {String} message - message to show
 */
function clB(message) {
    if(DEBUG_MODE > 0) {
    var sss = document.createElement("p");
    sss.style.padding = 0
    sss.style.margin = 0
    sss.style.color = "darkred";
    sss.innerHTML = message;
    document.getElementsByTagName("body")[0].insertBefore(sss, document.getElementsByTagName("body")[0].firstChild);
  }
}

/**
 * Get the CSS id from a task status id
 * 
 * @param {String} taskStatusId - Task status id to parse
 */
function getStatus(taskStatusId) {
  if(taskStatusId == "DONE") {
    return "done"
  } else if(taskStatusId == "HIGH") {
    return "high-priority"
  } else if(taskStatusId == "MEDIUM") {
    return "medium-priority"
  } else if(taskStatusId == "LOW") {
    return "low-priority"
  }
}

/**
 * Loops through all 'projects' and renders them to our output div.
 * 
 * @param {Objecct} projects - LAll projects to be rendered
 */
function renderProjects(projects) {

  const outProjects = document.getElementById("projects")
  const navOut = document.getElementById("nav-projects")

  try {

    // Projects
    for(var i = 0; i < projects.length; i++) {
      const out = document.createElement("div") 
      const progressBar = document.createElement("div") 
      const progressBarBar = document.createElement("span") 
      const spanNavProject = document.createElement("span") 
      const spanNavProjectTasks = document.createElement("span") 
      const aProjectNavigator = document.createElement("a") 
      const inputProjectHide = document.createElement("input") 
      const imgProject = document.createElement("img")
      let h1ProjectName

      const proj = projects[i]

      // Project wrapper Id (for hiding)
      out.id = proj.projectId

      // Span Nav project
      spanNavProject.className = "nav-project"

      // Append header image to main
      if(proj.projectImage != null) {

        if(proj.projectImage.src.indexOf("[id]") == -1) {
        imgProject.src = proj.projectImage.src
        } else {
          imgProject.src = "img/" + proj.projectId + proj.projectImage.src.split(" ")[1]
        }
        imgProject.src = proj.projectImage.src
        imgProject.title = proj.projectDescription
        
        if(proj.projectImage.style != null) {
          for(var k = 0; k < proj.projectImage.style.length; k++) {
            const styleAttr = proj.projectImage.style[k]
            imgProject.style[styleAttr[0]] = styleAttr[1]
          }
        }
        
        out.appendChild(imgProject)
      }
        
      // If no project image available - use h1 projectName.
      else {
        h1ProjectName = document.createElement("h1")
        h1ProjectName.className = "nav-project-h1"
        h1ProjectName.title = proj.projectDescription
        h1ProjectName.innerHTML = proj.projectName
        out.appendChild(h1ProjectName)
      }
      
      // Progress bar (directly underneath header text)
      if(proj.projectProgress != null && proj.projectProgress != -1) {
        progressBar.className = "project-progress-bar " + ((proj.projectProgress > 99) ? "project-complete" : "")
        progressBar.innerText = proj.projectProgress + "%"
        progressBarBar.className = "project-progress-bar-bar"
        setTimeout(() => progressBarBar.style.width = proj.projectProgress + "%", 2000)
        if(proj.projectProgressTitle != null) {
          progressBar.title = proj.projectProgressTitle
        }
        progressBar.appendChild(progressBarBar)
        out.appendChild(progressBar)
      }

      // Setup project navigator (main navbar click for this project)
      aProjectNavigator.title = proj.projectDescription
      aProjectNavigator.innerHTML = proj.projectName
      aProjectNavigator.href = "#" + proj.projectId

      inputProjectHide.id = proj.projectId + '-cb'
      inputProjectHide.setAttribute("type", "checkbox")
      inputProjectHide.onclick = (e) => {

        // Hide the project; update the saved filter object
        objSavedFilters[0].p[proj.projectId] = (hide(proj.projectId) == 'none') ? 0 : 1
        updateSavedFilters()

      }
      inputProjectHide.checked = true
      if(proj.projectHidden) {
        inputProjectHide.checked = false
        setTimeout(() => hide(proj.projectId), 500)
      }

      // Append new project navigator to navbar.
      spanNavProject.appendChild(inputProjectHide)
      spanNavProject.appendChild(aProjectNavigator)
      spanNavProject.appendChild(spanNavProjectTasks)
      navOut.appendChild(spanNavProject)

      // Display all tasks for this project.
      for(var j = 0; j < proj.tasks.length; j++) {
        const task = proj.tasks[j]

        const divTask = document.createElement("div")
        const taskBar = document.createElement("div") 
        const taskBarBar = document.createElement("span") 
        const nameName = document.createElement("name")
        const imgTaskImage = document.createElement("img")
        const descriptionDescription = document.createElement("description")
        const aNavTask = document.createElement("a")
        const spanTaskHide = document.createElement("span") 
        var imgNav
        
        // Create task/name/description container
        divTask.className = "task"
        divTask.id = task.taskId
        if(task.status != null && task.status.length > 0) {
          divTask.setAttribute(getStatus(task.status), "")
          aNavTask.setAttribute(getStatus(task.status), "")
        }
        if(task.inProgress && task.status != 'DONE') {
          divTask.setAttribute("progress", "")
          aNavTask.setAttribute("progress", "")
          aNavTask.style.color = "#3a3"
          if(task.status == "HIGH") {
            aNavTask.style.color = "#f33"
            aNavTask.style.borderRadius = "20px 0 20px 0" 
            aNavTask.style.borderBottom = aNavTask.style.borderTop = "1px outset red" 
          }
        }
        divTask.onclick = (event) => {
          if(event.altKey) {
            hideDOMObject(descriptionDescription)
          }
        }

        // Name
        nameName.innerHTML = task.name
        nameName.onclick = (event) => {
          if(event.ctrlKey) {
            clipboardCopyDiv(event.target)
          }
        }

        // Name image (Task image)
        if(task.taskImage != null) {
          if(task.taskImage.src.indexOf("[id]") == -1) {
          imgTaskImage.src = task.taskImage.src
          } else {
            imgTaskImage.src = "task-img/" + task.taskId + task.taskImage.src.split(" ")[1]
          }
          if(task.taskImage.style != null) {
            for(var k = 0; k < task.taskImage.style.length; k++) {
              const styleAttr = task.taskImage.style[k]
              imgTaskImage.style[styleAttr[0]] = styleAttr[1]
            }
          } else {
            for(var k = 0; k < DEFAULT_TASK_IMAGE_STYLE.length; k++) {
              const styleAttr = DEFAULT_TASK_IMAGE_STYLE[k]
              imgTaskImage.style[styleAttr[0]] = styleAttr[1]
            }
          }

          imgTaskImage.className = "task-image"
          imgTaskImage.style.float = "right"

          // Nav image
          imgNav = imgTaskImage.cloneNode()
          imgNav.className = "nav-task-image"
          imgNav.style = {}
        }

        // Nav image place-holder
        else {
          var imgNav = document.createElement("span") 
          imgNav.className = "nav-task-image gray-dot"
        }
        nameName.appendChild(imgTaskImage)
        
        // Description
        descriptionDescription.innerHTML = task.description

        // Append name 
        divTask.appendChild(nameName)
      
        // Task bar (completetion)
        if(task.taskProgress != null && task.taskProgress != -1) {
          taskBar.className = "task-progress-bar " + ((task.taskProgress > 99) ? "task-complete" : "")
          taskBar.innerText = task.taskProgress + "%"
          taskBarBar.className = "task-progress-bar-bar"
          setTimeout(() => taskBarBar.style.width = task.taskProgress + "%", 2000)
          if(task.taskProgressTitle != null) {
            taskBar.title = task.taskProgressTitle
          }
          taskBar.appendChild(taskBarBar)
          divTask.appendChild(taskBar)
        }

        // Append description
        divTask.appendChild(descriptionDescription)

        // Task hide (checkbox)
        spanTaskHide.className = "hide-task"
        spanTaskHide.onclick = (e) => hideDOMObject(descriptionDescription)
        divTask.appendChild(spanTaskHide)

        // Append task
        out.appendChild(divTask)

        // Also add task to the nav.
        aNavTask.href = "#" + task.taskId
        aNavTask.title = task.name
        aNavTask.innerHTML = task.taskName
        aNavTask.appendChild(imgNav)
        spanNavProjectTasks.appendChild(aNavTask)
      }

      // Append project to all projects
      outProjects.appendChild(out)
      
    }
  } catch(e) {

    // Display error
    cl("error");
    cl(e);
    
    // Error line #
    let auxx = unescape(e.stack)
    let aux = auxx.split(" at ")
    if(aux != null) {
      for(segment of aux) {
        clB(segment)
      }
    } 

  }
}

/**
 * Updates the view and (optionally) adds new save data to the saved obj
 * 
 * @param {Object} updatedFilter - Object to add to the save obj.
 */
function updateSavedFilters(updatedFilter) {

  const taSaveFilter = document.getElementById("save-filter")

  // View save textarea flicker effect
  if(taSaveFilter.style.opacity != SAVE_NOTICE_STYLE) {
    let taStyleTemp =  taSaveFilter.style.opacity
    taSaveFilter.style.opacity = SAVE_NOTICE_STYLE
    setTimeout(() => taSaveFilter.style.opacity = taStyleTemp, 500)
  }

  if(updatedFilter == null || updatedFilter.id == null) {
    taSaveFilter.innerHTML = generateSavedFilterString(objSavedFilters)
    return false
  }

  // Find updated save filter and update.
  // WARNING: Slows down filtering by n * n times.
  for(let i in objSavedFilters) {
    const replaceFilter = objSavedFilters[i]

    if(replaceFilter.id == updatedFilter.id) {
      //replaceFilter.id = updatedFilter.id
      if(updatedFilter.d != null) {
        replaceFilter.d = updatedFilter.d
      } 
      if(updatedFilter.dd != null) {  
        replaceFilter.dd = updatedFilter.dd
      }
      break
    }
  }

  // psued-save to textarea.
  taSaveFilter.innerHTML = generateSavedFilterString(objSavedFilters)

  return true

}

/**
 * Parse the global save object to string
 * 
 * @param {Object} filterObject - Save object
 */
function generateSavedFilterString(filterObject) {
  return JSON.stringify(filterObject)
}

/**
 * Parse a 'load file' (string) to a usable object.
 * 
 * @param {String} jsonStr - Full string to convert to an object.
 */
function generateObjFilter(jsonStr) {
  return JSON.parse(jsonStr)
}

/**
 * Cache data and apply click functionality.
 * Called 500ms AFTER the components are RENDERED.
 */
function setupUI() {

  try {

    // Retrieve DOM input objects
    cbLow = document.getElementById("low-filter")
    cbMed = document.getElementById("medium-filter")
    cbHigh = document.getElementById("high-filter")
    cbDefault = document.getElementById("default-filter")
    cbProgress = document.getElementById("progress-filter")
    cbDone = document.getElementById("done-filter")
    
    cbLowMin = document.getElementById("low-minimize")
    cbMedMin = document.getElementById("medium-minimize")
    cbHighMin = document.getElementById("high-minimize")
    cbDefaultMin = document.getElementById("default-minimize")
    cbProgressMin = document.getElementById("progress-minimize")
    cbDoneMin = document.getElementById("done-minimize")
    allTasks = document.getElementsByClassName("task")

    let loadedFilters = false

    // Saving / Loading
    if(LOAD_FILTERS) {

      if(SAVED_FILTERS != null && SAVED_FILTERS.indexOf("cb") != -1) {

        objSavedFilters = generateObjFilter(SAVED_FILTERS)
        loadedFilters = true

        // Render view from loaded filters
        cbLow.checked = Boolean(objSavedFilters[0].cb[CB_SAVE_LOW])
        cbMed.checked = Boolean(objSavedFilters[0].cb[CB_SAVE_MEDIUM])
        cbHigh.checked = Boolean(objSavedFilters[0].cb[CB_SAVE_HIGH])
        cbDefault.checked = Boolean(objSavedFilters[0].cb[CB_SAVE_DEFAULT])
        cbProgress.checked = Boolean(objSavedFilters[0].cb[CB_SAVE_PROGRESS])
        cbDone.checked = Boolean(objSavedFilters[0].cb[CB_SAVE_DONE])
        
        cbLowMin.checked = Boolean(objSavedFilters[0].cb[CB_SAVE_RIGHT_LOW])
        cbMedMin.checked = Boolean(objSavedFilters[0].cb[CB_SAVE_RIGHT_MEDIUM])
        cbHighMin.checked = Boolean(objSavedFilters[0].cb[CB_SAVE_RIGHT_HIGH])
        cbDefaultMin.checked = Boolean(objSavedFilters[0].cb[CB_SAVE_RIGHT_DEFAULT])
        cbProgressMin.checked = Boolean(objSavedFilters[0].cb[CB_SAVE_RIGHT_PROGRESS])
        cbDoneMin.checked = Boolean(objSavedFilters[0].cb[CB_SAVE_RIGHT_DONE])
        
        // Show/hide each project based on their loaded hidden state value. Also check/uncheck the box accordingly
        if(objSavedFilters[0].p != null) {
          for(project of MY_PROJECTS) {
            document.getElementById(project.projectId).style.display = ((
              document.getElementById(project.projectId + '-cb').checked = Boolean(objSavedFilters[0].p[project.projectId])
            ) == false) ? 'none' : 'block'
          }
        }

      }

    }

    // If there is NO saved object to load, set up our default 'file.'
    if(objSavedFilters == null) {

      let objProjectsVisible = {}

      for(project of MY_PROJECTS) {
        objProjectsVisible[project.projectId] = 1
      }

      objSavedFilters = [
        {
          // checkbox CHECKED data values
          cb: [1,1,1,1,1,1,1,1,1,1,1,1],

          // Set all projects to visible(1) on startup
          p: objProjectsVisible
        }
      ]
    }

    // Populate filter arrays based on .task attributes.
    for(let i = 0; i < allTasks.length; i++) {
      const task = allTasks[i]

      // Populate
      if(task.getAttribute("low-priority") != null) {
        taskLows.push(task)
      }
      else if(task.getAttribute("medium-priority") != null) {
        taskMeds.push(task)
      }
      else if(task.getAttribute("high-priority") != null) {
        taskHighs.push(task)
      }
      else if(task.getAttribute("progress") != null) {
        taskProgresses.push(task)
      }
      else if(task.getAttribute("done") != null) {
        taskDones.push(task)
      }
      else {
        taskDefaults.push(task)
      }

      // Initializing / Loading the saveFilter object.
      
      // no saved filters - create default
      if(loadedFilters == false) {

        // Setup save
        let newFilter = {
          // Task id
          id: task.id,
          // Task (div) style.display
          d: "block",
          // Task description style.display
          dd: "block"
        }
        
        objSavedFilters.push(newFilter)
      }

      // Format the View to the matching saved filter styles.
      else {

        // WARNING: Slows down filtering by n * n times.
        for(let toLoadFilter of objSavedFilters) {
          if(task.id == toLoadFilter.id) {
            task.id = toLoadFilter.id
            task.style.display = toLoadFilter.d
            task.getElementsByTagName("description")[0].style.display = toLoadFilter.dd
            break
          }
        }

      }

    } // allTask loop

    // Update save log
    updateSavedFilters()

    // Attach click functionality for hiding/showing task groups.
    cbLow.onclick = (e) => {
      for(task of taskLows) { 
        hideDOMObject(task)
      }
      objSavedFilters[0].cb[CB_SAVE_LOW] = e.target.checked ? 1 : 0
      updateSavedFilters()
    }

    cbMed.onclick = (e) => {
      for(task of taskMeds) {
        hideDOMObject(task)
      }
      objSavedFilters[0].cb[CB_SAVE_MEDIUM] = e.target.checked ? 1 : 0
      updateSavedFilters()
    }

    cbHigh.onclick = (e) => {
      for(task of taskHighs) {
        hideDOMObject(task)
      }
      objSavedFilters[0].cb[CB_SAVE_HIGH] = e.target.checked ? 1 : 0
      updateSavedFilters()
    }

    cbDone.onclick = (e) => {
      for(task of taskDones) {
        hideDOMObject(task)
      }
      objSavedFilters[0].cb[CB_SAVE_DONE] = e.target.checked ? 1 : 0
      updateSavedFilters()
    }

    cbProgress.onclick = (e) => {
      for(task of taskProgresses) {
        hideDOMObject(task)
      }
      objSavedFilters[0].cb[CB_SAVE_PROGRESS] = e.target.checked ? 1 : 0
      updateSavedFilters()
    }

    cbDefault.onclick = function(e) {
      for(task of taskDefaults) {
        hideDOMObject(task)
      }
      objSavedFilters[0].cb[CB_SAVE_DEFAULT] = e.target.checked ? 1 : 0
      updateSavedFilters()
    }
    
    // Attach click functionality for hiding/showing task descriptions.
    cbLowMin.onclick = (e) => { 
      for(task of taskLows) {
        e.target.checked ? maximizeTaskB(task) : minimizeTaskB(task)
      }
      objSavedFilters[0].cb[CB_SAVE_RIGHT_LOW] = e.target.checked ? 1 : 0
      updateSavedFilters()
    }

    cbMedMin.onclick = (e) => {
      for(task of taskMeds) {
        e.target.checked ? maximizeTaskB(task) : minimizeTaskB(task)
      }
      objSavedFilters[0].cb[CB_SAVE_RIGHT_MEDIUM] = e.target.checked ? 1 : 0
      updateSavedFilters()
    }

    cbHighMin.onclick = (e) => {
      for(task of taskHighs) {
        e.target.checked ? maximizeTaskB(task) : minimizeTaskB(task)
      }
      objSavedFilters[0].cb[CB_SAVE_RIGHT_HIGH] = e.target.checked ? 1 : 0
      updateSavedFilters()
    }

    cbDoneMin.onclick = (e) => {
      for(task of taskDones) {
        e.target.checked ? maximizeTaskB(task) : minimizeTaskB(task)
      }
      objSavedFilters[0].cb[CB_SAVE_RIGHT_DONE] = e.target.checked ? 1 : 0
      updateSavedFilters()
    }

    cbProgressMin.onclick = (e) => {
      for(task of taskProgresses) {
        e.target.checked ? maximizeTaskB(task) : minimizeTaskB(task)
      }
      objSavedFilters[0].cb[CB_SAVE_RIGHT_PROGRESS] = e.target.checked ? 1 : 0
      updateSavedFilters()
    }

    cbDefaultMin.onclick = function(e) {
      for(task of taskDefaults) {
        e.target.checked ? maximizeTaskB(task) : minimizeTaskB(task)
      }
      objSavedFilters[0].cb[CB_SAVE_RIGHT_DEFAULT] = e.target.checked ? 1 : 0
      updateSavedFilters()
    }

  } catch(e) {

    // Error
    let auxx = unescape(e.stack)
    let aux = auxx.split("at")
    if(aux != null) {
      for(segment of aux) {
        clB(segment)
      }
    }


    cl("setupUI error");
    cl(e);
  }
}
/*

    cbLow = document.getElementById("low-filter")
    cbMed = document.getElementById("medium-filter")
    cbHigh = document.getElementById("high-filter")
    cbDefault = document.getElementById("default-filter")
    cbProgress = document.getElementById("progress-filter")
    cbDone = document.getElementById("done-filter")
    
    cbLowMin = document.getElementById("low-minimize")
    cbMedMin = document.getElementById("medium-minimize")
    cbHighMin = document.getElementById("high-minimize")
    cbDefaultMin = document.getElementById("default-minimize")
    cbProgressMin = document.getElementById("progress-minimize")
    cbDoneMin = document.getElementById("done-minimize")
    allTasks = document.getElementsByClassName("task")

*/


/**
 * Handle keyboard input for show/hide tasks.
 * 
 * @param {Number} inputId - Key input id number
 */
function keyboardShortcut(inputId) {

  var getCBForLetter = {
    "Q": getCBDOMObjectForId(6),
    "W": getCBDOMObjectForId(7),
    "E": getCBDOMObjectForId(8),
    "R": getCBDOMObjectForId(9),
    "T": getCBDOMObjectForId(10),
    "Y": getCBDOMObjectForId(11),
  }

  let clickTarget, cbId;

  if(typeof inputId == "number" && inputId < 7) {
    clickTarget = getCBDOMObjectForId(inputId)
    clickTarget.onclick({target:clickTarget})
    clickTarget.checked = !clickTarget.checked
  } 
  else if(typeof inputId === "string" && inputId.length == 1) {
    clickTarget = getCBForLetter[inputId]
    clickTarget.checked = !clickTarget.checked
    clickTarget.onclick({target:clickTarget})
  }
}

/**
 * Handle key releasing.
 * 
 * @param {KeyEvent} keyEvent - Key event object
 */
function keyUpHandler(keyEvent) {
  
  // 1 - 6
  if(keyEvent.keyCode > 48 && keyEvent.keyCode < 55) {
    keyboardShortcut(keyEvent.keyCode - 49)
  } 
  
  else if(keyEvent.keyCode == 81) { // Q
    keyboardShortcut('Q')
  } else if(keyEvent.keyCode == 87) { // W
    keyboardShortcut('W')
  } else if(keyEvent.keyCode == 69) { // E
    keyboardShortcut('E')
  } else if(keyEvent.keyCode == 82) { // R
    keyboardShortcut('R')
  } else if(keyEvent.keyCode == 84) { // T
    keyboardShortcut('T')
  } else if(keyEvent.keyCode == 89) { // Y
    keyboardShortcut('Y')
  }
}

/**
 * Add our listeners.
 */
function initListeners() {
  window.addEventListener("keyup", keyUpHandler)
}

/**
 * Initialize our projects. This function is responsible for: adding all projects 
 * to the view, adding listeners and attaching click events to the UI.
 */
function init() {

  setTimeout( () => {
    scrollTo(0,0)
    setupUI()
  }, 500);
  
  renderProjects(MY_PROJECTS)

  initListeners()

}

// Attach all projects and tasks to the view.
init()

</script>