# Section 9: Classifiers (Lec 9.1 - Lec 9.6)

+ [Launching Wbe page](https://courses.edx.org/courses/course-v1:BerkeleyX+Data8.3x+2T2018/courseware/03a357f8203f4dfa8aa471e06b75affe/474dec3c53d64133aa87a260efa7347f/1?activate_block_id=block-v1%3ABerkeleyX%2BData8.3x%2B2T2018%2Btype%40vertical%2Bblock%401caeb79118e34ca39fe5447986857d4a)
+ [Web notebook](https://hub.data8x.berkeley.edu/user/37b80bfacc52ea5dfdad124579807188/notebooks/materials-x18/lec/x18/3/lec9.ipynb)
+ [Local Notebook](./notebooks/lec9.ipynb)
+ [Local Python Code](./notebooks/lec09.py)

## Lec 9.1 Terminology

### Note

+ Training a Classifier
    <a href="https://courses.edx.org/courses/course-v1:BerkeleyX+Data8.3x+2T2018/courseware/03a357f8203f4dfa8aa471e06b75affe/474dec3c53d64133aa87a260efa7347f/1?activate_block_id=block-v1%3ABerkeleyX%2BData8.3x%2B2T2018%2Btype%40vertical%2Bblock%401caeb79118e34ca39fe5447986857d4a">
        <br/><img src="diagrams/lec9-1.png" alt="Flow of Classifier Training" title= "Classifier Training" width="450">
    </a>
    + Classifier: a method predicting something about that example, the class of the example, or the label of the example
    + Usually class = label
    + Attributes: characteristics of the example
    + Classification rule depends on what patterns or associations might be found in that population
    + Training set to form classification rule while test set to evaluate the accuracy of the classifier


+ Nearest Neighbor Classifier
    <a href="https://courses.edx.org/courses/course-v1:BerkeleyX+Data8.3x+2T2018/courseware/03a357f8203f4dfa8aa471e06b75affe/474dec3c53d64133aa87a260efa7347f/1?activate_block_id=block-v1%3ABerkeleyX%2BData8.3x%2B2T2018%2Btype%40vertical%2Bblock%401caeb79118e34ca39fe5447986857d4a">
        <br/><img src="diagrams/lec9-2.png" alt="text" title= "caption" width="450">
    </a>


### Video

<a href="https://edx-video.net/BERD83FD2018-V003100_DTH.mp4" alt="Lec 9.1 Terminology" target="_blank">
    <img src="http://files.softicons.com/download/system-icons/windows-8-metro-invert-icons-by-dakirby309/png/64x64/Folders%20&%20OS/My%20Videos.png" alt="Video" width="60px"> 
</a>


## Lec 9.2 Dataset

### Note

+ The Google Science Fair
  + Brittany Wenger, a 17-year-old high school student in 2012
  + Won by building a breast cancer classifier with 99% accuracy

+ Demo
    ```python
    patients = Table.read_table('breast-cancer.csv').drop('ID')
    # Clump     Uniformity of  Uniformity of  Marginal  Single Epithelial  Bare    Bland      Normal    Mitoses  Class
    # Thickness Cell Size      Cell Shape     Adhesion  Cell Size          Nuclei  Chromatin  Nucleoli
    # 5         1              1              1         2                  1       3          1         1         0
    # 5         4              4              5         7                  10      3          2         1         0
    # ... (rows omitted)

    patients.scatter('Bland Chromatin', 'Single Epithelial Cell Size', colors='Class')

    def randomize_column(a):
        return a + np.random.normal(0.0, 0.09, size=len(a))

    # adding random noise to visualize the overlaps on the same spot
    jittered = Table().with_columns([
            'Bland Chromatin (jittered)', 
            randomize_column(patients.column('Bland Chromatin')),
            'Single Epithelial Cell Size (jittered)', 
            randomize_column(patients.column('Single Epithelial Cell Size')),
            'Class',
            patients.column('Class')
        ])

    jittered.scatter('Bland Chromatin (jittered)', 'Single Epithelial Cell Size (jittered)', colors='Class')
    ```

### Video

<a href="https://edx-video.net/BERD83FD2018-V003200_DTH.mp4" alt="Lec 9.2 Dataset" target="_blank">
    <img src="http://files.softicons.com/download/system-icons/windows-8-metro-invert-icons-by-dakirby309/png/64x64/Folders%20&%20OS/My%20Videos.png" alt="Video" width="60px"> 
</a>


## Lec 9.3 Distance

### Note

+ Rows of Tables <br/>
  Each row contains all the data for one individual
  + `t.row(i)` evaluates to $ith$ row of table `t`
  + `t.row(i).item(j)` is the value of column `j` in row `i`
  + If all values are numbers, then `np.array(t.row(i))` evaluates to an array of all the numbers in the row.
  + To consider each row individually, use
    ```python
    for row in t.rows:
        ... row.item(j) ...
    ```

+ Distance Between Two Points
  + Two attributes x and y:

    $$D = \sqrt{(x_0 - x_1)^2 + (y_0 - y_1^2)} $$

  + Three attributes x, y, and z:

    $$ D = \sqrt{(x_0 - x_1)^2 + (y_0 - y_1^2) + (z_0 - z_1)^2} $$
  + and so on ...

+ Demo
    ```python
    Table().with_columns(['X', [0, 2, 3], 'Y', [0, 2, 4]]).scatter('X', 'Y')

    def distance(pt1, pt2):
        """Return the distance between two points (represented as arrays)"""
        return np.sqrt(sum((pt1 - pt2) ** 2))

    def row_distance(row1, row2):
        """Return the distance between two numerical rows of a table"""
        return distance(np.array(row1), np.array(row2))

    attributes = patients.drop('Class')

    row_distance(attributes.row(0), attributes.row(1))      # 11.874342087037917
    row_distance(attributes.row(0), attributes.row(2))      # 2.23606797749979
    row_distance(attributes.row(0), attributes.row(0))      # 0.0
    ```

### Video

<a href="https://edx-video.net/BERD83FD2018-V003300_DTH.mp4" alt="Lec 9.3 Distance" target="_blank">
    <img src="http://files.softicons.com/download/system-icons/windows-8-metro-invert-icons-by-dakirby309/png/64x64/Folders%20&%20OS/My%20Videos.png" alt="Video" width="60px"> 
</a>


## Lec 9.4 Nearest Neighbors

### Note


+ Finding the $k$ Nearest Neighbors <br/>
  To find the $$ nearest neighbors of an example:
  + Find the distance between the example and each example in the training set
  + Augment the training data table with a column containing all the distances
  + Sort the augmented table in increasing order of the distances
  + Take the top $k$ rows of the sorted table


+ The Classifier <br/>
  To classify a point:
  + Find its $k$ nearest neighbors
  + Take a majority vote of the $k$ nearest neighbors to see which of the two classes appears more often
  + Assign the point the class that wins the majority vote


+ Demo
    ```python
    def distances(training, example):
        """Compute a table with the training set and distances to the example for each row in the training set."""
        dists = []
        attributes = training.drop('Class')
        for row in attributes.rows:
            dist = row_distance(row, example)
            dists.append(dist)
        return training.with_column('Distance', dists)

    def closest(training, example, k):
        """Return a table of the k closest neighbors to example"""
        return distances(training, example).sort('Distance').take(np.arange(k))

    patients.take(12)
    # Clump     Uniformity of  Uniformity of  Marginal  Single Epithelial  Bare    Bland      Normal    Mitoses  Class
    # Thickness Cell Size      Cell Shape     Adhesion  Cell Size          Nuclei  Chromatin  Nucleoli
    # 5         3               3               3       2                   3       4           4       1           1

    example = patients.drop('Class').row(12)
    # Row(Clump Thickness=5, Uniformity of Cell Size=3, Uniformity of Cell Shape=3, Marginal Adhesion=3, Single Epithelial Cell Size=2, Bare Nuclei=3, Bland Chromatin=4, Normal Nucleoli=4, Mitoses=1)

    closest(patients, example, 5)
    # Clump     Uniformity of  Uniformity of  Marginal  Single Epithelial  Bare    Bland      Normal    Mitoses  Class  Distance
    # Thickness Cell Size      Cell Shape     Adhesion  Cell Size          Nuclei  Chromatin  Nucleoli
    # 5         3               3               3       2                   3       4           4       1         1     0
    # 5         3               3               4       2                   4       3           4       1         1     1.73205
    # 5         1               3               3       2                   2       2           3       1         0     3.16228
    # 5         2               2               2       2                   2       3           2       2         0     3.16228
    # 5         3               3               1       3                   3       3           3       3         1     3.31662

    closest(patients.exclude(12), example, 5)
    # Clump     Uniformity of  Uniformity of  Marginal  Single Epithelial  Bare    Bland      Normal    Mitoses  Class  Distance
    # Thickness Cell Size      Cell Shape     Adhesion  Cell Size          Nuclei  Chromatin  Nucleoli
    # 5         3               3               4       2                   4       3           4       1           1   1.73205
    # 5         1               3               3       2                   2       2           3       1           0   3.16228
    # 5         2               2               2       2                   2       3           2       2           0   3.16228
    # 5         3               3               1       3                   3       3           3       3           1   3.31662
    # 4         3               3               1       2                   1       3           3       1           0   3.31662

    def majority_class(neighbors):
        """Return the class that's most common among all these neighbors."""
        return neighbors.group('Class').sort('count', descending=True).column('Class').item(0)

    def classify(training, example, k):
        "Return the majority class among the k nearest neighbors."
        nearest_neighbors = closest(training, example, k)
        return majority_class(nearest_neighbors)

    classify(patients.exclude(12), example, 5)      # 0
    ```

### Video

<a href="https://edx-video.net/BERD83FD2018-V003400_DTH.mp4" alt="Lec 9.4 Nearest Neighbors" target="_blank">
    <img src="http://files.softicons.com/download/system-icons/windows-8-metro-invert-icons-by-dakirby309/png/64x64/Folders%20&%20OS/My%20Videos.png" alt="Video" width="60px"> 
</a>


## Lec 9.5 Evaluation

### Note


+ Accuracy of a Classifier
  + The accuracy of a classifier on a labeled data set is the proportion of examples that are labeled correctly 
  + Need to compare classifier predictions to true labels
  + If the labeled data set is sampled at random from a population, then we can infer accuracy on that population


+ Demo
    ```python
    patients.num_rows       # 683

    shuffled = patients.sample(with_replacement=False) # Randomly permute the rows
    training_set = shuffled.take(np.arange(342))
    test_set  = shuffled.take(np.arange(342, 683))

    def evaluate_accuracy(training, test, k):
        test_attributes = test.drop('Class')
        num_correct = 0
        for i in np.arange(test.num_rows):
            # Run the classifier on the ith patient in the test set
            test_patient = test_attributes.row(i)
            c = classify(training, test_patient, k)
            # Was the classifier's prediction correct?
            if c == test.column('Class').item(i):
                num_correct = num_correct + 1
        return num_correct / test.num_rows

    evaluate_accuracy(training_set, test_set, 5)        # 0.9736070381231672
    evaluate_accuracy(training_set, test_set, 1)        # 0.9648093841642229
    evaluate_accuracy(training_set, training_set, 1)    # 1.0 -> bias
    ```

### Video

<a href="https://edx-video.net/BERD83FD2018-V003600_DTH.mp4" alt="Lec 9.5 Evaluation" target="_blank">
    <img src="http://files.softicons.com/download/system-icons/windows-8-metro-invert-icons-by-dakirby309/png/64x64/Folders%20&%20OS/My%20Videos.png" alt="Video" width="60px"> 
</a>


## Lec 9.6 Decision Boundaries

### Note

+ Decision Boundaries
    + A change in input attributes might change the prediction
    + Inputs that are very close but result in different predicted labels are on wither side of a __decision boundary__
    + To visualize, plot predictions of a regular set of inputs

+ Demo
    ```python
    ckd = Table.read_table('ckd.csv').relabeled('Blood Glucose Random', 'Glucose')


    kidney = ckd.select('Hemoglobin', 'Glucose', 'Class')
    kidney.scatter('Hemoglobin', 'Glucose', colors=2)
    plots.scatter(13, 250, color='red', s=30);

    def show_closest(t, point):
        """Show closest training example to a point."""
        near = closest(t, point, 1).row(0)
        t.scatter(0, 1, colors='Class')
        plots.scatter(point.item(0), point.item(1), color='red', s=30)
        plots.plot([point.item(0), near.item(0)], [point.item(1), near.item(1)], color='k', lw=2)
        
    show_closest(kidney, make_array(13, 250))

    def standard_units(any_numbers):
        """Convert any array of numbers to standard units."""
        return (any_numbers - np.mean(any_numbers)) / np.std(any_numbers)

    def standardize(t):
        """Return a table in which all columns of t are converted to standard units."""
        t_su = Table()
        for label in t.labels:
            t_su = t_su.with_column(label + ' (su)', standard_units(t.column(label)))
        return t_su

    kidney_su = standardize(kidney.drop('Class')).with_column('Class', kidney.column('Class'))
    show_closest(kidney_su, make_array(-0.2, 1.8))
    show_closest(kidney_su, make_array(-0.2, 1.3))
    show_closest(kidney_su, make_array(-0.2, 1))
    show_closest(kidney_su, make_array(-0.2, 0.9))

    def decision_boundary(t, k):
        """Decision boundary of a two-column + Class table."""
        t_su = standardize(t.drop('Class')).with_column('Class', t.column('Class'))
        decisions = Table(t_su.labels)
        for x in np.arange(-2, 2.1, 0.1):
            for y in np.arange(-2, 2.1, 0.1):
                predicted = classify(t_su, make_array(x, y), k)
                decisions.append([x, y, predicted])
        decisions.scatter(0, 1, colors='Class', alpha=0.4)
        plots.xlim(-2, 2)
        plots.ylim(-2, 2)
        t_su_0 = t_su.where('Class', 0)
        t_su_1 = t_su.where('Class', 1)
        plots.scatter(t_su_0.column(0), t_su_0.column(1), c='darkblue', edgecolor='k')
        plots.scatter(t_su_1.column(0), t_su_1.column(1), c='gold', edgecolor='k')
        
    decision_boundary(kidney, 1)
    decision_boundary(kidney, 5)
    decision_boundary(jittered, 1)
    decision_boundary(jittered, 5)
    ```

### Video

<a href="https://edx-video.net/BERD83FD2018-V003500_DTH.mp4" alt="Lec 9.6 Decision Boundaries" target="_blank">
    <img src="http://files.softicons.com/download/system-icons/windows-8-metro-invert-icons-by-dakirby309/png/64x64/Folders%20&%20OS/My%20Videos.png" alt="Video" width="60px"> 
</a>


## Reading and Practice

### Reading

This guide assumes that you have watched the videos for Section 9.

This corresponds to textbook sections:

[Chapter 17.1: Nearest Neighbors](https://www.inferentialthinking.com/chapters/17/1/Nearest_Neighbors)

[Chapter 17.2: Training and Testing](https://www.inferentialthinking.com/chapters/17/2/Training_and_Testing)

[Chapter 17.3: Rows of Tables](https://www.inferentialthinking.com/chapters/17/3/Rows_of_Tables)

[Chapter 17.4: Implementing the Classifier](https://www.inferentialthinking.com/chapters/17/4/Implementing_the_Classifier)

[Chapter 17.5: The Accuracy of the Classifier](https://www.inferentialthinking.com/chapters/17/5/Accuracy_of_the_Classifier)

In section 9, we learned how to create our own k-nearest neighbor classifier. We solidified our understanding of nearest neighbor classification, saw the difference between training and testing our model, and learned metrics used for evaluating our model.

Visualizations and decision boundaries are important in understanding how a k-nearest neighbor classifier works.

Let's try the following practice problems.


### Practice

Are the following statements true or false?

Q1. In k-nearest neighbors classification, increasing the value of k will always improve accuracy on the test set.

    Ans: False


Q2. In k-nearest neighbors classification, increasing the value of k can never improve accuracy on the test set.

    Ans: False


Q3. In nearest neighbors classification, the test set should be selected to include some data points from the training set and some data points that aren't in the training set.

Ans: False


We want to predict whether a watermelon is a seedless (class 0) or seeded (class 1) variety, based on two attributes: length and circumference. We have a training set of 9 examples and a test set with 2 examples, as shown in the plot below. No two watermelons have the same length and circumference.

<a href="https://courses.edx.org/courses/course-v1:BerkeleyX+Data8.3x+2T2018/courseware/03a357f8203f4dfa8aa471e06b75affe/56296378689f4329bde00d75bb4f0428/?child=first">
    <img src="https://prod-edxapp.edx-cdn.org/assets/courseware/v1/1084add53bf965490320f3247c7672c0/asset-v1:BerkeleyX+Data8.3x+2T2018+type@asset+block/watermelon.png" alt="Practice Question 4~9" title= "Watermelon" width="450">
</a>

Q4. The first watermelon in the test set has circumference 90 cm and length 40 cm. What class will a 1-nearest neighbor classifier predict for this watermelon?

    a. Class 0: Seedless
    b. Class 1: Seeded

    Ans: a


Q5. What class will a 3-nearest neighbors classifier predict for the same watermelon?

    a. Class 0: Seedless
    b. Class 1: Seeded

    Ans: b


Q6 What class will a 5-nearest neighbors classifier predict for the same watermelon?

    a. Class 0: Seedless
    b. Class 1: Seeded

    Ans: b


Q7. Suppose we have two more watermelons: one with length 41 cm and circumference 100 cm, and the other with length 52 cm and circumference 100 cm. Using the definition of distance provided in Section 9, find the distance between these two watermelons for use by a nearest neighbor classifier that has chosen length and circumference as the only two attributes.

    Ans: 11
 
Q8. What class will a 3-nearest neighbors classifier predict for a watermelon with length 41 cm and circumference 100 cm?

    a. Class 0: Seedless
    b. Class 1: Seeded

    Ans: b


Q9. What class will a 3-nearest neighbors classifier predict for a watermelon with length 52 cm and circumference 100 cm?

    a. Class 0: Seedless
    b. Class 1: Seeded

    Ans: a



