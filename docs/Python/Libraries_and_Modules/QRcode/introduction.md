![QRCode](images/QRCode.png){: .center}

This is a library that help us to generate a QR Code

1. [pypi](https://pypi.org/project/qrcode/#description)
2. [Github](https://github.com/lincolnloop/python-qrcode)

## Installation

```Bash
pip install qrcode
```

## Usage

There are several ways to generate the QR codes:

* Command Line.
* Basic Use.
* Advance Use.

### Commands

The simple way to generate the code will be using command line.

```Bash
qr "some text" > test.png
```

### Basic Use

we can use a short code `make`:

```python
import qrcode
img = qrcode.make("some data here")
```

### Advance Use

We can we more control if we use the `QRCode` Class

```python
import qrcode

qr = qrcode.QRCode(
	version=1,
	error_correction=qrcode.constants.ERROR_CORRECT_L,
	box_size=10,
	border=4,)
qr.add_data('same data')
qr.make(fit=True)

img = qr.make_image(fill_color="black", back_color="white")
```

Now from the code we have:

1. `version` it is a integer from 1 to 40 it control the sizes smallest been the version 1, or a matrix $21X21$, we can set it to `None` and later use `fit` parameter to determine the size automatically.
2. `fill_color` and `back_color` it can change the color of the background and the painting color of the QR.
3.  `box_size` controls how many pixels each "box" of the QR Code is.
4. `border` Controls how many boxes thick the border should be ( default 4, which is the maximum).

#### `error_correction`

This parameter control the error correction use for the QR Code, it has four possible constant values:

* `ERROR_CORRECT_L`: 7% or less errors can be corrected.
* `ERROR_CORRECT_M`: (*default*) 15% or less errors can be corrected.
* `ERROR_CORRECT_Q`: 25% or less error can be corrected.
* `ERROR_CORRECT_H`: 30% or less error can be corrected.
