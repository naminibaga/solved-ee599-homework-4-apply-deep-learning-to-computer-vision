Download Link: https://assignmentchef.com/product/solved-ee599-homework-4-apply-deep-learning-to-computer-vision
<br>
<p style="padding-left: 80px;">The goal of this assignment is to apply deep learning to computer vision. Particularly, you’ll work with the classification problem on a fashion compatibility dataset called Polyvore. Your goals will be to set up your category classifier and fashion compatibility classifier. Turn in your code and report as described in Section 5.

The starter code for this project can be found at https://github.com/davidsonic/EE599CV-Project but feel free to explore different hyper-parameters and model structures. Follow the instruction in the readme file to setup the codebase.

<h1>1             Dataset Description</h1>

<em>Polyvore Outfits </em>[1] is a real-world dataset created based on users’ preferences of outfit configurations on an online website named <em>polyvore.com</em>: items within the outfits that receive high-ratings are considered compatible and vice versa. It contains a total of 365,054 items and 68,306 outfits. The maximum number of items per outfit is 19. A visualization of an outfit is shown in Figure 1.

Figure 1: A visualization of a partial outfit in the dataset. The number at the bottom of each image is the ID of this item.

<h1>2             Category Classification</h1>

<ul>

 <li>The starter code provides the following files with blanks in them and can be read in this order. First, you need to set your dataset location in utils.py (Config[’root path’]).

  <ol>

   <li>train category.pytrain compat.py: training scripts</li>

   <li>py: CNN classification models</li>

   <li>py: dataset preparation</li>

   <li>py: utility functions and config</li>

  </ol></li>

 <li>Training takes place in train model function of train *.py. In each iteration, the model takes in batches of data provided by the dataloader (data.py). Record your training acc progress here, which will be used for plotting the learning curve.</li>

 <li>You’re expected to do finetuning and training from scratch.

  <ol>

   <li>Finetune a model pretrained on ImageNet (e.g, ResNet50). Frameworks nowadaysprovide easy access to those, refer to documentations online.</li>

   <li>Construct a model of your own and start training from scratch.</li>

   <li>Compare these two models and record the results. What is the advantage of usinga finetuned model? What’s the difference between the learning rates when you apply these two learning strategies (i.e finetuning vs from scratch)?</li>

  </ol></li>

</ul>

<strong>Note: </strong>images are located in images folder, each image is named by its id. Information for the item are stored in polyvore item metadata.json.

<ul>

 <li>Modify data.py to create data pairs (image, category label). Normalization is defined in get data transforms function.</li>

 <li>Split no less than 10% data for validating your final model. The test set is test category hw.txt.</li>

 <li><strong>Tips:</strong>

  <ol>

   <li>Over-fitting is expected. Play with model structure and hyper-parameter or regularization to reduce over-fitting. You can design any model structure you like.</li>

   <li>To speed up the training speed, you can set “use cuda” flag to true and increase the batch size defined in utils.py.</li>

   <li>You can restrict the size of the dataset for quick debugging. Set debug=True inutils.py. You do not necessarily need to use 20 epochs and the entire training set.</li>

   <li>It may take more than several epochs before the performance plateaus, dependingon the network structure you use and the learning rate.</li>

  </ol></li>

</ul>

<h1>3             Pairwise Compatibility Prediction</h1>

The task is to predict the compatibility of an outfit (Figure 2). It’s essentially a binary classification problem (compatible or incompatible), however, the difficulty of the task lies in the input–classify based on a set rather than a single item as you did in the last section. One idea to deal with set classification is to decompose it into pairwise predictions (you’re encouraged to propose different ideas for the bonus section). Therefore, you’ll first train a pairwise compatibility classifier.

Figure 2: Examples of a compatible item and an incompatible item.

<ul>

 <li>Modify data.py to create a new dataloader that takes in a pair of image inputs (compatible pair and incompatible pair). For example, let’s assume any pair of items in a compatible outfit are considered compatible whereas an incompatible outfit provides negative pairs.</li>

 <li>Modify model.py to create a new model that takes in a pair of inputs and outputs a compatbility probability for this pair.</li>

 <li>Split no less than 10% your data for validation. The test set is test pairwise compat hw.txt.</li>

 <li><strong>Bonus</strong>: Make outfit compatibility prediction based on pairwise predictions (i.e, average over n(n-1)/2 pairwise scores and then set a threshold for outfit compatibility). The test set is compatibility test hw.txt.</li>

 <li><strong>Tips:</strong>

  <ol>

   <li>Outfit descriptions are located in compatibility *.txt. Each line shows the compatibility of the outfit and its items. (e.g, 1 210750761 1 210750761 2 210750761 3: a compatible outfit id, whose outfit id is 210750761. It has three items, indexing from 1 to 3).</li>

   <li>Item ids and descriptions are located in polyvore item metadata.json. Their corresponding images are also indicated by item ids.</li>

   <li>To associate items in an outfit with their item id, you need to parse train.json/val.json.</li>

  </ol></li>

</ul>

<h1>4             Extra Bonus</h1>

Considering this is a real-world data and that fashion compatibility prediction is an open problem. You’re encouraged to refine the performance by adding various tricks.

<ul>

 <li>Perform learning rate scheduling</li>

 <li>Perform data augmentation to increase robustness</li>

 <li>Perform hard-negative mining for pairwise compatibility prediction</li>

 <li>Learn a permutation invariant feature for the entire set for compatibility prediction</li>

</ul>

.