## CSE 455 Chess Computer Vision Project

Source code can be found [here](https://colab.research.google.com/drive/1OkZM3U4HsIIXVX5CmT4-wwfZzSpJKV-0?usp=sharing) in my Jupyter Notebook available on Google Colab.

### Abstract
In this project, I explored applying a computer vision model to an image of chess diagram to record the current position of the pieces. Using the knowledge I learned from the course, I applied image resizing, color adjustment, and neural network training on an dataset of 6400 images of chess pieces of various styles. With minor adjustments to the base networks provided, I was able to reach a training accuracy of 90-95%.

[A video detailing this process]()

### Introduction and Motivation
A game as old as time, chess is a game played by two players on a board of 64 squares - 32 white squares and 32 black squares. Each player has 16 pieces: 8 pawns, 2 knights, 2 bishops, 2 rooks, a king, and a queen. Although traditionally played on a physical board, online chess has seen a massive surge in popularity recently. In place of physical boards and pieces, online chess utilizes a chess diagram. This system uses symbols on a screen to represent the pieces. Focusing on chess diagrams, I set out to convert a plain image of a chess diagram to a FEN string detailing the current layout of the game.

This project was very similar to Homework 5 where we processed input and trained a model using varied learning rate, weight, momentum, and decay.




```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [Basic writing and formatting syntax](https://docs.github.com/en/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/fawful514/455_final/settings/pages). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
