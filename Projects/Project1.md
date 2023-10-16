# Project 1 

## The Assignment
"This project focuses on a constrained search problem: finding an exact match pattern, variably
scaled in an image array (such as a specific face or pose that appears within a crowd scene). In
this assignment, we will focus on finding George P. Burdell, whose mugshot is shown in Figure
1, in an image that contains a crowd of faces, such as the sample scene in Figure 2. The faces in
the scene, including George's, may be at varying distances from the camera, so they may appear
scaled." 

Here is a sample test case of where to find George (Figure 2): 

<img width="282" alt="image" src="https://github.com/sgandikota100/ECE-2035-Programing-HW-SW-Systems/assets/113190903/1b9b3c22-53b8-44e1-86f6-5dd38b3d1674">

There are other criterias for the search to help simplify our code. The test cases, known as a crowd scene, is given in a 64 x 64 image array of pixels. Each pixel creates a word that contains 4 colors coded in little endian byte ordering. There are 10 total pixels, 7 of which are designated to be on facial features. The remain 3 are background colors. A diagram from the project PDF is shown below: 

<img width="525" alt="image" src="https://github.com/sgandikota100/ECE-2035-Programing-HW-SW-Systems/assets/113190903/87caaafe-1140-4205-a4f6-d353f686cc9a">

George will always look the same, but possibly scaled. However, important to consider the the variant of George which could "misuse" the features of George (which make the code a bit more inefficient).
All faces are facing forward and upright. They won't be mirrored either. Just possibly scaled by a scale factors ranging from 1 - 5. 

## What I learned 
The first step of this project was a High Level implementation in C. Only accuracy was mattered in order to familarize the problem. 

George has a few distinct features that make him George: 
<img width="126" alt="image" src="https://github.com/sgandikota100/ECE-2035-Programing-HW-SW-Systems/assets/113190903/ec184446-0f43-4e35-9653-f2da0e0b91fc">

- He always has a red hat with horizontal stripes
- He has a yellow face with NO glasses
- He has a smile :)
- He has a green shirt
