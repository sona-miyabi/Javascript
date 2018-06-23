### SVG
svg虽是html5的范畴, 但js同样可以对其进行操作.


#### svg矢量图画布
```html
<svg
  width=400
  height=300
></svg>
```

#### rect, circle, ellipse, line, polyline, polygon, path
```html
<svg>
  <rect
    x=10 y=10
    rx=0 ry=0
    width=40 height=30
    stroke-width="2" stroke="#000" fill="transparent" />
  <circle
    cx=25 cy=75  r=10
    stroke-width="2" stroke="#0f0" fill="transparent" />
  <ellipse
    cx=75 cy=75
    rx=20 ry=5
    stroke-width="2" stroke="#00f" fill="transparent" />
  <line
    x1=10 y1=60
    x2=90 y1=60
    stroke-width="2" stroke="#00f" fill="transparent" />
  <polyline points="60 110 65 120 70 115 75 130 80 125 85 140 90 135 95 150 100 145"
    stroke-width="2" stroke="#00f" fill="transparent" />
  <polygon points="50 160 55 180 70 180 60 190 65 205 50 195 35 205 40 190 30 180 45 180"
    stroke-width="2" stroke="#00f" fill="transparent" />
  <path d="20,230 Q40,205 50,230 T90,230"
    stroke-width="2" stroke="#00f" fill="transparent" />
</svg>
```
##### rect 矩形
attr|desc
-|-
x|矩形左上角的x位置
y|矩形左上角的y位置
width|矩形的宽度
height|矩形的高度
rx|圆角的x方位的半径
ry|圆角的y方位的半径
##### circle 圆形
attr|desc
-|-
r|圆的半径
cx|圆心的x位置
cy|圆心的y位置
