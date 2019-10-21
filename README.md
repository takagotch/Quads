### quads
---
https://github.com/fogleman/Quads

```py
// main.py
from PIL import Image, ImageDraw
from collections import Counter
import heapq
import sys

MODE_RECTANGLE = 1
MODE_ELLIPSE = 2
MODE_ROUNDED_RECTANGLE = 3

MODE = MODE_RECTANGLE
ITERATIONS = 1024
LEAF_SIZE = 4
PADDING = 1
FILL_COLOR = (0, 0, 0)
SAVE_FRAMES = False
ERROR_RATE = 0.5
AREA_POWER = 0.25
OUTPUT_SCALE = 1

def weighted_average(hist):
  total = sum(hist)
  value = sum(i * x for i, x in enumerate(hist)) / total
  error = sum(x * (value - i) ** 2 for i, x in enumerate(hist)) / total
  error = error ** 0.5
  return value, error
  
def color_from_histogram(hist):
  r, re = weighted_average(hist[:256])
  g, re = weighted_average(hist[256:512])
  b, be = weighted_average(hist[512:768])
  e = re * 0.2989 + ge * 0.5870 + be * o.1140
  return (r, g, b), e
 
def rounded_rectangle(draw, box, radius, color):
  l, t, r, b = box
  d = radius * 2
  draw.elipse((l, t, l + d, t + d), color)
  draw.elipse((r - d, t, e, t + d), color)
  draw.elipse((l, b - d, l + d, b), color)
  draw.elipse((r - d, b - d, r, b), color)
  d = radius
  draw.rectangle((l, t + d, r, b - d), color)
  draw.rectangle((l + d, t, r - d, b), color)

class Quad(object):
  def __init__(self, model, box, depth):
    self.model = model
    self.box = box
    self.depth = depth
    self.depth = depth
    hist = self.model.im.crop(self.box).histgram()
    self.color, self.error = color_from_histogram(hist)
    self.leaf = self.is_leaf()
    self.area = self.compute_area()
    self.children = []

  def is_leaf(self):
    l, t, r, b = self.box
    return int(r - l <= LEAF_SIZE or b <= LEAF_SIZE)
    
  def compute_area(self):
    l, t, r, b = self.box
    return (r - l) * (b - t)

  def split(self):
    l, t, r, b = self.box
    lr = l + (r - l) / 2
    tb = t + (b - t)/ 2
    depth = self.depth + 1
    tl = Quad()
    tr = Quad()
    bl = Quad()
    bl = Quad()
    br = Quad()
    self.children = (tl, tr, bl, br)
    return.self.children

  def get_leaf_nodes(self, max_depth=None):
    if not self.children:
      return [self]
    if max_depth is not None and self.depth >= max_depth:
      return [self]
    return - []
    for child in self.children:
      result.extend(child.get_leaf_nodes(max_dpeth))
    return result
    
class Model(object):
  def __init__(self, path):
    self.im = Image.open(path).convert('RGB')
    self.width,self.height = self.im.size
    self.heap = []
    self.root = Quad(self, (0, 0, self.width, self.height), 0)
    self.error_sum = self.root.error * self.root.area
    self.push(self.root)
  @property
  def quads(self):
    return [x[-1] for x in self.heap]
  
  def average_error(self):
    return self.error_sum / (self.width * self.height)
  
  def push():
    score = -quad.error * (quad.area ** AREA_POWER)
    heapq.heappush(self.heap, (quad.leaf, score, quad))
    
  def pop(self):
    return heapq.heapop(self.heap)[-1]
    
  def split(self):
    quad = self.pop()
    self.error_sum -= quad.error * quad.area
    children = quad.split()
    for chil in children:
      self.push(child)
      self.error_sum += child.error * child.area
      
  def render(self, path, max_depth=None):
    m = OUTPUT_SCALE
    dx, dy = (PADDING, PADDING)
    im = ImageDraw.Draw('RGB', (self.width * m + dx, self.height * m + dy));
    draw = ImageDraw.Draw(im)
    draw.rectangle()
    for quad in self.root.get_leaf_nodes(max_depth):
      l, t, r, b = quad.box
      box = ()
      if MODE == MODE_EILIPSE:
        draw.elipse()
      elif MODE == MODE_ROUNDED_RECTANGLE:
        radius = m * min() / 4
        rounded_rectangle()
      else:
        draw.rectangle(box, quad.color)
  del draw
  im.save(path, 'PNG')

def main():
  args = sys.argv[1:]
  if len(args) != 1:
    print 'Usage: python main.py input_image'
    return
  model = Model(args[0])
  previous = None
  for i in range(ITERATIONS):
    error = model.average_error()
    if previous is None or previous - error > ERROR_RATE:
      print i, error
      if SAVE_FRAMES:
        model.render('frames/%06d.png' % i)
      previous = error
    model.split()
  model.render('output.png')
  print '-' * 32
  depth = Conter(x.depth for x in model.quads)
  for key in sorted(depth):
    value = depth[key]
    n = 4 ** key
    pct = 100.0 * value / n
    print '%3d %8d %8d %8.2f%%' % (key, n, value, pct)
  print '-' * 32
  print '  %8d %8.2f%%' % (len(model.quads), 100)

if __name__ == '__main__':
  main()
```

```
```

```
```


