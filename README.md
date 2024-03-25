
# Installation and Setup related <br>
  `pip install requirements.txt`
# Directory structure:
```
|--  root_directory-> must be on python path
|    |-- data
|    |   |-- 300W_landmarks_train.csv
|    |   |-- WFLW_landmarks_test.csv
|    |   |-- WFLW_landmarks_train.csv
|    |-- images (references)
|    |   |-- 300W_image_annotation_style.jpg (Ref: https://ibug.doc.ic.ac.uk/resources/300-W/)
|    |   |-- pydevd_plugin_plugin_name.py (Ref: https://wywu.github.io/projects/LAB/WFLW.html)
|    |-- output
|    |   |-- 300W_landmarks_test.csv (Ans to Q1)
|    |   |-- WFLW_normalized_landmarks_test.csv (Ans to Q2)
|    |-- plots (representative)
|    |   |-- WFLW-test-translate-rotate-scale-for-4-faces.png 
|    |   |-- WFLW-test-vs-300W-test-face-plot-for-5-faces.png
|    |-- Facial Landmarking.ipynb (Completes all the code with all the illustrations)
|    |-- Final_notebook.pdf (Pdf version of the final notebook)
```
# Summary:
* Please check `Facial Landmarking.ipynb` : it contains step-wise elaboration
* Using `numpy` and `pandas`, we investigate the data and perform vectorized operations. Using `matplotlib`, our plots show the meaning of our results.
* The first part of the problem asks us to transfer the annotations from `WFLW` (98-point annotation system) to `300W` (68-point annotation systems) for images with same face-ids and create a `csv` file. We make observations with localized representative points (of areas such as eyes etc.) and create a mapping function, which is then used to create `300W` test dataset. Please check `output/300W_landmarks_test.csv`. We make references to appropriate sources in the notebook, which provides complete detail to this solution. The plot to this part is at `images/WFLW-test-vs-300W-test-face-plot-for-5-faces.png`
* The second part of the problem asks us for WFLW test dataset specifically. Here, we perform three operations in succession: translation, rotation and scaling. At each step, we make sure that the 98-point system becomes invariant to these operations.
* To achieve this, for translation, we localize the set of points around their centroid, which makes them robust against translation.
* For rotation, we fix the first point as the source and calculate its relative rotation angle (or slope) with respect to x-axis. Then evaluating using this rotation angle, we obtain the rotation_matrix (using the negative of this angle to undo the rotation) which when applied to all sets of points makes the system invariant to rotations. Mathematical details are provided in the notebook.
* For scaling, we normalize the points with the magnitude or norm of the vectors from origin, essentially making them unit vectors which is scaling-invariant.
* We finally apply these operations in succession to the annotated dataset and store the result in `output/WFLW_normalized_landmarks_test.csv`. The graphical plot to this part is at `images/WFLW-test-vs-300W-test-face-plot-for-5-faces.png`.
# Citations:
<a id="1">[1]</a> 
Wu, Wayne and Qian, Chen and Yang, Shuo and Wang, Quan and Cai, Yici and Zhou, Qiang (2018). 
Look at Boundary: A Boundary-Aware Face Alignment Algorithm.
CVPR.
<br>
<a id="2">[2]</a>
Goodall, Colin. “Procrustes Methods in the Statistical Analysis of Shape.” Journal of the Royal Statistical Society. Series B (Methodological), vol. 53, no. 2, 1991, pp. 285–339. JSTOR, http://www.jstor.org/stable/2345744.
<br>
<a id="3">[3]</a>
Christos Sagonas, Epameinondas Antonakos, Georgios Tzimiropoulos, Stefanos Zafeiriou, Maja Pantic,
300 Faces In-The-Wild Challenge: database and results,
Image and Vision Computing,
Volume 47,
2016,
Pages 3-18,
ISSN 0262-8856,
https://doi.org/10.1016/j.imavis.2016.01.002.
(https://www.sciencedirect.com/science/article/pii/S0262885616000147)

