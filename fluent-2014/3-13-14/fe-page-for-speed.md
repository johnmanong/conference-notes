# Designing for Front-End Page Speed (4:15pm)
## Lara Swanson (Etsy)
### [slides] (laraswanson.com/design)

# intro
- web performance is user experience
- users expect 2 seconds
- after 3 seconds, 40% will abandon your site
- case studies
  - etsy: 160kb to a page -> +12% bounce rate
  - doubleclick: client side redirect -> +12% click through rate
- design does not usually consider performance
- performance + beauty = user experience

# what are we optimizing for?
- web page test
- number of requests
- size of requests
- image formatting
- cutting down font weights
- semantic markup
- deliberate asset loading

## image formating
- images are majority of content bytes
- png
  - few colors (256 colors for PNG-8)
  - transparency
  - PNG-8, PNG-24
- jpg
  - lots of colors
  - photos
  - 80-90% quality is usually ok
  - **ImageOptim** for lossless compression
- gifs
  - heavy
  - animations can be used in css
- 26 thumbnails vs spriting
  - spriting increased page size
  - but decreased page load time
- questions
  - compressed? 
  - colors?
  - transparency?
  - sprite it?
- if amazon compressed images, 20% less energy to load page

## css3
- can elminate resource request
- transisions
- gradients
- css geometry daily (tumblr)
- can affect ui/ux if overused

## fonts
- IE6-8 downloads all the fonts
- only @import font weights you need
- optimize charater subsetting (only chars you need)
- ajax in a stylesheet with new font
  - what font weights do I need?
  - can any weights be combined/consolidated?
  - remove chars?

## semantics and repurposability
- clean ur code
- create repurposable code
- rename non-semantic elements
  - e.g. .blue = bad, .tags = (good)
- remove inefficient selectors
  - e.g. heavily nested
- remove unneeded elements (divtitis)
- questions
  - design pattern?
  - semantic markup?
  - can someone else use this?

## responsive
- mobile only internet usage
  - 25% in the US
- mobile performance is terrible
  - desktop wifi rtt < 50ms
  - mobile rtt ~300ms (dialup!)

### mobile first workflow
- what is core purpose?
- deliberate about loading assets
- conditional loading
  - RESS: RWD with server side detection
  - [adaptive images](adaptive-images.com)
- lazy loading
- 3rd party scripts
  - always asynchronous
- picture fill
  - [github](https://github.com/scottjehl/picturefill)

### who is responsible for performance?
- no more performance cops or janitors
  - not sustainable
  - everyone's responsible
  - culture of performance
- how did etsy change culture
- performance reports
  - get comfortable with transparency
  - forced iteration and improve
- page load times are not private

### questions 
- how many asesets am I loading?
- what can be repurposed?
- measure impacts!
- good performance is good design