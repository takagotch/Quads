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

def weighted_average(hist):
  total = sum(hist)
  value = sum() / total
  error = sum(x * (value - i) ** 2 for i, x in enumerate(hist)) / total
  












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
  
  
  
  
  def render():
    m = OUTPUT_SCALE
    dx, dy = ()
    im = ImageDraw.Draw()
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


