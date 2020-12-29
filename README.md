## Bitcoin BoToF Score

Welcome to the Bitcoin BoToF score page !
BoTof is the acronyme of Bottom and Top Finder and the Bitcoin BoToF Score is a metric built from different market value, onchain and sentiment indicators. These indicators are well known for roughly finding Bitcoin's tops and bottoms. BoToF score aims to combine them to find the exact tops and bottoms, nothing less !

## Actual BTC BoToF Score 

  <div id="preview">
  	<canvas width=400 height=200 id="canvas-preview"></canvas>
  	<div id="preview-textfield"></div>
  </div>

## Buy and sell signals 



## Used Indicators 



## Historical BoToF Scores 

Under construction

<script src="dist/gauge.js"></script>

<script type="text/javascript">
  prettyPrint();

  $('#divisionsCbx').click(function(){
    $('.subDivisions').toggle();
    $('#subDivisions').toggle();
    fdSlider.redrawAll();
  })

  function update() {
    var opts = {};
    var tmp_opts = opts;
    tmp_opts.renderTicks = {};

    if ($('.subDivisions:visible').length) {
    $('.renderTicks').each(function() {
      var val = $(this).hasClass("color") ? this.value : parseFloat(this.value);
      if($(this).hasClass("color")){
        val = "#" + val;
      }
      if (this.name.indexOf("divLength") != -1 ||
      this.name.indexOf("subLength") != -1) {
        val /= 100;
      }
      if (this.name.indexOf("divWidth") != -1 ||
      this.name.indexOf("subWidth") != -1) {
        val /= 10;
      }

      $('#opt-' + this.name.replace(".", "-")).text(val);

      if(this.name.indexOf(".") != -1){
      	var elems = this.name.split(".");

      	for (var i=0; i < elems.length - 1; i++) {
      		if (!(elems[i] in tmp_opts)) {
      			tmp_opts.renderTicks[elems[i]] = {};
      		}
      		tmp_opts = tmp_opts.renderTicks[elems[i]];
      	}
      	tmp_opts.renderTicks[elems[elems.length - 1]] = val;
      } else if ($(this).hasClass("color")) {
        // color picker is removing # from color values
      	opts.renderTicks[this.name] = "#" + this.value
        $('#opt-' + this.name.replace(".", "-")).text("#" + this.value);
      } else {
      	opts.renderTicks[this.name] = val;
      }
    });
  }


    $('.opts input[min], .opts .color').not('.renderTicks').each(function() {
      var val = $(this).hasClass("color") ? this.value : parseFloat(this.value);
      if($(this).hasClass("color")){
        val = "#" + val;
      }
      if(this.name.indexOf("lineWidth") != -1 ||
        this.name.indexOf("radiusScale") != -1 ||
        this.name.indexOf("angle") != -1 ||

        this.name.indexOf("pointer.length") != -1){
        val /= 100;
      }else if(this.name.indexOf("pointer.strokeWidth") != -1){
        val /= 1000;
      }
      $('#opt-' + this.name.replace(".", "-")).text(val);
      if(this.name.indexOf(".") != -1){
      	var elems = this.name.split(".");
      	var tmp_opts = opts;
      	for(var i=0; i<elems.length - 1; i++){
      		if(!(elems[i] in tmp_opts)){
      			tmp_opts[elems[i]] = {};
      		}
      		tmp_opts = tmp_opts[elems[i]];
      	}
      	tmp_opts[elems[elems.length - 1]] = val;
      }else if($(this).hasClass("color")){
        // color picker is removing # from color values
      	opts[this.name] = "#" + this.value
        $('#opt-' + this.name.replace(".", "-")).text("#" + this.value);
      }else{
      	opts[this.name] = val;
      }
      if(this.name == "currval"){
      	// update current demo gauge
      	demoGauge.set(parseInt(this.value));
      	AnimationUpdater.run();
      }
    });
    $('#opts input:checkbox').each(function() {
      opts[this.name] = this.checked;
      $('#opt-' + this.name).text(this.checked);
    });
    demoGauge.animationSpeed = opts.animationSpeed;
    opts.generateGradient = true;
    console.log(opts);
    demoGauge.setOptions(opts);
    demoGauge.ctx.clearRect(0, 0, demoGauge.ctx.canvas.width, demoGauge.ctx.canvas.height);
    demoGauge.render();
    if ($('#share').is(':checked')) {
      window.location.replace('#?' + $('form').serialize());
    }

  }
  function initGauge(){
    document.getElementById("class-code-name").innerHTML = "Gauge";
    demoGauge = new Gauge(document.getElementById("canvas-preview"));
    demoGauge.setTextField(document.getElementById("preview-textfield"));
    demoGauge.maxValue = 3000;
    demoGauge.set(1244);
  };
  function initDonut(){
    document.getElementById("class-code-name").innerHTML = "Donut";
    demoGauge = new Donut(document.getElementById("canvas-preview"));
    demoGauge.setTextField(document.getElementById("preview-textfield"));
    demoGauge.maxValue = 3000;
    demoGauge.set(1244);
  };
  function initZones(){
    document.getElementById("class-code-name").innerHTML = "Gauge";
    demoGauge = new Gauge(document.getElementById("canvas-preview"));
    var opts = {
      angle: -0.25,
      lineWidth: 0.2,
      radiusScale:0.9,
      pointer: {
        length: 0.6,
        strokeWidth: 0.05,
        color: '#000000'
      },
      staticLabels: {
        font: "10px sans-serif",
        labels: [200, 500, 2100, 2800],
        fractionDigits: 0
      },
      staticZones: [
         {strokeStyle: "#F03E3E", min: 0, max: 200},
         {strokeStyle: "#FFDD00", min: 200, max: 500},
         {strokeStyle: "#30B32D", min: 500, max: 2100},
         {strokeStyle: "#FFDD00", min: 2100, max: 2800},
         {strokeStyle: "#F03E3E", min: 2800, max: 3000}
      ],
      limitMax: false,
      limitMin: false,
      highDpiSupport: true
    };
    demoGauge.setOptions(opts);
    demoGauge.setTextField(document.getElementById("preview-textfield"));
    demoGauge.minValue = 0;
    demoGauge.maxValue = 3000;
    demoGauge.set(1244);
  };
  function initNew(){
    document.getElementById("class-code-name").innerHTML = "Gauge";
    demoGauge = new Gauge(document.getElementById("canvas-preview"));
    var bigFont = "14px sans-serif";
    var opts = {
      angle: 0.1,
      radiusScale:0.9,
      lineWidth: 0.2,
      pointer: {
        length: 0.6,
        strokeWidth: 0.05,
        color: '#000000'
      },
      staticLabels: {
        font: "10px sans-serif",
        labels: [{label:200, font: bigFont}, 
        {label:750}, 
        {label:1500}, 
        {label:2250}, 
        {label:3000}, 
        {label:3500, font: bigFont}],
        fractionDigits: 0
      },
      staticZones: [
        {strokeStyle: "rgb(255,0,0)", min: 0, max: 500, height: 1.2},
        {strokeStyle: "rgb(200,100,0)", min: 500, max: 1000, height: 1.1},
        {strokeStyle: "rgb(150,150,0)", min: 1000, max: 1500, height: 1},
        {strokeStyle: "rgb(100,200,0)", min: 1500, max: 2000, height: 0.9},
        {strokeStyle: "rgb(0,255,0)", min: 2000, max: 3100, height: 0.8},
        {strokeStyle: "rgb(80,255,80)", min: 3100, max: 3500, height: 0.7},
        {strokeStyle: "rgb(130,130,130)", min: 2470, max: 2530, height: 1}        
      ],
      limitMax: false,
      limitMin: false,
      highDpiSupport: true
    };
    demoGauge.setOptions(opts);
    document.getElementById("preview-textfield").className = "preview-textfield"; 
    demoGauge.setTextField(document.getElementById("preview-textfield"));
    demoGauge.minValue = 0;
    demoGauge.maxValue = 3500;
    demoGauge.set(2122);
  };
  $(function() {
    var params = {};
    var hash = /^#\?(.*)/.exec(location.hash);
    if (hash) {
      $('#share').prop('checked', true);
      $.each(hash[1].split(/&/), function(i, pair) {
        var kv = pair.split(/=/);
        params[kv[0]] = kv[kv.length-1];
      });
    }
    $('.opts input[min], #opts .color').each(function() {
      var val = params[this.name];
      if (val !== undefined) this.value = val;
      this.onchange = update;
    });
    $('.opts input[name=currval]').mouseup(function(){
    	AnimationUpdater.run();
    });

    $('.opts input:checkbox').each(function() {
      this.checked = !!params[this.name];
      this.onclick = update;
    });
    $('#share').click(function() {
      window.location.replace(this.checked ? '#?' + $('form').serialize() : '#!');
    });

    $("#type-select li").click(function(){
    	$("#type-select li").removeClass("active")
    	$(this).addClass("active");
    	var type = $(this).attr("type");
    	if(type=="donut") {
          initDonut();
          $("input[name=lineWidth]").val(10);
          $("input[name=fontSize]").val(24);
          $("input[name=angle]").val(35);
          $("#preview-textfield").removeClass("reset");
          $("input[name=colorStart]").val("6F6EA0")[0].color.importColor();
          $("input[name=colorStop]").val("C0C0DB")[0].color.importColor();
          $("input[name=strokeColor]").val("EEEEEE")[0].color.importColor();

          fdSlider.disable('input-ptr-len');
          fdSlider.disable('input-ptr-stroke');
          $("#input-ptr-color").prop('disabled', true);

          selectGaguge1.set(1);
          selectGaguge2.set(3000);
          selectGauge3.set(1);
          selectGauge4.set(1);
          
        } else if (type=="zones") {
          initZones();
          fdSlider.disable('input-ptr-len');
          fdSlider.disable('input-ptr-stroke');
          $("#preview-textfield").removeClass("reset").addClass("reset");
          $("input[name=angle]").val(-20);
          $("input[name=lineWidth]").val(20);

          fdSlider.enable('input-ptr-len');
          fdSlider.enable('input-ptr-stroke');
          $("input[name=colorStart]").prop('disabled', true);
          $("input[name=colorStop]").prop('disabled', true);
          $("input[name=strokeColor]").prop('disabled', true);

          $("input[name=colorStop]").prop('disabled', true);
          $("input[name=strokeColor]").prop('disabled', true);

          selectGaguge1.set(1);
          selectGaguge2.set(1);
          selectGauge3.set(3000);
          selectGauge4.set(1);
          
      } else if (type=="new") {
        initNew();
        $("input[name=lineWidth]").val(30);
    		$("input[name=fontSize]").val(41);
        $("input[name=angle]").val(10);
        $("#preview-textfield").removeClass("reset").addClass("reset");
        selectGaguge1.set(1);
        selectGaguge2.set(1);
        selectGauge3.set(1);
        selectGauge4.set(2213);
      } else{
    		initGauge();
    		$("input[name=lineWidth]").val(44);
    		$("input[name=fontSize]").val(41);
        $("input[name=angle]").val(15);
        $("#preview-textfield").removeClass("reset").addClass("reset");
        

    		$("input[name=colorStart]").val("6FADCF")[0].color.importColor();
    		$("input[name=colorStop]").val("8FC0DA")[0].color.importColor();
    		$("input[name=strokeColor]").val("E0E0E0")[0].color.importColor();

    		fdSlider.enable('input-ptr-len');
    		fdSlider.enable('input-ptr-stroke');
            $("#input-ptr-color").prop('disabled', false);
            selectGaguge1.set(3000);
            selectGaguge2.set(1) ;
            selectGauge3.set(1);
            selectGauge4.set(1);
    	}
    	//fdSlider.updateSlider('input-line-width');
    	fdSlider.updateSlider('input-font-size');
    	fdSlider.updateSlider('input-angle');
    	$("#example").removeClass("donut, gauge").addClass(type);
    	update();
    });

    selectGaguge1 = new Gauge(document.getElementById("select-1"));
    selectGaguge1.maxValue = 3000;
    selectGaguge1.set(1552);

    selectGauge4 = new Gauge(document.getElementById("select-4"));
    var opts2 = {
      angle: 0.1,
      lineWidth: 0.2,
      pointer: {
        length: 0.5,
        strokeWidth: 0.05,
        color: '#000000'
      },
      staticZones: [
         {strokeStyle: "#F03E3E", min: 0, max: 500, height: 2},
         {strokeStyle: "#FFDD00", min: 500, max: 1000, height: 1.5},
         {strokeStyle: "#30B32D", min: 1000, max: 1500, height: 1},
         {strokeStyle: "#FFDD00", min: 1500, max: 2000, height: 0.7},
         {strokeStyle: "#F03E3E", min: 2000, max: 3000, height: 0.3}
      ],
      limitMax: false,
      limitMin: false,
      highDpiSupport: true
    };
    selectGauge4.minValue = 0;
    selectGauge4.maxValue = 3000;
    selectGauge4.setOptions(opts2);
    selectGauge4.set(2122);

    selectGaguge2 = new Donut(document.getElementById("select-2"));
    selectGaguge2.maxValue = 3000;
    selectGaguge2.set(1844);

    selectGauge3 = new Gauge(document.getElementById("select-3"));
    var opts = {
      angle: -0.25,
      lineWidth: 0.2,
      pointer: {
        length: 0.6,
        strokeWidth: 0.05,
        color: '#000000'
      },
      staticZones: [
         {strokeStyle: "#F03E3E", min: 0, max: 200},
         {strokeStyle: "#FFDD00", min: 200, max: 500},
         {strokeStyle: "#30B32D", min: 500, max: 2100},
         {strokeStyle: "#FFDD00", min: 2100, max: 2800},
         {strokeStyle: "#F03E3E", min: 2800, max: 3000}
      ],
      limitMax: false,
      limitMin: false,
      strokeColor: '#E0E0E0',
      highDpiSupport: true
    };
    selectGauge3.minValue = 0;
    selectGauge3.maxValue = 3000;
    selectGauge3.setOptions(opts);
    selectGauge3.set(1607);

    initGauge();
    update();

  });
</script>
<script type="text/javascript">

  var _gaq = _gaq || [];
  _gaq.push(['_setAccount', 'UA-11790841-11']);
  _gaq.push(['_trackPageview']);

  (function() {
    var ga = document.createElement('script'); ga.type = 'text/javascript'; ga.async = true;
    ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'http://www') + '.google-analytics.com/ga.js';
    var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ga, s);
  })();

</script>


## Delete this !

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/botof-score/botof-score.github.io/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
