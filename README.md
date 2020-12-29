## Bitcoin BoToF Score

Welcome to the Bitcoin BoToF score page !
BoTof is the acronyme of Bottom and Top Finder and the Bitcoin BoToF Score is a metric built from different market value, onchain and sentiment indicators. These indicators are well known for roughly finding Bitcoin's tops and bottoms. BoToF score aims to combine them to find the exact tops and bottoms, nothing less !

## Actual BTC BoToF Score 

<canvas id="foo"></canvas>

## Buy and sell signals 



## Used Indicators 



## Historical BoToF Scores 

Under construction

<script src="dist/gauge.js"></script>

<script type="text/javascript">
  var opts = {
  angle: -0.2, // The span of the gauge arc
  lineWidth: 0.2, // The line thickness
  radiusScale: 1, // Relative radius
  pointer: {
    length: 0.6, // // Relative to gauge radius
    strokeWidth: 0.035, // The thickness
    color: '#000000' // Fill color
  },
  limitMax: false,     // If false, max value increases automatically if value > maxValue
  limitMin: false,     // If true, the min value of the gauge will be fixed
  colorStart: '#6FADCF',   // Colors
  colorStop: '#8FC0DA',    // just experiment with them
  strokeColor: '#E0E0E0',  // to see which ones work best for you
  generateGradient: true,
  highDpiSupport: true,     // High resolution support
  
};
var target = document.getElementById('foo'); // your canvas element
var gauge = new Gauge(target).setOptions(opts); // create sexy gauge!
gauge.maxValue = 100; // set max gauge value
gauge.setMinValue(0);  // Prefer setter over gauge.minValue = 0
gauge.animationSpeed = 32; // set animation speed (32 is default value)
gauge.set(50); // set actual value

staticZones: [
   {strokeStyle: "#F03E3E", min: 100, max: 130}, // Red from 100 to 130
   {strokeStyle: "#FFDD00", min: 130, max: 150}, // Yellow
   {strokeStyle: "#30B32D", min: 150, max: 220}, // Green
   {strokeStyle: "#FFDD00", min: 220, max: 260}, // Yellow
   {strokeStyle: "#F03E3E", min: 260, max: 300}  // Red
],
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
