# simonguest.com

TBD

## Generating banners for post articles

```
ffmpeg -i main.webp -vf "eq=brightness=-0.2:contrast=0.9,boxblur=4:1" banner.webp
```