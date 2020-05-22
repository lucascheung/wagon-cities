# redux-boilerplate

Simple React + Redux starter with the following config:

- React, ReactDOM
- Redux, React-Redux
- Webpack 3
- Babel with es2015 and react presets
- Bootstrap (css only, loaded from a cdn in `index.html`)
- work with `.js` or `.jsx` files
- main `application.scss` stylesheet is imported in `index.js` as a module to enjoy hot reloading

<style type="text/css" media="screen">
html,
body {
  overflow: hidden;
  width: 100%;
  padding: 0;
}

body {
  background: #ececec;
}

#p {
  position: absolute;
  width: 100%;
  padding-left: 20px;

  font-family: "Raleway", sans-serif;
  font-size: 52px;
  text-align: center;

  opacity: 0;

  animation-duration: 1.3s;
  animation-delay: 1550ms;
}
</style>
<p id="p" class="animated bounceIn">Get well soon Matt!</p>
class Heart extends mojs.CustomShape {
  getShape () {
    return '<path d="M73.6170213,0 C64.4680851,0 56.5957447,5.53191489 51.7021277,13.8297872 C50.8510638,15.3191489 48.9361702,15.3191489 48.0851064,13.8297872 C43.4042553,5.53191489 35.3191489,0 26.1702128,0 C11.9148936,0 0,14.0425532 0,31.2765957 C0,48.0851064 14.893617,77.8723404 47.6595745,99.3617021 C49.1489362,100.212766 50.8510638,100.212766 52.1276596,99.3617021 C83.8297872,78.5106383 99.787234,48.2978723 99.787234,31.2765957 C100,14.0425532 88.0851064,0 73.6170213,0 L73.6170213,0 Z"></path>';
  }
}
mojs.addShape( 'heart', Heart );

const CIRCLE_RADIUS = 200;
const RADIUS = 230;
const HEART_RADIUS = 140;
const HEART_SIZE = 300;

const circle = new mojs.Shape({
  left:         0,
  top:          0,
  stroke:       '#FF9C00',
  strokeWidth:  { [2*CIRCLE_RADIUS] : 0 },
  fill:         'none',
  scale:        { 0: 1 },
  radius:       CIRCLE_RADIUS,
  duration:     400,
  easing:       'cubic.out'
});

const burst = new mojs.Burst({
  left: 0, top: 0,
  radius:   { 4: RADIUS },
  angle:    45,
  count:    12,
  timeline: { delay: 300 },
  children: {
    radius:       2.5,
    fill:         '#FD7932',
    scale:        { 1: 0, easing: 'quad.in' },
    pathScale:    [ .8, null ],
    degreeShift:  [ 13, null ],
    duration:     [ 500, 700 ],
    easing:       mojs.easing.bezier(0.1, 1, 0.3, 1)
  }
});

const heart = new mojs.Shape({
  left: 0, top: 2,
  shape:    'heart',
  fill:     '#E5214A',
  scale:    { 0 : 1 },
  easing:   'elastic.out',
  duration: 1600,
  delay:    300,
  radius:   HEART_RADIUS
});

setTimeout(function() {
  const text = document.getElementById("p");
  const coords = { x: animationPosX(), y: animationPosY() };
  
  text.style.top = (documentHeight() / 5 * 3) + "px";
  
  burst
    .tune(coords)
    .replay();
  
  circle
    .tune(coords)
    .replay();
  
  heart
    .tune(coords)
    .replay();
}, 1500);

function animationPosX()
{
  return (documentWidth() / 2) + "px";
}

function animationPosY()
{
  return (documentHeight() / 3) + "px";
}

function documentHeight()
{
  const body = document.body,
        html = document.documentElement;

  const height = Math.max(body.scrollHeight, body.offsetHeight, 
                         html.clientHeight, html.scrollHeight, html.offsetHeight);
  
  return height;
}

function documentWidth()
{
  const body = document.body,
        html = document.documentElement;

  const height = Math.max(body.scrollWidth, body.offsetWidth, 
                         html.clientWidth, html.scrollWidth, html.offsetWidth);
  
  return height;
}
