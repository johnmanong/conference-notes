# keynote with Paul Irish (9:10am)

# Delivering the goods
## minimizing page load time and finally answering the page size vs # of requests

## page optimization
-[an engineer's guide to optimization]
  - id area which will change business needle
  - ...
  - what is speed limit
  - approach limit

- what does performance mean to user
- example: twitter
  - page load at 2.4s (nothing on page)
  - activity finished at ~8s
  - The Speed Index
- not about dom ready or page load, its about pixels on the page

## number of requests vs page size
- correlation to speed index does not differentiate between these
- asked Ilya
  - want to be in good health
  - how do you optimize food intake
  - how often do you eat and how much
  - no one would measure a diet this way
  - not all requests, bytes are eual

## bandwidth and latency
- gains diminish at higher bandwidth
- latency has a much more linear relationship
- latency bounds web browsing
- bw bounds streaming media

### tcp
- intitial handshake to open connection
- *tcp slow start*
  - ramps up size of payload
  - 4 >> 8 >> 16 >>32
  - RTT much slower on mobile
  - dns lookup + handshake + content
- tcp optimized for large data stream
- tcp bottleneck is latency

### critical path
- reddit on mobile, duck feeding the fishes
- webpage test on imgur
  - filmstrip view to view how network requests affect what user sees
  - image url isn't in initial html payload
  - make api request for it
  - also blocked by head loading
  - can also create Timeline (chrome dev tools)
- what is critical in css
  - can inline critical css
  - get the rest later
- eliminate any render-clocking js
  - load all async
- minimize render-blocking css
  - inline vs stylesheet
- deliver the goods
  - no redirect for html
  - gzip

- wrapping up
  - pagespeed insights is totally sweet
  - want a really fast mobile page load
    - first 14 kb request should have everything
  - max 200 ms of server response
  - speed index under 1000