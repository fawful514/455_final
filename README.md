# Creating an Engine-Readable Notation from a Chess Diagram

Source code can be found [here](https://github.com/fawful514/455_final/blob/gh-pages/Chess_Vision.ipynb) in my Jupyter Notebook and available on [Google Colab](https://colab.research.google.com/drive/1OkZM3U4HsIIXVX5CmT4-wwfZzSpJKV-0?usp=sharing).

## Abstract
In this project, I explored applying a computer vision model to an image of chess diagram to record the current position of the pieces. Using the knowledge I learned from the course, I applied image resizing, color adjustment, and neural network training on an dataset of 6400 images of chess pieces of various styles. With minor adjustments to the base networks provided, I was able to reach a training accuracy of 90-95%.

[A video detailing this process](https://github.com/fawful514/455_final/blob/gh-pages/2022-03-16%2020-54-06.mkv)

## Introduction
A game as old as time, chess is a game played by two players on a board of 64 squares - 32 white squares and 32 black squares. Each player has 16 pieces: 8 pawns, 2 knights, 2 bishops, 2 rooks, a king, and a queen. Although traditionally played on a physical board, online chess has seen a massive surge in popularity recently. In place of physical boards and pieces, online chess utilizes a chess diagram. This system uses symbols on a screen to represent the pieces. Focusing on chess diagrams, I set out to convert a plain image of a chess diagram to a FEN string detailing the current layout of the game.

This project was very similar to Homework 5 where we processed input and trained a model using varied learning rate, weight, momentum, and decay.

![Basic chess diagram](https://github.com/fawful514/455_final/blob/gh-pages/images/better%20diagram.PNG)

## Motivation

In the last few years, I have been playing quite a bit of online chess. This includes practicing numerous online chess puzzles. Frequently, these puzzles are simply images on a website with a caption describing which color moves next and sometimes how many moves for the solution. The problem with this approach arises when it is time to check the solution I found. I find myself meticulously arranging pieces on a chess engine website like [nextchessmove.com](https://nextchessmove.com/). It would be much easier to simply screenshot the diagram and quickly convert the position into a engine-readable notation. This project aims to fulfill that niche.


## Approach

### Data Collection

The dataset I used for this project was found on [GitHub](https://github.com/IlicStefan/ChessDiagramRecognition) through a kaggle page. It contains 6400 images of chess pieces on squares, half on white squares and half on dark squares. The data had a uniform size, so I simply needed to convert each image to greyscale for easier use. The data was stored in such a way that there were 26 subdirectories containing only images of a single piece, so using a Python script I was able to parse the entire directory and create my `chess_pieces.csv` file containing label information for each piece. Splitting the pieces into  85/15 train-test, I used Pytorch's DataLoader to begin the training.

### Neural Network

This part of the project was fairly simple thanks to the clean and simple dataset I had. Using the template provided for us in Pytorch Tutorial 1, I simply had to adjust my input values, learning rate, momentum, and decay until I reached a satisfactory result. I tried adding more layers, but the results did not improve. After a bit of tinkering, I was able to reach a training accuracy of 93.8% and a testing accuracy of 93.1% with a loss of ~0.300 using 25 epochs. 

![Testing plot](https://github.com/fawful514/455_final/blob/gh-pages/images/testing%20plot.png)

## Applying the Model

### More Data Collection

With the model trained and saved, it was time to move to the most difficult portion of the project. The model was only trained on uniformly sized images of individual chess pieces, but I wanted to analyze the entire chess diagram. For this, I needed to acquire another dataset of clean images of chess diagrams. The same GitHub repo had a handful of chess diagrams, but they were not uniform shape or size. I quickly resized the images and once again converted them to greyscale. The data was now ready for the model.

![Dataset Diagram](https://github.com/fawful514/455_final/blob/gh-pages/images/d74.jpg)

### Breaking Apart the Diagram

Once the model was loaded and instantiated, it was ready for my data. The model, however, only took images of individual pieces. There is no way it could perform accurately with just an image of a chess diagram. To circumvent this issue, I split the images of the diagrams into 64 uniform squares. Using some resizing tricks and numpy arrays, I was able to effectively seek out each individual square to feed to the model. Using each evaluation of the model, I carefully stepped square by square to predict what piece occupied each square of the diagram. With the predictions all collected, I converted the results to Forsyth-Edwards Notation (FEN), a string used by chess engines to understand the layout of the game.

Full understanding of the notation isn't important, but lowercase letters denote black's pieces, uppercase letters denote white's pieces, and the numbers indicate how many squares in a row are empty. The slashes indicate the end of a row.

`r1n2rk1/pp2p2p/3pbpp1/8/2PPPP2/1P6/P5PP/P4RK1 w - - 0 1`

## Results

The results of this project were slightly lackluster. As expected, the model did not perform at the tested ~90%. This is certainly due to the resizing of images to fit the restrictions of the model. Images close to 256x256 pixels performed the best, as the model was trained on images of size 32x32. From inspecting the results, it appears that the model is accurate ~70% of the time. While 70% may seem decent, it often leads to kings being mistaken for empty squares, something that is impossible in a game of chess. Overall, the results are still exciting as the output usually follows a similar shape to the diagram, with just a piece missing or mistaken here or there.

The origial diagram: 

![d15 Diagram](https://github.com/fawful514/455_final/blob/gh-pages/images/d15.jpg)

The diagram from FEN output: 

![d15 FEN](https://github.com/fawful514/455_final/blob/gh-pages/images/d15%20FEN%20Output.PNG)

## Discussion

As stated earlier, I am mostly happy with the results. It clearly is not a perfect product, but it certainly is exciting to see what progress can be made. Some of the limitations of an implementation like this is the lack of context required to evaluate chess positions. From just an image, there is no way to know who's turn it is to move, whether either player can castle, and other factors that affect the evaluation of the position. In the future, I would love to collect my own data to tighten up the uniformity of the model. I also would like to directly implement this with an online chess engine, perhaps through some API. There is a lot of space for this project to grow, but the foundation created here is promising and inspiring.
