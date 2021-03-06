# Section 7: Regression Inference (Lec 7.1 - Lec 7.3)

+ [Launching Web Page](https://courses.edx.org/courses/course-v1:BerkeleyX+Data8.3x+2T2018/courseware/9e3318ad6da44461990e1d4e3a64986f/4f90f7d56ed74420b5b641cdb0fedc65/?child=first)
+ [Web Notebook](https://hub.data8x.berkeley.edu/user/37b80bfacc52ea5dfdad124579807188/notebooks/materials-x18/lec/x18/3/lec7.ipynb#)
+ [Local notebook](./notebooks/lec7.ipynb)
+ [Local Python Code](./notebooks/lec7.py)

+ Common Functions for Linear Regression
    ```python
    def standard_units(any_numbers):
        """Convert any array of numbers to standard units."""
        return (any_numbers - np.average(any_numbers)) / np.std(any_numbers)

    def correlation(t, x, y):
        """Return the correlation coefficient (r) of two variables."""
        return np.mean(standard_units(t.column(x)) * standard_units(t.column(y)))

    def slope(t, x, y):
        """The slope of the regression line (original units)."""
        r = correlation(t, x, y)
        return r * np.std(t.column(y)) / np.std(t.column(x))

    def intercept(t, x, y):
        """The intercept of the regression line (original units)."""
        return np.mean(t.column(y)) - slope(t, x, y) * np.mean(t.column(x))

    def fit(t, x, y):
        """The fitted values along the regression line."""
        a = slope(t, x, y)
        b = intercept(t, x, y)
        return a * t.column(x) + b

    def plot_residuals(t, x, y):
        """Plot a scatter diagram and residuals."""
        t.scatter(x, y, fit_line=True)
        actual = t.column(y)
        fitted = fit(t, x, y)
        residuals = actual - fitted
        print('r:', correlation(t, x, y))
        print('RMSE:', np.mean(residuals**2)**0.5)
        t.select(x).with_column('Residual', residuals).scatter(0, 1)
    ```

## Lec 7.1 Regression Model

### Note

+ A “Model”: Signal + Noise
    <a href="https://courses.edx.org/courses/course-v1:BerkeleyX+Data8.3x+2T2018/courseware/9e3318ad6da44461990e1d4e3a64986f/4f90f7d56ed74420b5b641cdb0fedc65/?child=first">
        <br/><img src="./diagrams/lec7-1.png" title= "Regression model" alt="A regression line represents the distance between the regression values and observed values" width="450">
    </a>

+ Demo
    ```python
    def draw_and_compare(true_slope, true_int, sample_size):
        x = np.random.normal(50, 5, sample_size)
        xlims = np.array([np.min(x), np.max(x)])
        errors = np.random.normal(0, 6, sample_size)
        y = (true_slope * x + true_int) + errors
        sample = Table().with_columns('x', x, 'y', y)
        
        sample.scatter('x', 'y')
        plots.plot(xlims, true_slope*xlims + true_int, lw=2, color='green')
        plots.title('True Line, and Points Created')
        
        sample.scatter('x', 'y')
        plots.title('What We Get to See')
        
        sample.scatter('x', 'y', fit_line=True)
        plots.title('Regression Line: Estimate of True Line')
        
        sample.scatter('x', 'y', fit_line=True)
        plots.plot(xlims, true_slope*xlims + true_int, lw=2, color='green')
        plots.title('Regression Line and True Line')
        
    draw_and_compare(2, -5, 10)
    draw_and_compare(2, -5, 100)
    draw_and_compare(2, -5, 1000)
    ```

### Video

<a href="https://edx-video.net/BERD83FD2018-V002600_DTH.mp4" alt="Lec 7.1 Regression Model" target="_blank">
    <img src="http://files.softicons.com/download/system-icons/windows-8-metro-invert-icons-by-dakirby309/png/64x64/Folders%20&%20OS/My%20Videos.png" alt="Video" width="60px"> 
</a>

## Lec 7.2 Prediction Variability

### Note

+ Regression Prediction
    + If the data come from the regression model,
    + and if the sample is large, then:
    + The regression line is close to the true line
    + Given a new value of $x$, predict $y$ by finding the point on the regression line at that $x$

+ Confidence Interval for Prediction
    + Bootstrap the scatter plot
    + Get a prediction for $y$ using the regression line that goes through the resampled plot
    + Repeat the two steps above many times
    + Draw the empirical histogram of all the predictions.
    + Get the “middle 95%” interval.
    + That’s an approximate 95% confidence interval for the height of the true line at $y$.

+ Predictions at Different Values of $x$
    + Since y is correlated with $x$, the predicted values of $y$ depend on the value of $x$.
    + The width of the prediction interval also depends on $x$.
        + Typically, intervals are wider for values of $x$ that are further away from the mean of $x$.

+ Demo
    ```python
    baby = Table.read_table('baby.csv')
    # Birth   Gestational Maternal    Maternal    Maternal            Maternal
    # Weight  Days        Age         Height      Pregnancy Weight    Smoker
    # 120     284         27          62          100                 False
    # 113     282         33          64          135                 False
    # 128     279         28          64          115                 True
    # ... (rows omitted)

    plot_residuals(baby, 'Gestational Days', 'Birth Weight')
    # r: 0.4075427933888511
    # RMSE: 16.730358256655432

    x = 300
    a = slope(baby, 'Gestational Days', 'Birth Weight')
    b = intercept(baby, 'Gestational Days', 'Birth Weight')
    predicted_y = a * x + b
    baby.scatter('Gestational Days', 'Birth Weight', fit_line=True)
    plots.scatter(300, predicted_y, color='gold', s=200);

    predicted_y     # 129.2129241703143

    def prediction_at(t, x):
        a = slope(t, 'Gestational Days', 'Birth Weight')
        b = intercept(t, 'Gestational Days', 'Birth Weight')
        return a * x + b

    for i in np.arange(4):
        resample = baby.sample()
        predicted_y = prediction_at(resample, 300)
        resample.scatter('Gestational Days', 'Birth Weight', fit_line=True)
        plots.scatter(300, predicted_y, color='gold', s=200)

    # draw 10 different regression lines
    lines = Table(['slope', 'intercept', 'at 150', 'at 300', 'at 350'])

    for i in range(10):
        resample = baby.sample()
        a = slope(resample, 'Gestational Days', 'Birth Weight')
        b = intercept(resample, 'Gestational Days', 'Birth Weight')
        lines.append([a, b, a * 150 + b, a * 300 + b, a * 350 + b])
        
    baby.scatter('Gestational Days', 'Birth Weight')
    for i in np.arange(lines.num_rows):
        line = lines.row(i)
        plots.plot([150, 350], [line.item('at 150'), line.item('at 350')], lw=1)
        plots.scatter(300, line.item('at 300'), s=200)

    # zoom in @ x=300 around
    lines = Table(['slope', 'intercept', 'at 291', 'at 300', 'at 309'])

    for i in range(10):
        resample = baby.sample()
        a = slope(resample, 'Gestational Days', 'Birth Weight')
        b = intercept(resample, 'Gestational Days', 'Birth Weight')
        lines.append([a, b, a * 291 + b, a * 300 + b, a * 309 + b])
        
    for i in np.arange(lines.num_rows):
        line = lines.row(i)
        plots.plot([291, 309], [line.item('at 291'), line.item('at 309')], lw=1)
        plots.scatter(300, line.item('at 300'), s=30)

    def bootstrap_prediction(table, x, y, new_x, repetitions=5000):
        # Bootstrap resampling
        predictions = []
        for i in np.arange(repetitions):
            resample = table.sample()
            a = slope(resample, x, y)
            b = intercept(resample, x, y)
            predicted_y = a * new_x + b
            predictions.append(predicted_y)

        # Find the ends of the approximate 95% prediction interval
        left = percentile(2.5, predictions)
        right = percentile(97.5, predictions)

        # Display results
        Table().with_column('Prediction', predictions).hist(bins=20)
        plots.xlabel('predictions at x='+str(new_x))
        plots.plot([left, right], [0, 0], color='yellow', lw=8);
        print('Approximate 95%-confidence interval for height of true line:')
        print(left, right, '(width =', right - left, ')')

    # CI @ 280 narrower than CI @ 300 & 330
    bootstrap_prediction(baby, 'Gestational Days', 'Birth Weight', 300)
    # Approximate 95%-confidence interval for height of true line: 127.31138623489576 131.34398739036294 (width = 4.032601155467177 )

    bootstrap_prediction(baby, 'Gestational Days', 'Birth Weight', 330)
    # Approximate 95%-confidence interval for height of true line: 138.7471293196391 147.7679833940758 (width = 9.020854074436699 )

    bootstrap_prediction(baby, 'Gestational Days', 'Birth Weight', 280)
    # Approximate 95%-confidence interval for height of true line: 118.94357663343759 120.83354105018853 (width = 1.8899644167509422 )
    ```

### Video

<a href="https://edx-video.net/BERD83FD2018-V002700_DTH.mp4" alt="Lec 7.2 Prediction Variability" target="_blank">
    <img src="http://files.softicons.com/download/system-icons/windows-8-metro-invert-icons-by-dakirby309/png/64x64/Folders%20&%20OS/My%20Videos.png" alt="Video" width="60px"> 
</a>

## Lec 7.3 The True Slope

### Note

+ Confidence Interval for True Slope
    + Bootstrap the scatter plot.
    + Find the slope of the regression line through the bootstrapped plot.
    + Repeat.
    + Draw the empirical histogram of all the generated slopes.
    + Get the “middle 95%” interval.
    + That’s an approximate 95% confidence interval for the slope of the true line.

+ Rain on the Regression Parade
    <a href="url">
        <br/><img src="./diagrams/lec7-2.png" title= "caption" alt="Regression slope" width="350">
    </a>

+ Test Whether There Really is a Slope
    + __Null hypothesis__: The slope of the true line is 0.
    + __Alternative hypothesis__: No, it’s not.
    + Method:
        + Construct a bootstrap confidence interval for the true slope.
        + If the interval doesn’t contain 0, reject the null hypothesis.
        + If the interval does contain 0, there isn’t enough evidence to reject the null hypothesis.

+ Demo
    ```python
    slope(baby, 'Gestational Days', 'Birth Weight')     # 0.4665568769492152

    # resample 4 times with similar regression lines
    for i in np.arange(4):
        baby.sample().scatter('Gestational Days', 'Birth Weight', fit_line=True)

    baby.scatter('Gestational Days', 'Birth Weight')
    for i in np.arange(4):
        resample = baby.sample()
        s = slope(resample, 'Gestational Days', 'Birth Weight')
        c = intercept(resample, 'Gestational Days', 'Birth Weight')
        xlims = make_array(150, 350)
        plots.plot(xlims, s*xlims + c, lw=4)

    baby.num_rows               # 1174
    baby.sample().num_rows      # 1174

    slopes = []
    for i in np.arange(5000):
        resample = baby.sample()
        resample_slope = slope(resample, 'Gestational Days', 'Birth Weight')
        slopes.append(resample_slope)
    Table().with_column('Bootstrap Slopes', slopes).hist(bins=20)

    left = percentile(2.5, slopes)
    right = percentile(97.5, slopes)
    [left, right]       # [0.38403181781352447, 0.560962450953542]

    # 5000 different slopes
    def bootstrap_slope(table, x, y, repetitions=5000):
        
        # Bootstrap resampling
        slopes = []
        for i in np.arange(repetitions):
            resample = table.sample()
            resample_slope = slope(resample, x, y)
            slopes.append(resample_slope)
        
        # Find the endpoints of the 95% confidence interval for the true slope
        left = percentile(2.5, slopes)
        right = percentile(97.5, slopes)
        
        # Slope of the regression line from the original sample
        observed_slope = slope(table, x, y)
        
        # Display results
        Table().with_column('Bootstrap Slopes', slopes).hist(bins=20)
        plots.plot([left, right], [0, 0], color='yellow', lw=8);
        print('Slope of regression line:', observed_slope)
        print('Approximate 95%-confidence interval for the true slope:')
        print(left, right)
        
    bootstrap_slope(baby, 1, 0)
    # Slope of regression line: 0.4665568769492152
    # Approximate 95%-confidence interval for the true slope: 0.3825996089892574 0.5558900672708974

    plot_residuals(baby, 2, 1)
    # r: -0.053424773507798104  RMSE: 15.980630030890573

    bootstrap_slope(baby, 2, 1)
    # Slope of regression line: -0.14702142270280957
    # Approximate 95%-confidence interval for the true slope: -0.3043433713081157 0.002489069633700973
    ```

### Video

<a href="https://edx-video.net/BERD83FD2018-V002500_DTH.mp4" alt="Lec 7.3 The True Slope" target="_blank">
    <img src="http://files.softicons.com/download/system-icons/windows-8-metro-invert-icons-by-dakirby309/png/64x64/Folders%20&%20OS/My%20Videos.png" alt="Video" width="60px"> 
</a>

## Reading and Practice

### Reading

This guide assumes that you have watched the videos for Section 7.

This corresponds to textbook section:

[Chapter 16.1: A Regression Model](https://www.inferentialthinking.com/chapters/16/1/Regression_Model)

[Chapter 16.2: Inference for the True Slope](https://www.inferentialthinking.com/chapters/16/2/Inference_for_the_True_Slope)

[Chapter 16.3: Prediction Intervals](https://www.inferentialthinking.com/chapters/16/3/Prediction_Intervals)

In section 7, we learned about the regression model and regression inference. The regression model states that our scatter plot of data resembles points generated by adding random noise (that satisfies specific assumptions about the randomness) to points originally along a straight line (the true line). We approximate the true line by finding the regression line.

If we believe that this model holds true for our data, then we can apply the inference techniques we already know to draw conclusions about unknown parameters of the model.

Let's review the process.


### Practice

Q1. When we bootstrap a scatter plot, we sample the x and y variables independently.

Ans: False


Q2. The fitted value at a given x is the regression estimate of y based on that x.

Ans: True


Q3. Suppose we believe that the assumptions of the regression model are valid for our scatter plot. Order the steps in the process for testing whether the regression slope we are seeing is real, or just due to sampling variability.

    Step 1: State the null hypothesis (true slope is 0) and alternative (true slope is not 0).
    Step 2: Specify the desired P-value cutoff and the corresponding confidence level.
    Step 3: Assume the null hypothesis is true.
    Step 4: Use the bootstrap to generate new random samples based on the original sample.
    Step 5: Find the regression slope based on each resampled scatter plot.
    Step 6: Use percentiles of all the slopes to construct a confidence interval for the true slope.
    Step 7: If 0 is in the interval, reject the null. Otherwise fail to reject the null.





