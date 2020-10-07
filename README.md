# EXTRACT DICE SCORE
Extracts the score from blue and red dices from a given image, also it outputs the score for each dice separately.
Function **'extract_dice_score'** returns 2 numbers that represent the sum of numbers on blue and red dices.<br />
Function **'extract_dice_score_bonus'** returns the score for each dice separately.

# IMPLEMENTATION
**Extraction of the scores on the blue and red dices:**<br />
The images are converted from RGB to HSV color format, because the idea is to use the saturation channel to extract blue and red dots from the background and to use hue channel to distinguish between red and blue dots. 
Setting the saturation threshold to 0.5 the image is binarized and the blue and red dots are extracted:<br />
![img1](https://github.com/Digital-Image-Processing-kosta/Extract-dice-score-from-image/blob/master/garbage/9.png)<br />
To remove the blue and red dots on the sides, morphological operation of openning is performed. Then morphological operation of erosion is performed to separte the segments:<br />
![img2](https://github.com/Digital-Image-Processing-kosta/Extract-dice-score-from-image/blob/master/garbage/10.png)<br />
By counting the connected objects on the resulting image the sum of the scores on the blue and red dices is extracted.<br />
Setting the threshold for the hue channel to 0.93 red segments are extracted from the orignal image:
![img3](https://github.com/Digital-Image-Processing-kosta/Extract-dice-score-from-image/blob/master/garbage/11.png)<br />
As before, same morphological operations of openning and erosion are applied:<br />
![img4](https://github.com/Digital-Image-Processing-kosta/Extract-dice-score-from-image/blob/master/garbage/12.png)<br />
By counting the number of connected objects, the score of the red dices is calculated. Subtracting that score from the sum of the scores on the blue and red dices we get the score of the blue dices.<br />
**Extraction of the scores on each dice separately:**
Same segmentation steps are applied as before and now we have 2 binarized images. First image contains blue and red segments and the second contains only red segments. The following algorithm is applied on both images:<br />
Using the function *regionprops* we extract the position of the centroids for each connected segment. Each centroid initially gets unique integer starting from 1. That number represents the number of the dice that centroid belongs to. We iterate thorugh all of the centroids and if the distance between 2 centroids is relatively small (threshold distance is hyperparameter), second centroid gets the integer number of the dice of the first centroid. Now resulting centroids that belong to the same dice have the same integer number. By summing the same integer numbers we get the score on each dice separately.<br />
By applying this algorithm on the second image we get the scores of the red dices and by applying it to the first image we get scores of the red and blue dices. Excluding the scores which appear in the red dices from the joint scores we get the scores on the blue dices.




# TEST: 
Run the **main.py** to test the functions on 12 images.

# NOTE: 
Hyperparameters are tuned for Matlab 2017.
