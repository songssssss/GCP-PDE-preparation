
# Neural Networks and Deep Learning
- Neural networks reflect the behavior of the human brain, allowing computer programs to recognize patterns and solve common problems in the fields of AI, machine learning, and deep learning.
- Weights and Biases are adjusted by a neural network as it learns from a training dataset

## Feature engineering
To learn more about features, click [here](https://github.com/singhgautam7/GCP-PDE-preparation---GRS/blob/main/study_material/others/ai_ml_terminologies.md)
### Definition
Manipulation of features to improve the quality and predictive capabilities of machine learning models. This is known as feature engineering.
### Steps
- Identify useful features
- Features may be in original data but might need some transformations
- Features derived from other features.
### Ways to engineering features
- Transform the orginal features
	- Ex: Lower case words and remove punctuation
	- Map Numeric valriable to a scale of 0 to 1 if the different features are from different numeric range (**Normalization**)
- Bucketing
	- Create sub-groups of feature values
	- This reduces number of values
- Feature cross	
	- Cartesian product of two or more features
	- Helps when there are non-linear relationships
- Binary features
	- Ex: is_red, is_blue etc
- Decompose values to parts
	- Ex: From date extract year, month and day

Certainly! Let's delve into the concepts of **crossed feature columns** and **bucketization of a continuous feature**. Both are techniques used in feature engineering to improve the performance of machine learning models.

### C. Crossed Feature Columns

**Crossed feature columns** involve creating new features by combining two or more existing features. This technique is particularly useful for capturing interactions between features that might be important for predicting the target variable.

#### Explanation:

1. **Concept**:
   - Crossing features means creating a new feature that represents the interaction between two or more features. For example, if you have features `A` (e.g., age) and `B` (e.g., gender), crossing these features could create a new feature like `A_B`, which combines `age` and `gender` into a single feature representing different age-gender combinations.

2. **Why Use Crossed Features?**:
   - **Interaction Effects**: Sometimes, the relationship between features can provide valuable information that individual features alone cannot. For instance, the effect of age on purchasing behavior might differ between genders.
   - **Non-linearity**: Crossed features help capture non-linear relationships between features that a simple linear model might miss.

3. **Implementation**:
   - **One-Hot Encoding**: In many implementations, crossed features are one-hot encoded, turning each unique combination of feature values into a binary column.
   - **Embedding**: In some models, especially neural networks, crossed features might be represented as embeddings to reduce dimensionality and capture interactions in a more compact form.

4. **Example**:
   - If you have two categorical features, `Country` (with values like 'USA', 'Canada') and `Product` (with values like 'Electronics', 'Clothing'), crossing these features would create new feature combinations like `Country_USA_Product_Electronics` and `Country_Canada_Product_Clothing`.

5. **Use Cases**:
   - Crossed features are used in various contexts, including recommendation systems, advertising, and other domains where feature interactions are crucial for accurate predictions.

### D. Bucketization of a Continuous Feature

**Bucketization** (or discretization) involves transforming a continuous feature into categorical bins or buckets. This technique is used to convert continuous variables into discrete categories to simplify the model or handle non-linear relationships.

#### Explanation:

1. **Concept**:
   - Bucketization divides the range of a continuous feature into discrete intervals or buckets. For example, if you have a continuous feature like `income`, you might bucketize it into ranges like `$0-$20k`, `$20k-$40k`, `$40k-$60k`, and so on.

2. **Why Use Bucketization?**:
   - **Handling Non-Linearity**: Bucketizing can help the model handle non-linear relationships between the continuous feature and the target variable.
   - **Simplifying Models**: Reducing a continuous feature to a limited number of categories can simplify the model and make it easier to interpret.
   - **Handling Outliers**: Bucketization can mitigate the impact of outliers by grouping extreme values into a single bucket.

3. **Implementation**:
   - **Equal-width Buckets**: Divide the range of the feature into intervals of equal width.
   - **Equal-frequency Buckets**: Divide the feature so that each bucket contains approximately the same number of data points.
   - **Custom Buckets**: Define buckets based on domain knowledge or specific criteria.

4. **Example**:
   - Suppose you have a continuous feature `age`. You might bucketize it into age groups: 0-18, 19-35, 36-50, 51-65, and 66+. Each age group is treated as a separate categorical feature.

5. **Use Cases**:
   - Bucketization is commonly used in decision trees and other models where handling continuous variables directly can be complex. It is also used in cases where certain thresholds or ranges have specific implications for the target variable.

### Summary

- **Crossed Feature Columns**: Create new features by combining two or more existing features to capture interactions and non-linear relationships. Useful for models that benefit from feature interactions.
- **Bucketization of a Continuous Feature**: Transform continuous features into categorical buckets to simplify modeling and handle non-linear relationships. Useful for making continuous variables more manageable and interpretable.

Both techniques are valuable tools in feature engineering that can help improve model performance by addressing specific characteristics of the data and relationships between features.

## One-Hot Encoding
- Map from an attribute value to a single bit in a binary array
- Each postion in array represent a possible value
- Ex: Red represent 100, Blue represent 010 and Green represent 001. Here we mapped colors to three different binary arrays

# Common Facts/Terminologies for examination

### Clustering
It is unsupervised learning technique for identifying group of similar entities

### Normalization
It is a transform that scales numeric value to the range 0 to 1

### Bucketing
It is used to convert a feature bin to multiple binary features that is typically based on a value range.
Ex: A grade for marks 80 - 100, B grade 60 - 79 and so on

### Regularization
Limiting the information captured by model to prevent overfitting.

### Overfitting
- Fits too well with the training data
- When the model performs great on the input(training) data but poorly on the test data
- Correction for overfitting: 
        - Regularization, which limits the amount of data captured.

### Underfitting
- When the model performs poorly on the input(training) data but great on the test data. 
- Correction for underfitting: 
        - Increase the complexity of model. Ex: Increase the number of layers in deep learning.
        - Increase the training time, epochs

### High Variance
 - Small changes in a few features leads to large differences in the output.
 - Low variance is desired

### High Bias
- Occurs when relationships are missed.
- Low bias is desired
- Happens when we do not generalize the training data enough 

<details><summary>Bias vs Variance</summary>
<p>

![enter image description here](https://community.alteryx.com/t5/image/serverpage/image-id/52874iE986B6E19F3248CF?v=v2)

</p>
</details>

### Learning rate
- Increasing the learning rate = Fast learning (at the risk of possibly missing the absolute optimal solution)
- Decreasing the learning rate = Slow learning

### Hyperparameters
- Hyperparameters are values that need to be selected before training process begins also can be modified during training
- Hyperparameters are parameters whose values control the learning process and determine the values of model parameters that a learning algorithm ends up learning.
- Ex: 
	- Learning Rate.
	- Number of Epochs.
	- Momentum.
	- Regularization constant.
	- Number of branches in a decision tree. 

### Difference between of Parameters and Hyperparameters
| Parameters | Hyperparameters |
|--|--|
| Estimated during the training with historical data | Values set beforehand |
| It is a part of the model | External to the model |
| The estimated value is saved with the trained model | Not a part of trained model, hence values aren't saved |
| Dependent on the dataset that the system is trained with | Independent of the dataset |

### Difference between of Features and Labels
|Features|Labels|
|--|--|
|Attribute of an entity|Attribute that is predicted|
|Describe characteristics of an entity|Category of an entity|
|Acts as I/P variable|Acts as O/P|

### Example of Features and Labels
|Features|Labels|
|--|:-:|
|No. of rooms, no. of bedrooms, size of kitchen, zip code etc.|Selling Price|
|Petal length, petal widh, sepal length, sepal width|Flower Species|
|Amount, product purchased, time of day, location|Fraud/Not Fraud|
|Age, occupation, zip code, no. of years of education|Income|

# Some other Terminologies
<details><summary>click to expand</summary>
<p>
	
### Tensorflow Terminologies
(Taken from this [link](https://medium.com/google-cloud/a-tensorflow-glossary-cheat-sheet-382583b22932))
-   **Train/Eval/Test** — Training is data used to optimize the model, evaluation is used to asses the model on new data during training with new data, test is used to provide the final result
-   **Classification/Regression —** Regression is prediction a number (e.g. housing price), classification is prediction from a set of categories or output classes (e.g. prediction the color of a house from red/blue/green).
-   **Linear regression-** A classic way of predicting an output by multiplying and summing input features with weights and biases. Useful for regression
-   **Logistic regression —** Similar to linear regression but predicts a probability, useful for classification.
-   **Neural network —** Like linear/logistic regression, but with the addition of an activation function, that makes it possible to predict outputs that are not linear combinations of inputs. Often intermediate layers of nodes are used “deep learning”.
-   **Weights / biases** — Weights are values that the input features are multiplied by to predict an output value. Biases are the value of the output given a weight of 0.
-   **Converge —** An algorithm that converges will eventually reach the optimal answer, even if very slowly. An algorithm that doesn’t converge may never reach the optimal answer.
-   **Learning rate**  — How quickly the optimizers changes weights and biases. Generally a high learning rate trains faster but risks not converging, whereas a lower rate trains slower
-   **Bias/Variance —** How much the output is determined by the features. more variance often can mean overfitting, more bias can mean a bad model
-   **Regularization**  — Variety of approaches to reduce overfitting, including adding the weights to the loss function, randomly dropping layers (dropout).
-   **Epochs** — How many times you run the optimization over the training data
-   **Batch size —** How many training examples you optimize for a time
-   **Ensemble learning** — Training multiple models with different parameters to solve the same problem
-   **Numerical instability —** Many deep learning algorithms can run issues with very large or very small values due to the limits of floating point number representations in computers
-   **Gradient explosion**- A common case of numerical instability
- **Label**: The correct classification/value
- **Input**: Predictor Variables - Example: Input + Label sample to train your model
- **Model**: Mathematical function, Some work is done on inputs for an output
- **Training**: Adjusting Variable weights in a model to minimize error
- **Prediction**: Using the model to guess the label for an input - Supervised Learning: Training your model using examples data to predict future data
- **Unsupervised Learning**: Data is analyzed without labels for patterns or clusters
- **Neuron**: A way to combine inputs and weighting them to make a decision (it is one unit of input combination)
- **Gradient Descent**: The process of testing error in order to minimize its value iteratively decreases towards a minimum. (This can be global or local maximum and starting points and learning rates are important to ensure the process doesn’t stop at local minima. Too low a learning rate and your model will train slowly, too high and it may miss the minimum)
- **Hidden Layer**: A set of neurons that act on the same input data.
- **Features**: The data values/fields you choose to model, these can be transformed (x^2, y^2, etc)
- **Feature Engineering**: The process of building a set of feature combinations to act on inputs
- **Precision**: The positive predictive value how many times it correctly predicted a thing as its classification (eg cat)
- **Recall**: The true positive rate, How many times a think is in the class (the actual number of cats)
- **Sparse Vector**: Sparse vector contains only 0 and 1, whereas only one 1

</p>
</details>
