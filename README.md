## Solves Bombcrypto newest captcha
 This project has been discontinued since the game removed the captcha.
 
![Working example](https://i.imgur.com/2AqbIJO.gif)
A very compact implementation using just cv2 and ctypes, ready to be deployed to your own project.

### How does it work

It takes multiple pictures (cropped to a smaller area) whilst moving the mouse in a sweep movement throughout the screen.

The small pictures are joined together using bitwise or operation within the image:

![bitwise or image](https://i.imgur.com/yHlipeX.png)

A HSV filter is applied to isolate the contrast

![hsv image](https://i.imgur.com/i1c4Jlf.png)

The red portion its masked with a band pass filter

![filtered image](https://i.imgur.com/lx6YGcP.png)

And finally the noise is reduced by applying mathematical morphology

![morph image](https://i.imgur.com/dgTGPTG.png)

The image is compared withing a preset of numbered images in a very shallow OCR attempt.

This will result in a numbered string with the number ordered.

### Sliding

The slider is located with template matching and by using a small variation to avoid detection, it moves the slider towards the right while comparing the appeared numbers with the puzzle number.

Once found the slider is let go, completing the captcha.

### Usage

Clone this repository into a folder
While in the directory, using Python 3.9 (suggested), do the following in the terminal:

`python -m pip install -r requeriments.txt`

This will install the used libraries.

The program will try to find windows with Bombcrypto within its name, focus on the window and locate the captcha.
If you have multiple windows with Bombcrypto name that ain't the game, the bot probably won't do its thing.

You can run the CaptchaSolver by running:

`python captchaSolver.py`

### Importing to your project

You probably will have a way of targeting the window, if so, you can remove the code that targets the windows and the functions it uses (most of ctypes functions)

You will need to specify the area in which your game is running, for performance purpose by creating the following dict:
```python
m = {
    'left': X,
    'top': Y,
    'width': width,
    'height': height
}
```

to receive the full image from the captcha:

```python
img = sweepScreen(m)
```

using the image to get the code, hsvOcr is the folder name containing the hsv numbered images
```python
number = numberOcr(img, "hsvOcr")
```

this will solve the captcha by comparing with the number found
```python
slideAndDrop(m,number)
```

### Donations

If you liked the project, consider donating to the following address:

`0x07CdF7E94C637298315F134ebB02309896349Ad4`
