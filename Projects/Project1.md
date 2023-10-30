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

For these guidelines, here was the baseline: 90 static instructions, 2400 dynamic instructions (avg.), and 17 words storage (not including the 1024 alloc for array and 2 decicated registers). 

## What I learned 
The first step of this project was a High Level implementation in C. Only accuracy was mattered in order to familarize the problem. Afterwards, the second part of the project was the MIPS implementation that MUST meet or be below the given baseline values for static instructions, dynamic instructions, and words of data used. 

George has a few distinct features that make him George: 
<img width="126" alt="image" src="https://github.com/sgandikota100/ECE-2035-Programing-HW-SW-Systems/assets/113190903/ec184446-0f43-4e35-9653-f2da0e0b91fc">

- He always has a red hat with horizontal stripes
- He has a yellow face with NO glasses
- He has a smile :)
- He has a green shirt

My C implementation played around with an idea thrown out durring class. Nothing special here. When it came to the MIPS implementation, I knew it was very ineffecient because I used two nested for-loops to traverse the array, along with additional loops and conditional statements (I'm assuming $O(n^3)$ in the most generous case). 

In order to create the most effcient algorithm, I need to start by chosing a feature of George that is the least prevalent on him and his peers. With that in mind, I then had to choose a starting point to traverse the array where I would quickly encounter this feature. I ended up using a single for-loop to decrease my dynamic instruction count. I also did not check every single pixel of the array, but rather skipped by $n$ pixels, where $n$ is the length of the feature. If I found a 

Once the feature was found, I had to determine if I had the right face, or let alone, the right feature (the edge cases would mix up the location of the colors of George varients!). After several versions of the code, I ended up using small loops that help me determine my feature. In other words, I ensured that I was at specific anchor point by using short loops that don't overload the instruction count. 

Afterwards, with using the scale, you can relavitly determine how to check various features of the face. Using a bit of algebra, I decreased the number of calculations by using the old value of a feature in a register to determined what to add to get to the desired value. Here's an example: 

<img width="107" alt="image" src="https://github.com/sgandikota100/ECE-2035-Programing-HW-SW-Systems/assets/113190903/d0057f1b-f89e-47ce-92d5-e02c645474aa">

In this picture of a George varient, let's assume the current feature is the eye. The address for the byte is stored in some register. Becuase my scale factor is 1, I just need to go down 2 blocks and right 1 block. My first attempt wrote it in terms for a row variable, `i`, and a column variable, `j`, but it's much more effecient to simply shift the current address down 2 two (add 128 bytes) plus right 1 (add 1 more byte). And using shifting bits rather than multiplying makes it much faster. 

My final statistics were as follows: 

80 static instructions, 1037 dynamic instructions, 8 words of storage required

Pretty good benchmarks that crush the baseline of 90 static, 2,400 dynamic, and 17 words of storage 😎
