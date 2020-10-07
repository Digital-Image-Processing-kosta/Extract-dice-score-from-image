# EXTRACT DICE SCORE
Extracts the score from blue and red dices from a given image, also it outputs the score for each dice separately.
Function **'extract_dice_score'** returns 2 numbers that represent the sum of numbers on blue and red dices.<br />
Function **'extract_dice_score_bonus'** returns the score for each dice separately.

# IMPLEMENTATION
The images are converted from RGB to HSV color format, because the idea is to use the saturation channel to extract blue and red dots from the background and to use hue channel to distinguish between red and blue dots. 
Setting the saturation threshold to 0.5 the image is binarized and the blue and red dots are extracted:<br />
![img1](https://github.com/Digital-Image-Processing-kosta/Extract-dice-score-from-image/blob/master/garbage/9.png)<br />
To remove the blue and red dots on the sides, morphological operation of openning is performed. Then morphological operation of erosion is performed to separte the segments:<br />
![img2](https://github.com/Digital-Image-Processing-kosta/Extract-dice-score-from-image/blob/master/garbage/10.png)<br />
By counting the connected objects on the resulting image the sum of the score on the blue and red dices is extracted.<br />
Setting the threshold for the hue channel to 0.93 red segments are extracted from the orignal image:
![img3](https://github.com/Digital-Image-Processing-kosta/Extract-dice-score-from-image/blob/master/garbage/11.png)<br />
As before, same morphological operations of openning and erosion are applied:<br />
![img4](https://github.com/Digital-Image-Processing-kosta/Extract-dice-score-from-image/blob/master/garbage/12.png)<br />



# TEST: 
Run the **main.py** to test the functions on 12 images.

# NOTE: 
Hyperparameters are tuned for Matlab 2017.
