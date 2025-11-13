# Teachable Machine → micro:bit (4 classes)

이 저장소는 Teachable Machine 이미지 분류 모델을 웹브라우저에서 실행하고,
분류 결과(0/1/2/3)를 Web Serial API를 통해 micro:bit로 전송하는 데모입니다.

## 사용 방법 (GitHub Pages)

1. 이 저장소를 GitHub에 업로드합니다.
2. **Settings → Pages**에서 Branch를 `main`, 폴더를 `/root`로 지정합니다.
3. 배포가 완료되면 `https://사용자명.github.io/저장소명` 으로 접속합니다.

## micro:bit 쪽 코드 (예시, MicroPython)

```python
from microbit import *
import micropython
micropython.kbd_intr(-1)

uart.init(baudrate=115200)
display.show(Image.ASLEEP)

ICON0 = Image.NO
ICON1 = Image.SQUARE_SMALL
ICON2 = Image.SQUARE
ICON3 = Image.DIAMOND

def show_icon(code):
    if code == '0':
        display.show(ICON0)
    elif code == '1':
        display.show(ICON1)
    elif code == '2':
        display.show(ICON2)
    elif code == '3':
        display.show(ICON3)

while True:
    if uart.any():
        b = uart.read(1)
        if not b:
            continue
        try:
            ch = b.decode('utf-8','ignore')
        except:
            continue
        if ch in ('0','1','2','3'):
            show_icon(ch)
    else:
        sleep(5)
```

## 브라우저 요구사항

- Chrome 또는 Edge 최신 버전
- HTTPS(또는 localhost) 환경
- Web Serial API 지원 브라우저
