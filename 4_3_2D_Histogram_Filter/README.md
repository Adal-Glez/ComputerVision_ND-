# Localization Problem in Robotics : 2D Histogram Filter
### Adalberto Gonzalez

Computer Vision Nanodegree Program

# Overview
In this project, I've implemented a 2-Dimensional histogram/bayesian filter to locate a robot in space and represent uncertanty in robot motion.

<img src="https://github.com/Adal-Glez/ComputerVision_ND-/blob/master/4_3_2D_Histogram_Filter/2dfilter.png"/> 



## highlights

Complete the `sense` function at `localizer.py` 
and pass the test passes.

As we can see everything is working correctly you should see the beliefs
converge to a single large circle at the same position as the 
red star.

```python
def sense(color, grid, beliefs, p_hit, p_miss):
    new_beliefs = []
    for r in range(len(grid)):
        rb=[]
        for c in range(len(grid[r])):
            #print(grid[r][c])
            hit = (color == grid[r][c])
            rb.append(beliefs[r][c] * (hit * p_hit + (1-hit) * p_miss))
        new_beliefs.append(rb)
    #print(len(beliefs),len(new_beliefs))
...    
```
### debug
a bug appeared at
---> 40             new_G[int(new_i)][int(new_j)] = cell
was fixed and annotated.
```python
def move(dy, dx, beliefs, blurring):
    height = len(beliefs)
    width = len(beliefs[0])
    new_G = [[0.0 for i in range(width)] for j in range(height)]
    for i, row in enumerate(beliefs):
        for j, cell in enumerate(row):
            #switch height and width, not detected in wquare world
            new_i = (i + dy ) % height
            new_j = (j + dx ) % width
            #pdb.set_trace()
            new_G[int(new_i)][int(new_j)] = cell
    return blur(new_G, blurring)
```
