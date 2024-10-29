## Problem description

Consider a picture representing a white sheet of A4 paper with some handwritten numbers in a dark color (they have
different sizes, but they are all oriented in the same direction, which is aligned with one of the edges of the paper).
Consider the attached pictures as examples. Some are easy, others are harder. Note that the paper might be pictured at
an angle or from a slanted perspective. In all pictures the four edges of the paper are clearly visible, but might be
incomplete.

Write a notebook that, given a directory, will process all images in that directory and extract all digits it can find
from each picture. For each file, it should then print:

- the name of the file, followed by

- each of the digits that has been identified on that sheet of paper, from top to bottom.

## Suggested approach

One possible approach is the following:

- Load the image and resize it to a manageable size. You may want to convert it to grayscale.

- Look for edges using the Canny edge detector.

- Look for four long straight lines using the Hough line detector.

- The intersections between pairs of these lines should correspond to the corners of the paper sheet.
  (note: 4 lines define 6 different intersections!)

- Once you have the four corners of the sheet, you can obtain a straightened version of your sheet of paper, by a
  geometric transformation.

- Binarize and find connected components (this might be tricky when illumination is uneven. How to fix that?).

- Cut a square bounding box around each connected component.

- Resize that to a 28x28 and classify it using a convnet trained on the MNIST dataset.

## Some useful functions

To resize an image:
skimage.transform.resize(image, output_shape)

The notebooks in this section help in finding the intersection point of two lines, and rectifying the image of sheet of
paper.

To download a large dataset of handwritten digits, which can be used to train a classifier:

from keras.datasets import mnist
(x_train, y_train), (x_test, y_test) = mnist.load_data()

## Rules and expectations

The task is difficult and comprises several sub-tasks. You are not expected to implement a solution that works always
perfectly.

The main goal is to implement a simple straightforward solution for each sub-task, then identify and discuss its
weaknesses. When does it work? When does it fail? How could we make it better?

A forum is created on moodle to freely discuss these issues, brainstorm improvements, and exchange ideas about their
implementation; the instructor takes part in the discussion and can provide suggestions.

## Submission and grading

Submission is compulsory.

Submit through moodle an HTML or PDF file of your notebook implementing your solution and describing your approach.
Before saving, reset the kernel and run the entire notebook. Use markdown cells to describe what your code does, and
illustrate intermediate results.

The activity is not graded; however, the final exam might contain questions that are related to the solution of the
assignment. The submission is compulsory. Submit your solution on time, even if it is incomplete.